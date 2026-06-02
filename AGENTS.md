# Nautilus — Procesador de Documentos

## Propósito
Procesar documentos en bruto de `documentos_bruto/`, analizarlos, traducirlos si procede, estructurarlos y moverlos a `camara_procesada/`.

## Activación (solo bajo demanda)

| Comando | Acción |
|---|---|---|
| `ayuda` | Muestra esta tabla de comandos disponibles |
| `procesa` | Procesa **todos** los documentos pendientes en `documentos_bruto/` |
| `procesa <archivo>` | Procesa un archivo específico (ej: `procesa claudeprompts-valorar.md`) |
| `procesa ayuda` | Alias de `ayuda` |

## Flujo por cada documento

1. **Leer** el archivo desde `documentos_bruto/`
2. **Detectar idioma**:
   - Inglés → traducir a español castellano
   - Castellano → mantener intacto
3. **Renombrar** con la taxonomía oficial (ver más abajo):
   - Elegir el prefijo según el tipo documental
   - Formato: `[TIPO] - [Tema principal] (calificador opcional).md`
   - El calificador solo se usa para desambiguar si dos documentos compartieran prefijo y tema
   - Sin números de versión en el nombre (van en frontmatter)
4. **Determinar carpeta destino** según las reglas de `META - Estructura de Carpetas.md`:
   - Elegir carpeta temática, por tipo o `Varios/` según corresponda
   - Crear la carpeta dentro de `camara_procesada/` si no existe
   - Si hay duda, preguntar al usuario
5. **Agregar frontmatter YAML** con fecha, versión, idioma y estado si el documento lo merece
6. **Agregar título interno** debajo del frontmatter con `# Título completo del documento`
7. **Agregar bloque `> [!summary]`** con un resumen del documento si lo merece
8. **Escribir** el archivo final en `camara_procesada/` (en la carpeta determinada)
9. **Mover el original** a `documentos_bruto/_procesados/`

## Reglas de título y nombre de archivo

- El **título interno** (`# Título completo`) refleja el contenido real del documento con total fidelidad
- El **nombre del archivo** se sintetiza a partir de ese título, eliminando artículos determinantes (`el`, `la`, `los`, `las`) y similares que no aporten valor semántico al nombre

## Taxonomía de nombrado

Al iniciar cualquier operación `procesa`, leer el archivo **`META - Guideline oficial.md`** que contiene:
- Regla maestra de nombrado
- Taxonomía oficial V2 (tabla completa con 20 prefijos)
- Formato base y reglas operativas
- Formato de frontmatter y estados recomendados
- Bloque estándar de resumen

Ese archivo es la fuente única de verdad. Si se actualiza, el agente trabajará con la versión vigente automáticamente.

## Reglas de ubicación

Al iniciar cualquier operación `procesa`, leer el archivo **`META - Estructura de Carpetas.md`** que define:
- Jerarquía de carpetas
- Reglas de asignación temática vs. por tipo documental
- Subcarpetas específicas

Si hay duda sobre dónde colocar un documento, preguntar al usuario.

## Pendientes por definir
- [ ] Validar si `Articulos/` se mantiene como carpeta separada o se integra en carpetas temáticas

## Notas
- No alterar el significado ni el tono del documento original
- Traducción natural al español castellano, no literal
- La herramienta, fuente o universo van en el tema, no en el prefijo
