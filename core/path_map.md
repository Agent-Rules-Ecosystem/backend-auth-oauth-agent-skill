# Mapa canónico de rutas

## Reglas globales: submódulo `.agents/`

| Recurso | Ruta | Carga |
|---|---|---|
| Router | `.agents/AGENTS.md` | Obligatoria |
| Adaptadores | `.agents/adapters/` | Al instalar |
| Comunicación | `.agents/core/communication.md` | Obligatoria |
| Brain | `.agents/core/brain.md` | Obligatoria |
| Conocimiento | `.agents/knowledge/` | Bajo demanda |
| Plantillas | `.agents/templates/` | Al iniciar |
| Skills | `.agents/skills/` | Bajo demanda |

## Estado local: raíz del proyecto

| Recurso | Ruta | Carga |
|---|---|---|
| Sesión | `overview/session.md` | Inicio/cierre |
| Trabajo | `overview/work.md` | Inicio/cierre |
| Aprendizajes | `overview/learning.md` | Al cerrar |
| Arquitectura real | `overview/architecture.md` | Al iniciar |
| Arquitectura | `overview/trackers/architecture.md` | Bajo demanda |
| Progreso | `overview/trackers/progress.md` | Inicio/cierre |
| Contenido | `overview/trackers/content_*.md` | Si aplica |
| Historial | `overview/history/` | Al resumir |

## Alias heredados

| Alias | Ruta actual |
|---|---|
| `overview/tracker.md` | `overview/trackers/architecture.md` |
| `overview/tasks.md` | `overview/work.md` |
| `memory_session.md` | `overview/session.md` |
