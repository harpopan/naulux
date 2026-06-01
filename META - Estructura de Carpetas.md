---
version: 1.0
estado: borrador
---

# META — Estructura de Carpetas

> [!summary] Resumen
> Define la jerarquía de carpetas de la bóveda y las reglas para asignar cada documento a su ubicación correcta según tipo documental y temática. Sirve tanto para organización manual como para el agente `procesa`.

---

## Regla general

Un documento se ubica en la **carpeta temática** que corresponda a su tema principal.
Si no encaja en ninguna carpeta temática, se usa la **carpeta por tipo documental**.
Si no encaja en ninguna, va a `Varios/`.

## Carpetas temáticas

| Carpeta | Temática | Tipos habituales | Ejemplos |
|---|---|---|---|
| `- Meta/` | Sistema de la bóveda | `META`, `TPL` | Guías del sistema, plantillas |
| `CiberSeguridad/` | Seguridad informática | `DOC`, `CHK` | Raspberry Pi hacking, OWASP |
| `CiberSeguridad/IA/` | Seguridad en IA | `DOC` | OWASP Top 10 para LLM |
| `Creatividad/` | Creatividad analógica | `REF` | Libretas Moleskines |
| `Crecimiento/` | Desarrollo personal y aprendizaje | `DOC`, `PROMPT` | Método loci, tutorizar |
| `Desarrollo/` | Desarrollo de software general | `DOC`, `REF`, `PROMPT` | RenPy, Promesas JS, herramientas |
| `Desarrollo/IDEs/` | Entornos de desarrollo | `GUIA`, `REF` | OpenCode, VSCode, ContinueDev |
| `Desarrollo/Web/` | Desarrollo web | `GUIA`, `PROMPT` | Buenas prácticas web, formularios |
| `Desarrollo/Wordpress/` | WordPress | `CHK` | Alcance proyecto WP |
| `Diseño/` | Diseño gráfico y generación de imagen | `PROMPT`, `REF` | Fotor, Easy Diffusion, MageSpace |
| `IA/` | Inteligencia Artificial general | `DOC`, `REF`, `CHK`, `GUIA` | Modelos LLM, uso responsable |
| `Informatica/` | Informática general / IT | `CHK`, `REF` | Instalación equipo, Linux Mint |
| `Proyectos/` | Hubs de proyecto | `PROY`, `LOG`, `MAP`, `SPEC` | Nautilus, Akkorogotchi, Vivero |
| `Proyectos/Licencias/` | Licencias de proyectos | `LEGAL`, `REF` | Licencias de distribución |
| `Salud/` | Salud y bienestar | `ART`, `TIP` | Natación, consejos |
| `Varios/` | Miscelánea sin otra ubicación | `NOTA`, `PROMPT` | Lore DnD, nombres vikingos |

## Carpeta por tipo documental

Cuando un documento **no pertenezca claramente a ninguna temática** de las anteriores, se usa la carpeta que corresponde a su tipo:

| Tipo | Carpeta |
|---|---|
| `ART` | `Articulos/` |
| `NOTA` | `Varios/` |
| `IDEA` | `Varios/` |
| `FRAG` | `Varios/` |
| Otros | `Varios/` |

## Reglas operativas

1. **Prioridad temática**: primero buscar carpeta temática. Si el tema del documento encaja en una carpeta de la tabla temática, va ahí aunque sea de un tipo que tenga carpeta propia (ej: un `ART` sobre natación va a `Salud/`, no a `Articulos/`).
2. **`- Meta/` es exclusiva** para `META` y `TPL`. Nunca mezclar documentos temáticos ahí.
3. **`Proyectos/`** contiene solo documentos vinculados a un proyecto concreto (`PROY`, `LOG` de proyecto, `MAP` de proyectos, `SPEC` de proyecto). No usar para documentación técnica general.
4. **Subcarpetas específicas** (ej: `Desarrollo/IDEs/`) tienen prioridad sobre su carpeta padre. Si un documento trata sobre IDEs, va a `Desarrollo/IDEs/`, no a `Desarrollo/`.
5. **Si hay duda**, preguntar al usuario antes de mover.

## Pendientes
- Validar si `Articulos/` debe seguir existiendo como carpeta separada o integrarse en las carpetas temáticas (actualmente hay 2 `ART` sin temática clara ahí)
