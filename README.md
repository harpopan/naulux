# Naulux

**Naulux** es el agente principal del sistema de procesamiento documental del *Vivero*. Gestiona el flujo de documentos en bruto desde `documentos_bruto/` hasta `camara_procesada/`, aplicando clasificación, traducción, renombrado y estructuración.

## Uso

Naulux se invoca mediante comandos desde el chat del agente:

| Comando | Acción |
|---|---|---|
| `ayuda` | Muestra esta tabla de comandos disponibles |
| `procesa` | Procesa **todos** los documentos pendientes en `documentos_bruto/` |
| `procesa <archivo>` | Procesa un archivo específico (ej: `procesa claudeprompts-valorar.md`) |
| `procesa ayuda` | Alias de `ayuda` |

## Flujo de procesamiento

1. **Leer** el documento desde `documentos_bruto/`
2. **Detectar idioma** — inglés se traduce a español castellano; castellano se conserva
3. **Renombrar** con la taxonomía oficial: `[TIPO] - [Tema principal] (calificador).md`
4. **Ubicar** en la carpeta temática correspondiente dentro de `camara_procesada/`
5. **Agregar frontmatter** YAML (versión, estado, etc.)
6. **Agregar resumen** en bloque `> [!summary]`
7. **Escribir** el archivo final en `camara_procesada/`
8. **Mover** el original a `documentos_bruto/_procesados/`

## Taxonomía

Naulux usa 20 prefijos (tipos documentales): `META`, `CHK`, `CITA`, `TAREA`, `TIP`, `GUIA`, `DOC`, `REF`, `PROMPT`, `ART`, `NOTA`, `IDEA`, `LAB`, `PROY`, `MAP`, `SPEC`, `CONOC`, `LOG`, `LEGAL`, `PLANT`, `FRAG`. La fuente única de verdad es `META - Guideline oficial.md`.

## Estructura del proyecto

```
naulux/
├── AGENTS.md              ← Instrucciones del agente
├── META - Guideline oficial.md   ← Taxonomía y reglas
├── META - Estructura de Carpetas.md  ← Reglas de ubicación
├── documentos_bruto/      ← Documentos pendientes de procesar
│   └── _procesados/       ← Originales ya procesados
├── camara_procesada/      ← Documentos ya clasificados y estructurados
│   ├── CiberSeguridad/
│   ├── Crecimiento/
│   ├── IA/
│   └── ...
└── README.md
```
