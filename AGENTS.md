---
name: agent-rules-governance
description: Bootstrap and governance for shared Flutter agent rules.
---

# Flutter Agent Rules

## Bootstrap obligatorio

Antes de responder o editar, leer y cumplir:

1. `.agents/core/path_map.md`
2. `.agents/core/communication.md`
3. `.agents/core/brain.md`

**Triggers de arranque** — las siguientes frases o condiciones disparan el protocolo completo (discovery + `overview/` + mapeo de archivos):

- **"ejecuta .agents"** (o "corre .agents", "bootstrap .agents") → dispara además el Protocolo de Auditoría de Learning definido en `brain.md`.
- "nuevo proyecto" / "inicializar" / "bootstrap" / "empieza" en el primer mensaje.
- Ausencia de `overview/session.md` al comenzar cualquier tarea de código.
- Primer mensaje de conversación cuando el proyecto tiene `.agents/` pero no `overview/`.

Para cualquier tarea que inspeccione o cambie código del proyecto, antes de analizar o responder cargar `overview/session.md`, `overview/work.md` y `overview/trackers/progress.md`. Si falta `overview/` o uno de esos archivos, crearlo desde `.agents/templates/`. Si falta `overview/architecture.md`, crearlo desde su plantilla.

Las reglas globales viven solo en `.agents/`. Si agente no descubre `.agents/AGENTS.md`, instalar adaptador mínimo desde `.agents/adapters/`; nunca duplicar reglas. Al editar este repositorio oficial directamente, usar rutas locales equivalentes (`core/`, `templates/`, etc.).

## Estado local versionado

Crear `overview/` desde `.agents/templates/` al iniciar proyecto. Al inicio y cierre, cargar/actualizar:

- `overview/session.md`
- `overview/work.md`
- `overview/trackers/progress.md`
- `overview/context/` para archivos de dominio no mapeables
- `overview/learning.md` cuando surja mejora candidata

`overview/history/` conserva sesiones antiguas. Cambios a reglas globales solo ocurren en repositorio oficial con aprobación del propietario.
