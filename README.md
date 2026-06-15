# Naulux

**Naulux** es el agente principal del sistema de procesamiento documental del *Vivero*. Gestiona el flujo de documentos en bruto desde `0_DatosBrutos/` hasta `1_DatosProcesados/`, aplicando clasificación, traducción, renombrado y estructuración.

## Uso

Naulux se invoca mediante comandos desde el chat del agente:

| Comando | Acción |
|---|---|---|
| `ayuda` | Muestra esta tabla de comandos disponibles |
| `procesa` | Procesa **todos** los documentos pendientes en `0_DatosBrutos/` |
| `procesa <archivo>` | Procesa un archivo específico (ej: `procesa claudeprompts-valorar.md`) |
| `procesa ayuda` | Alias de `ayuda` |

## Flujo de procesamiento

1. **Leer** el documento desde `0_DatosBrutos/`
2. **Detectar idioma** — inglés se traduce a español castellano; castellano se conserva
3. **Renombrar** con la taxonomía oficial: `[TIPO] - [Tema principal] (calificador).md`
4. **Ubicar** en la carpeta temática correspondiente dentro de `1_DatosProcesados/`
5. **Agregar frontmatter** YAML (versión, estado, etc.)
6. **Agregar resumen** en bloque `> [!summary]`
7. **Escribir** el archivo final en `1_DatosProcesados/`
8. **Mover** el original a `0_DatosBrutos/_procesados/`

## Taxonomía

Naulux usa 20 prefijos (tipos documentales): `META`, `CHK`, `CITA`, `TAREA`, `TIP`, `GUIA`, `DOC`, `REF`, `PROMPT`, `ART`, `NOTA`, `IDEA`, `LAB`, `PROY`, `MAP`, `SPEC`, `CONOC`, `LOG`, `LEGAL`, `PLANT`, `FRAG`. La fuente única de verdad es `META - Guideline oficial.md`.

## Estructura del proyecto

```
naulux/
├── AGENTS.md              ← Instrucciones del agente
├── META - Guideline oficial.md   ← Taxonomía y reglas
├── META - Estructura de Carpetas.md  ← Reglas de ubicación
├── 0_DatosBrutos/      ← Documentos pendientes de procesar
│   └── _procesados/       ← Originales ya procesados
├── 1_DatosProcesados/      ← Documentos ya clasificados y estructurados
│   ├── CiberSeguridad/
│   ├── Crecimiento/
│   ├── IA/
│   └── ...
└── README.md
```
