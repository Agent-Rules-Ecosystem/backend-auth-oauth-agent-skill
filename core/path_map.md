# DIRECTORIO DE RUTAS DEL SISTEMA (PATH MAP)

> [!CRITICAL]
> **FUENTE ÚNICA DE LA VERDAD DE RUTAS.** Todos los agentes deben consultar este archivo para resolver rutas sin adivinar.

---

## 1. Reglas Globales y Estáticas (Submódulo `.agents/`)
*Ubicación:* Repositorio central `flutter-agent-rules` incluido como submódulo en la raíz de cada proyecto.

| Dominio | Archivo | Propósito | Carga |
|---|---|---|---|
| **Router** | `.agents/AGENTS.md` | Punto de entrada universal y gobernanza | Obligatoria |
| **Directorio** | `.agents/core/path_map.md` | Mapa canónico de rutas del sistema | Obligatoria |
| **Core Brain** | `.agents/core/brain.md` | Protocolo de 2 fases y lógica de decisión | Obligatoria |
| **Comunicación** | `.agents/core/communication.md` | Modo Cavernícola y ahorro de tokens | Obligatoria |
| **Arquitectura** | `.agents/knowledge/architecture.md` | Plantilla de capas y flujo Mermaid | Bajo demanda |
| **Estilo** | `.agents/knowledge/code_style.md` | Convenciones Flutter/Dart y auto-learn | Bajo demanda |
| **Release** | `.agents/knowledge/release_checklist.md` | Triggers y checklist previo a build | Bajo demanda |
| **Rutas (Plantilla)**| `.agents/knowledge/routes_tracker.md` | Plantilla de mapa de rutas Mermaid | Bajo demanda |
| **Skills** | `.agents/skills/` | Habilidades especializadas | Bajo demanda |
| **Vector Store** | `.agents/vector_store/` | Configuración y manifiesto de embeddings | Bajo demanda |

---

## 2. Memoria y Estado Local del Proyecto (`overview/`)
*Ubicación:* Carpeta **propia y visible** en la raíz de cada proyecto Flutter (no en el submódulo).

| Tipo | Archivo | Propósito | Carga |
|---|---|---|---|
| **Episódica** | `overview/session.md` | Resumen de la sesión activa y cambios | Obligatoria |
| **Tareas** | `overview/tasks.md` | Backlog y tarea en progreso actual | Obligatoria |
| **Tracker** | `overview/tracker.md` | Diagrama Mermaid de rutas y estados `:::done`/`:::pending` | Obligatoria |
| **Arquitectura Local**| `overview/architecture.md` | Diagrama real del proyecto activo (si aplica) | Bajo demanda |

---

## 3. Matriz de Mapeo de Nombres Históricos / Equivalencias

| Nombre Histórico / Alias | Ruta Canónica Actual | Ámbito |
|---|---|---|
| `routes_tracker.md` / `home_route_tracker.md` | `overview/tracker.md` | Proyecto local |
| `memory_session.md` / `resumen_sesion.md` | `overview/session.md` | Proyecto local |
| `memory_tasks.md` / `resumen_pendientes.md` | `overview/tasks.md` | Proyecto local |
| `antigravityia.md` | `.agents/core/communication.md` | Submódulo `.agents/` |
| `brain.md` | `.agents/core/brain.md` | Submódulo `.agents/` |
