# Arquitectura del proyecto

Reglas compartidas de agentes y gobernanza del ecosistema Flutter.

```mermaid
graph TD
    AGENTS[AGENTS.md Router] --> Core[core/ path_map | communication | brain]
    AGENTS --> Templates[templates/]
    AGENTS --> Adapters[adapters/]
    AGENTS --> Skills[skills/]
    AGENTS --> Knowledge[knowledge/]
```

| Capa | Implementación real |
|---|---|
| Router | `AGENTS.md` |
| Core | `core/path_map.md`, `core/communication.md`, `core/brain.md` |
| Plantillas | `templates/` |
| Adaptadores | `adapters/` |
