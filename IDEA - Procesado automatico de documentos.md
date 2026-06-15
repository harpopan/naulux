---
fecha: 2026-05-27
version: "1.0"
idioma: es
estado: borrador
---

# META — Procesado automático de documentos

> [!summary] Resumen
> Análisis de opciones para que el pipeline Nautilus procese documentos de forma autónoma en cuanto aparecen en `documentos_bruto/`, sin necesidad de ejecutar `procesa` manualmente.

---

## Contexto

Actualmente el pipeline solo se activa bajo demanda con el comando `procesa`. Esto requiere que el usuario abra opencode y lo ejecute explícitamente. Este documento explora las alternativas para automatizar ese paso.

---

## Opción 1 — Watch (sesión interactiva)

Un comando `procesa --watch` que inicia un vigilante en la terminal usando `inotifywait`.

**Cómo funciona:**
- Se lanza dentro de una sesión de opencode
- Usa `inotifywait` (Linux) para monitorizar `documentos_bruto/`
- Cuando detecta un archivo nuevo (evento `close_write` o `moved_to`), ejecuta el pipeline completo: leer, traducir, clasificar, estructurar y mover
- El agente procesa los documentos en tiempo real

**Ventajas:**
- Sin APIs externas — usa el mismo agente que ya tiene el pipeline
- Sin infraestructura adicional
- El agente aplica toda la inteligencia (traducción natural, clasificación contextual)

**Limitaciones:**
- La sesión de opencode debe estar abierta
- Consume terminal — la sesión no puede usarse para otra cosa
- Solo funciona mientras el agente esté activo

**Implementación mínima:**
```bash
inotifywait -m documentos_bruto/ -e close_write -e moved_to |
  while read dir action file; do
    echo "procesa \"$file\""
  done
```

---

## Opción 2 — Script autónomo externo

Un script en bash o Python independiente que procesa documentos sin necesidad de opencode.

**Cómo funciona:**
- Usa `inotifywait` para detectar archivos nuevos
- Llama a una API de LLM (Claude API, OpenAI, etc.) para cada paso:
  - Traducción: endpoint de chat con instrucción de idioma
  - Clasificación: prompt que asigna el prefijo taxonómico
  - Generación de frontmatter y resumen
- Aplica la taxonomía localmente y mueve el archivo

**Ventajas:**
- Corre en segundo plano (daemon, systemd, screen/tmux)
- No requiere sesión de opencode
- Puede ejecutarse en un servidor o VPS

**Limitaciones:**
- Requiere API key y consume créditos por documento
- El prompt de clasificación hay que diseñarlo y mantenerlo
- No tiene el contexto del agente — decisiones más rígidas
- Coste recurrente por cada documento procesado

**Coste estimado (Claude API):**
- Un documento de ~500 palabras → ~0,01-0,03 USD por traducción + clasificación
- 50 documentos/mes → ~0,50-1,50 USD/mes

---

## Opción 3 — Notificador + agente manual

Un script ligero que solo avisa cuando llega algo nuevo y el agente se encarga del trabajo pesado.

**Cómo funciona:**
- Script `vigia.sh` que se ejecuta en segundo plano
- Usa `inotifywait` para detectar archivos nuevos
- Al detectar uno, lanza una notificación:
  - Echo en terminal: `* Nuevo documento: X — ejecuta 'procesa X'`
  - Notificación del sistema (`notify-send` en Linux)
  - Log en un archivo `_pendientes.log`
- El usuario abre opencode y ejecuta `procesa` (o `procesa X`)
- El agente aplica el pipeline completo

**Ventajas:**
- Casi cero implementación — script de 10 líneas
- Sin APIs ni costes
- El agente sigue haciendo el trabajo inteligente

**Limitaciones:**
- Sigue requiriendo intervención manual para ejecutar `procesa`
- Útil como recordatorio, no como automatización completa

**Ejemplo de script notificador:**
```bash
#!/bin/bash
inotifywait -m ~/nautilus-agents-workers/documentos_bruto/ \
  -e close_write -e moved_to --format '%f' |
  while read file; do
    [[ "$file" == _procesados/* ]] && continue
    echo "[$(date +%H:%M)] Nuevo documento: $file"
    echo "→ Ejecuta: procesa \"$file\""
    notify-send "Nautilus" "Nuevo documento: $file" 2>/dev/null || true
  done
```

---

## Opción 4 — GitHub Actions (si el repo está en GitHub)

Un workflow que se ejecute al hacer push a `documentos_bruto/`.

**Cómo funciona:**
- Trigger: `on: push: paths: ['documentos_bruto/**']`
- El workflow ejecuta un script que:
  - Detecta los archivos nuevos respecto al commit anterior
  - Llama a una API de LLM (con secret almacenado en GitHub Secrets)
  - Traduce, clasifica y estructura
  - Hace commit del resultado en `camara_procesada/`

**Ventajas:**
- Automatización total sin necesidad de tener nada corriendo en local
- Historial de cambios en Git
- Se puede usar desde cualquier dispositivo

**Limitaciones:**
- Requiere API key en GitHub Secrets
- Coste de API + minutos de Actions (gratis hasta 2000 min/mes en cuentas gratuitas)
- Dependencia de GitHub
- Tiempo de ejecución: 10-30 segundos por workflow

---

## Tabla comparativa

| Aspecto | Watch | Script autónomo | Notificador | GitHub Actions |
|---|---|---|---|---|
| Automatización completa | ✅ Sí* | ✅ Sí | ❌ No | ✅ Sí |
| Sesión abierta | ✅ | ❌ | ❌ | ❌ |
| API externa | ❌ | ✅ | ❌ | ✅ |
| Coste recurrente | ❌ | ✅ (bajo) | ❌ | ✅ (bajo) |
| Complejidad | Mínima | Media | Mínima | Baja |
| Inteligencia del agente | ✅ Completa | Parcial (prompts) | ✅ Completa | Parcial (prompts) |

*\* Mientras la sesión de opencode esté abierta.*

---

## Recomendación

El orden lógico de implantación sería:

1. **Notificador** → primeras semanas, mínima inversión
2. **`procesa --watch`** → cuando quieras dejar sesiones largas abiertas
3. **Script autónomo** o **GitHub Actions** → cuando quieras automatización sin depender de una terminal

Cada opción es independiente y no requiere migración entre ellas.
