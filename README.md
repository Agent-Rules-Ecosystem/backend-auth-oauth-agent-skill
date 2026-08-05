# Flutter Agent Rules

Repositorio centralizado: cerebro operativo para proyectos Flutter. Reduce ruido/tokens, conserva continuidad y exige calidad verificable. Se instala como submódulo `.agents/`; reglas globales son independientes del proyecto.

## Qué aporta

1. **Comunicación concisa** — modo cavernícola + ahorro de tokens sin bajar calidad técnica.
2. **Trackers separados** — arquitectura, trabajo, progreso y contenido por agente.
3. **Memoria versionada** — sesión con firma de Agente, historial de intentos incremental y aprendizajes candidatos.
4. **Handoff de Agente** — protocolo para cambiar de modelo sin perder estado ni repetir trabajo fallido.
5. **Historial de intentos firmado** — cada bug registra quién intentó qué y quién lo resolvió, con causa raíz y solución.
6. **$-Comandos** — atajos explícitos (`$boot`, `$status`, `$close`, `$learn`, `$learnagnostico`, `$work`) para disparar protocolos cuando el bootstrap automático falla o es incompleto.
7. **Validación explícita** — `verificado`, `no verificado` o `conflicto`; nunca presentar como validado sin evidencia.
8. **Adaptadores mínimos** — Codex, Claude, Gemini/Antigravity y Cursor; sin duplicar reglas.

## Instalación

```bash
git submodule add https://github.com/xolotl-hub/flutter-agent-rules.git .agents
```

Instalar adaptador de `.agents/adapters/` que reconozca el agente. En el **proyecto Flutter**, crear `overview/` desde `.agents/templates/` (`$boot`). El submódulo `.agents/` no versiona `overview/`: solo plantillas y reglas.

## Uso rápido

| Escribir | Resultado |
|---|---|
| `$boot` | Bootstrap completo + handoff si cambió el agente |
| `$status` | Estado actual en 5 líneas |
| `$close` | Cierre de sesión con validación |
| `$learn [texto]` | Registrar aprendizaje candidato |
| `$learnagnostico [texto]` | Abstraer y registrar aprendizaje genérico |
| `$work [descripción]` | Registrar tarea o bug nuevo |
| `ejecuta .agents` | Bootstrap completo + auditoría de learning |

## Contenido contrastado

Cada agente registra datos en su tracker. Un dato es `verificado` cuando al menos dos coinciden, las fuentes son compatibles y no hay conflicto abierto. Registro final: dato, valor, fuentes, fecha y estado.
