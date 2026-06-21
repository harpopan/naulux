---
version: 1.0
estado: activo
idioma: castellano
---

# Guía de Configuración de Modelos para Continue.dev (RTX 2060 8GB)

> [!summary] Resumen
> Configuración optimizada de modelos para usar Continue.dev en VS Code con una GPU RTX 2060 de 8GB. Propone una arquitectura con un modelo principal de razonamiento, uno ligero para autocompletado y uno de embeddings, maximizando calidad sin saturar VRAM.

## Objetivo

Este documento propone una configuración optimizada de modelos para usar Continue.dev en VS Code con una GPU RTX 2060 de 8GB.

La estrategia se basa en:
- Maximizar calidad de razonamiento sin saturar VRAM
- Separar tareas por especialización (chat, autocomplete, embeddings, etc.)
- Reutilizar modelos cuando sea posible para estabilidad

## Arquitectura recomendada

En una GPU de 8GB, la clave es evitar demasiados modelos grandes simultáneos. En su lugar:

- 1 modelo principal (razonamiento)
- 1 modelo ligero (autocomplete)
- 1 modelo de embeddings eficiente
- rerank opcional

## CHAT / PLAN / AGENT

### Rol
Es el "cerebro principal" del sistema.

### Modelos recomendados
- Qwen2.5-Coder 7B Instruct (cuantizado 4-bit)
- Llama 3.1 8B Instruct (cuantizado 4-bit)

### Recomendación
- Si trabajas principalmente con código → Qwen Coder
- Si haces razonamiento general → Llama 3.1

### Usos
- Chat
- Planificación de tareas
- Edición conceptual
- Agente autónomo

## AUTOCOMPLETE

### Rol
Modelo ultrarrápido para sugerencias en tiempo real mientras escribes.

### Modelos recomendados
- DeepSeek Coder 1.3B Instruct
- Qwen2.5-Coder 3B Instruct

### Características
- Baja latencia
- Bajo consumo de VRAM
- Respuestas cortas y sintácticas

## EDIT / APPLY

### Rol
Transformación precisa de código y aplicación de cambios.

### Recomendación clave
Usar el MISMO modelo que en CHAT.

### Por qué
- Mantiene coherencia entre razonamiento y ejecución
- Evita inconsistencias en diffs
- Mejora estabilidad en refactors

## EMBEDDINGS

### Rol
Indexación del código y documentación para @codebase y @docs.

### Modelos recomendados
- bge-small-en-v1.5
- nomic-embed-text

### Características
- Muy ligeros
- Pueden ejecutarse en CPU
- No consumen VRAM relevante

## RERANK

### Rol
Reordenación de resultados de búsqueda semántica.

### Modelo recomendado
- bge-reranker-base

### Nota
- Opcional
- Puede desactivarse si se busca simplicidad

## Configuración ideal resumida

| Rol | Modelo |
|-----|--------|
| CHAT / PLAN / AGENT | Qwen 7B o Llama 3.1 8B |
| EDIT | Igual que CHAT |
| APPLY | Igual que CHAT |
| AUTOCOMPLETE | DeepSeek 1.3B o Qwen 3B |
| EMBED | bge-small o nomic-embed |
| RERANK | bge-reranker-base (opcional) |

## Filosofía de uso

Con una RTX 2060 8GB no buscas abundancia de modelos, sino armonía.

Piensa en el sistema como una tripulación:
- Un cerebro principal (CHAT)
- Un reflejo rápido (AUTOCOMPLETE)
- Un archivista (EMBED)
- Un crítico opcional (RERANK)

## Siguiente paso sugerido

Si quieres mejorar aún más esta configuración, los siguientes pasos naturales serían:

- Crear perfiles separados por tarea (coding vs documentación)
- Optimizar cuantización según VRAM real disponible
- Añadir routing entre modelos (ligero vs potente)
- Integrar LM Studio + Ollama híbrido

Este documento está pensado como base exportable para tu setup en Continue.dev + VS Code.
