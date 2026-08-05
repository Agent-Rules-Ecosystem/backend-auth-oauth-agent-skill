# Mapa canónico de rutas

## Reglas globales: submódulo `.agents/`

| Recurso | Ruta | Carga |
|---|---|---|
| Comunicación | `.agents/core/communication.md` | Obligatoria — **leer primero** |
| Router | `.agents/AGENTS.md` | Obligatoria |
| Brain | `.agents/core/brain.md` | Obligatoria |
| Comandos | `.agents/core/commands.md` | Obligatoria |
| Adaptadores (Codex / Cursor / etc) | `.agents/adapters/` (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `cursor-rule.mdc`, `README.md`) | Al instalar |
| Estructura Flutter | `.agents/knowledge/flutter_structure.md` | Discovery |
| Estilo Dart / Clean Arch | `.agents/knowledge/code_style.md` | Bajo demanda |
| Arquitectura Base | `.agents/knowledge/architecture.md` | Bajo demanda |
| Release Checklist | `.agents/knowledge/release_checklist.md` | `$close` / Build |
| Plantillas `overview/` | `.agents/templates/` | `$boot` / Inicio |
| Skill Clean Arch & Limits | `.agents/skills/flutter-clean-arch/SKILL.md` | Refactors / UI |
| Skill Diagrams Mermaid | `.agents/skills/mermaid-diagrams/SKILL.md` | Diagramación |

## Estado local: raíz del proyecto

| Recurso | Ruta | Carga |
|---|---|---|
| Sesión | `overview/session.md` | Inicio/cierre |
| Trabajo (Índice Maestro) | `overview/work.md` | Inicio/cierre |
| Tarea Activa | `overview/work/tasks.md` | Inicio/en ejecución |
| Pendientes | `overview/work/pendientes.md` | Cierre/bajo demanda |
| Deuda Técnica | `overview/work/deuda_tecnica.md` | Inicio/bajo demanda |
| Protocolo Revisión Work | `overview/work_review.md` | Fin de `$boot` |
| Aprendizajes | `overview/learning.md` | Al cerrar |
| Arquitectura real | `overview/architecture.md` | Al iniciar |
| Tracker Arquitectura | `overview/trackers/architecture.md` | Bajo demanda |
| Tracker Progreso | `overview/trackers/progress.md` | Inicio/cierre |
| Contenido | `overview/trackers/content_*.md` | Si aplica |
| Modularización Contenido | `overview/trackers/content/<cat>/<item>.md` | Bajo demanda |
| Historial | `overview/history/` | Al resumir |
| Contexto de dominio | `overview/context/` | Inicio/bajo demanda |
| Flujos de dominio | `overview/workflows/` | Bajo demanda |

> `overview/context/` es para archivos de dominio no mapeables al framework ni al estado de sesión: contexto general, changelogs de contenido, datos de referencia de la app. Se leen al reanudar como checkpoints.

> `overview/workflows/` es para guías de dominio por flujo en términos agnósticos (ej. `Origen → Procesamiento → Destino`). Separado de `architecture.md` (mapa técnico) y de `context/` (datos/referencia).

### Backlog canónico único

- `overview/work.md` = **único** índice y tabla maestra de IDs (`tarea` / `bug` / `deuda`).
- Detalle de ejecución: `overview/work/tasks.md` (tarea activa), `overview/work/pendientes.md` (seguimiento al cerrar) y `overview/work/deuda_tecnica.md` (deuda ordenada por prioridad Alta, Media y Baja).
- No escribir backlogs paralelos o aislados fuera del esquema canónico.

## Alias heredados

| Alias | Ruta actual |
|---|---|
| `overview/tracker.md` | `overview/trackers/architecture.md` |
| `overview/tasks.md` (raíz) | `overview/work.md` / `overview/work/tasks.md` |
| `memory_session.md` | `overview/session.md` |

> Si coexisten alias y canónico con contenido distinto → flag `[consolidar alias]` obligatorio (`brain.md`). Nunca asumir cuál manda sin verificar.
