---
version: 2.5
estado: activo
---
# Sistema de Organizacion de Vivero (Markdown) - V2

> [!summary] Resumen
> Esta V2 reduce la taxonomia a un conjunto pequeno y estable de tipos documentales.
> La regla principal es que el prefijo solo debe expresar que es el documento, nunca la herramienta, el tema, el estado ni la fuente.
> Esta revision anade el tipo `TIP` para consejos practicos, la justificacion del registro actual y un mapeado alternativo completo en castellano para comparar criterios.
> La V2.5 anade los tipos temporales `PEND` y `SAM` para el flujo de trabajo de documentos pendientes de revision y exports de la extension Samjoko.
> El anexo final incluye una tabla completa de renombrado sugerido para los Markdown actuales de la boveda.

## Objetivo

Construir un sistema de nombres que permita:

- localizar documentos rapido
- filtrar por tipo sin ambiguedad
- crecer sin crear prefijos nuevos por cada herramienta o contexto
- separar tipo documental, tema y estado del documento

## Regla maestra

El prefijo representa solo el tipo documental.
No debe representar:
- herramienta o plataforma
- universo tematico
- idioma
- version del archivo
- estado del trabajo
- formato de captura puntual si ya existe un tipo mejor

Ejemplos correctos:

- `GUIA - OpenCode Setup.md`
- `LAB - Easy Diffusion Impressionism Models.md`
- `LOG - Ecosistema MicroApps (Copilot).md`
- `PROMPT - Fotor.md`
- `IDEA - Akkoro.md`
- `TIP - Natacion Aguas Abiertas.md`

### Excepcion temporal: `PEND` y `SAM`

`PEND` y `SAM` son prefijos de proceso, no tipos documentales permanentes. Indican que un documento esta pendiente de revision y clasificacion. **Deben desaparecer** una vez el documento sea revisado, renombrado con su tipo real y movido a su carpeta.

- `PEND` → documentos anadidos manualmente a la boveda, sin clasificar
- `SAM` → documentos exportados desde la extension Samjoko

Ambos prefijos conviven temporalmente en la raiz hasta que se procesen.

## Formato base

`[TIPO] - [Tema principal] (calificador opcional)`

Reglas operativas:
- un solo prefijo por archivo
- prefijos en singular
- sin numeros de version en el nombre salvo que formen parte inseparable del objeto estudiado
- el tema debe poder entenderse sin abrir el archivo
- el estado va en frontmatter, no en el nombre

## Taxonomia oficial V2

| Tipo | Uso recomendado | No usar para |
| --- | --- | --- |
| `META` | ✅ Documentos del propio sistema de la boveda, normas, analisis estructural, plantillas marco | 🚫 Documentos tematicos normales |
| `CHK` | ✅ Checklist cerrada o verificable | 🚫 Backlogs abiertos o listas mezcladas |
| `CITA` | ✅ Cita o colección de citas motivadoras, inspiradoras o relevantes de cualquier ámbito | 🚫 Consejos prácticos (`TIP`), fragmentos sueltos (`FRAG`) o artículos redactados (`ART`) |
| `TAREA` | ✅ Lista de tareas abiertas, backlog, pendientes | 🚫 Checklist de validacion cerrada |
| `TIP` | ✅ Consejo practico, recomendacion breve, buena practica resumida | 🚫 Guias paso a paso (`GUIA`), chuletas tecnicas (`REF`), apuntes efimeros (`NOTA`) |
| `GUIA` | ✅ Paso a paso, proceso, modo de uso, onboarding | 🚫 Referencias sueltas sin procedimiento |
| `DOC` | ✅ Documento general explicativo cuando no aplica un tipo mas preciso | 🚫 Cualquier cosa que ya encaje en `REF`, `GUIA`, `LOG`, `LEGAL` o `SPEC` |
| `REF` | ✅ Material de consulta, recopilaciones, chuletas, listados utiles | 🚫 Procedimientos detallados |
| `PROMPT` | ✅ Prompt individual o coleccion de prompts | 🚫 Documentos sobre prompting que son una guia metodologica |
| `ART` | ✅ Articulo redactado o pieza de reflexion | 🚫 Nota rapida o recopilacion |
| `NOTA` | ✅ Captura breve, apunte rapido, nota efimera | 🚫 Bancos de ideas o referencias consolidadas |
| `IDEA` | ✅ Idea individual o banco corto de ideas relacionadas | 🚫 Tareas, checklist o documento consolidado |
| `LAB` | ✅ Exploracion, pruebas, iteracion, experimentos, trabajo en curso | 🚫 Documentacion estable o de consulta final |
| `PROY` | ✅ Documento hub o documento troncal de un proyecto | 🚫 Nota operativa aislada |
| `MAP` | ✅ Indice, mapa de conocimiento, tabla de enlaces | 🚫 Documento tematico normal |
| `SPEC` | ✅ Especificacion tecnica, funcional o contractual | 🚫 Apunte o brainstorming |
| `CONOC` | ✅ Conocimiento consolidado y sintetizado | 🚫 Borradores o recopilaciones sin refinar |
| `LOG` | ✅ Bitacora, transcripcion, historial de trabajo, chat registrado | 🚫 Guia o conocimiento consolidado |
| `LEGAL` | ✅ Licencias, avisos legales, condiciones de uso | 🚫 Documentacion tecnica general |
| `PLANT` | ✅ Plantilla reutilizable | 🚫 Documento de trabajo real |
| `FRAG` | ✅ Fragmento breve reutilizable | 🚫 Documentos largos o con contexto amplio |
| `PEND` | ✅ Prefijo temporal para documentos pendientes de revision, clasificacion y ubicacion definitiva | 🚫 Documentos ya revisados o en su carpeta correcta |
| `SAM` | ✅ Prefijo temporal para documentos exportados desde la extension Samjoko, pendientes de clasificar | 🚫 Documentos ya procesados y movidos a su carpeta |

## Justificacion de la taxonomia actual

La V2 oficial usa prefijos en singular y codigos cortos porque esta tratando el prefijo como una clase documental, no como una descripcion literal del contenido.

Esto implica:
- el prefijo responde a que es el archivo, no a cuantos elementos contiene
- el singular clasifica mejor que el plural: un archivo es una `GUIA`, una `IDEA`, un `LAB` o una `TAREA`
- los codigos breves facilitan escaneo visual, orden alfabetico, filtros y renombrados masivos
- la consistencia del sistema pesa mas que traducir cada etiqueta de forma literal

Si la boveda va a usarse solo en castellano, una taxonomia castellanizada completa es viable, pero conviene adoptarla como sistema entero y no solo como excepcion puntual. Para visualizarlo, se incluye una propuesta en el anexo C.

### Sobre `TIP`

`TIP` se anade para cubrir contenido que no encajaba bien en los tipos existentes: consejos practicos, recomendaciones breves y recopilaciones de buenas practices sobre un tema concreto.

| Si el contenido es... | Usar |
|----------------------|------|
| "Consejo: apaga el WiFi al instalar Linux" | `TIP` |
| "Pasos para instalar Linux Mint desde cero" | `GUIA` |
| "Listado de comandos Linux utiles" | `REF` |
| "3 trucos para memorizar mejor" | `TIP` |
| "Guia metodologica completa de como estudiar" | `GUIA` |

Los tips deben ser accionables: "Haz X" / "Evita Y porque Z". Si el tip es un paso de un proceso mayor, probablemente pertenece a una `GUIA`.

## Flujo de trabajo con pendientes (V2.5)

### Ciclo de vida de un documento pendiente

1. **Captura** → el documento entra en la boveda con prefijo `PEND` o `SAM` y se ubica en la raiz
2. **Revision** → se abre el documento, se evalua su contenido y se le asigna su tipo documental real
3. **Clasificacion** → se renombra con el tipo correcto, se completa el frontmatter y se mueve a su carpeta tematica

### Reglas para `PEND` y `SAM`

- Ambos conviven en la raiz hasta que se procesen
- `PEND` es para documentos anadidos manualmente
- `SAM` es para exports automaticos de la extension Samjoko
- Ambos desaparecen al completar el ciclo de revision
- Si un documento `SAM` ya esta claro, puede ir directamente a su carpeta con su tipo real sin pasar por `PEND`

### Ejemplo

```
PEND - Articulo Natacion.md          → (raiz, pendiente)
SAM - Tutorial Linux.md              → (raiz, pendiente)
...revision...
GUIA - Natacion Aguas Abiertas.md    → Salud/
DOC - Tutorial Linux Básico.md       → Desarrollo/
```

## Convenciones obligatorias

### Herramienta, fuente o universo van en el tema

Casos correctos:

- `GUIA - OpenCode Setup.md`
- `LAB - Easy Diffusion LHNovel Impressionism 1.7.md`
- `REF - Modelos LLM.md`
- `DOC - Lore DnD Seio.md`

### Versionado y estado en frontmatter

Usar siempre el bloque:

```yaml
---
version: 1.0
estado: borrador
---
```

Estados recomendados:
- `borrador`
- `activo`
- `congelado`
- `archivado`

## Bloque estandar de resumen

```markdown
> [!summary] Resumen
> Descripcion clara del proposito del documento, cuando usarlo y que problema resuelve.
>
> Si el documento es operativo o experimental, indicar tambien el contexto y el limite de uso.
```

