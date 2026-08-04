# Flutter Agent Rules

Repositorio centralizado: cerebro operativo para proyectos Flutter. Reduce ruido/tokens, conserva continuidad y exige calidad verificable. Se instala como submódulo `.agents/`; reglas globales son independientes del proyecto.

## Qué aporta

1. Comunicación concisa para ahorrar tokens sin bajar calidad.
2. Trackers separados de arquitectura, trabajo, progreso y contenido.
3. Memoria versionada del proyecto: sesión, historial y aprendizajes candidatos.
4. Validación explícita: `verificado`, `no verificado` o `conflicto`.
5. Adaptadores mínimos para Codex, Claude, Gemini/Antigravity y Cursor; nunca se duplican reglas.

## Instalación

```bash
git submodule add https://github.com/tu-usuario/flutter-agent-rules.git .agents
```

Instalar adaptador de `.agents/adapters/` que reconozca agente. Crear `overview/` desde `.agents/templates/`. Ambos forman parte del repositorio Flutter; `.agents/` conserva reglas y `overview/` conserva estado del proyecto.

## Contenido contrastado

Cada agente registra datos en su tracker. Un dato es `verificado` cuando al menos dos coinciden, las fuentes son compatibles y no hay conflicto abierto. Registro final: dato, valor, fuentes, fecha y estado.
