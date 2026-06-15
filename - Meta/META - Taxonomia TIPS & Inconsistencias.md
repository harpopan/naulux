---
version: 1.0
estado: borrador
---

# META — Taxonomía TIPS y auditoría de bóveda

> [!summary] Resumen
> Este documento recoge: (1) el análisis y decisión de añadir `TIPS` como nuevo tipo documental para consejos prácticos, (2) la definición formal del tipo, y (3) la auditoría de incidencias estructurales detectadas en la bóveda.

---

## 1. Necesidad detectada

No existía un tipo documental para **consejos prácticos sueltos o recopilados**: tips de natación, de estudio, de programación, de organización, etc.

Los tipos existentes cubrían mal este formato:

- `GUIA` → paso a paso secuencial (demasiado estructurado)
- `REF` → material de consulta genérico (se mezcla con chuletas técnicas)
- `NOTA` → apunte efímero (el tip suele ser perenne)
- `CONOC` → conocimiento consolidado (demasiado formal)

El hueco: contenido **breve, autónomo, accionable** que puede aparecer en cualquier temática.

---

## 2. Evaluación de opciones

| Tipo | ¿Cubre tips/consejos? | Problema |
|------|-----------------------|----------|
| `REF` | Podría, pero es muy genérico | Se mezcla con listados técnicos, documentación de consulta |
| `GUIA` | Demasiado rígido | Un tip suelto no es un procedimiento paso a paso |
| `NOTA` | Demasiado efímero | Los tips se conservan y reconsultan |
| `CONOC` | Se acerca | Suena muy formal para "no uses git add . sin revisar" |
| **`TIPS`** | **Encaja justo** | Claro, directo, escalable a cualquier tema |

**Decisión**: crear el tipo `TIPS`.

> Nota: la taxonomía V2 usa prefijos en singular (`TIP` sería la forma canónica), pero se adopta `TIPS` por claridad semántica y porque el usuario lo ha establecido así.

---

## 3. Taxonomía oficial de `TIPS`

| Aspecto | Definición |
|---------|-----------|
| **Tipo** | `TIPS` |
| **Uso** | Consejo práctico, recomendación breve, "buena práctica" resumida, recopilación de tips sobre un tema concreto |
| **Formato** | `TIPS - [Tema].md` |
| **No usar para** | Guías paso a paso (`GUIA`), chuletas técnicas (`REF`), notas rápidas efímeras (`NOTA`) |
| **Ubicación** | La carpeta temática que corresponda (igual que cualquier otro tipo) |

### Reglas de contenido

- Cada `TIPS` puede contener **uno o varios consejos** sobre el mismo tema.
- Si el documento tiene un solo consejo, que el tema sea lo bastante descriptivo.
- Si tiene varios, que compartan un hilo común (ej. `TIPS - Natacion Aguas Abiertas.md` y dentro 5 consejos).
- Los tips deben ser **accionables**: "Haz X" / "Evita Y porque Z".
- No usar `TIPS` para documentación de referencia extensa (eso es `REF`).

### Ejemplos de uso correcto

```
TIPS - Natacion Aguas Abiertas.md          → Salud/
TIPS - Estudio Efectivo.md                 → Crecimiento/
TIPS - Git.md                              → Desarrollo/
TIPS - Bash.md                             → Desarrollo/
TIPS - Mantener Hardware.md                → Informatica/
TIPS - Prompting IA.md                     → IA/
```

### Diferencia con tipos fronterizos

| Si el contenido es... | Usar |
|----------------------|------|
| "Consejo: apaga el WiFi al instalar Linux" | `TIPS` |
| "Pasos para instalar Linux Mint desde cero" | `GUIA` |
| "Listado de comandos Linux útiles" | `REF` |
| "Anotación rápida: hoy probé X y no funcionó" | `NOTA` |
| "Guía metodológica completa de cómo estudiar" | `GUIA` |
| "3 trucos para memorizar mejor" | `TIPS` |

---

## 4. Auditoría de inconsistencias actuales

### 4.1 Crítico — documentos sin prefijo (raíz)

- `lahermita.sytes.net - Certificados.md`
- `lahermita.sytes.net - Rasp Customization.md`
- `MAPEO2DWIFI.md`
- `mazm-canciones usables.md`

### 4.2 Alto — documentos mal ubicados (en raíz, deberían estar en su carpeta)

| Documento | Carpeta propuesta |
|-----------|-------------------|
| `GUIA - Ollama Local.md` | `IA/` o `Desarrollo/` |
| `IDEA - RANDOM.md` | `Varios/` o `Proyectos/` |
| `NOTA - Nvidia Build Temp Account.md` | `Informatica/` |
| `NOTA - Uso VRAM.md` | `IA/` o `Informatica/` |
| `PROMPT - Análisis Técnico Diagramas ASCII.md` | `IA/` o `Desarrollo/` |
| `PROMPT - Claude Testing V01.md` | `IA/` o `Varios/` |
| `PROMPT - Comfy Generar Video.md` | `Diseño/` |
| `REF - Guia windows.md` | `Informatica/` |
| `REF - Habilitar Opencode Powershell.md` | `Desarrollo/IDEs/` |
| `REF - Libretas Moleskines.md` | `Varios/` o `Creatividad/` |
| `REF - LLM Locales Continue Dev.md` | `IA/` o `Desarrollo/` |
| `TAREA - CACSA.md` | `Proyectos/` |
| `TAREA - Largo Plazo.md` | `Proyectos/` |
| `TAREA - Variadas.md` | `Proyectos/` |

### 4.3 Medio — nombre o prefijo dudoso

- `PROMPT - Claude Testing V01.md` — lleva `V01` en el nombre. La versión va en frontmatter, no en el archivo.
- `REF - Guia windows.md` — el nombre dice "Guia" pero el prefijo es `REF`. ¿Es referencia o guía? Decidir uno.
- `REF - Easy Diffusion Impressionism Models.md` (en `Diseño/`) — parece más `LAB` (exploración) que `REF`.

### 4.4 Estructura — todo correcto ✅

- `- Meta/` contiene solo `META*` y `TPL*` ✅
- Todos los `PROY-*` están dentro de `Proyectos/` ✅
- Las carpetas temáticas existen y están bien nombradas ✅

---

## 5. Priorización sugerida para resolver

1. **Crítico**: poner prefijo a los 4 documentos sin él
2. **Alto**: mover los 14 documentos de la raíz a sus carpetas
3. **Medio**: ajustar nombres dudosos (V01, REF vs GUIA, REF vs LAB)
4. **Bajo**: revisar frontmatter y summary de documentos movidos

---

*Este documento es parte del sistema de la bóveda. Pertenece a `- Meta/`.*
