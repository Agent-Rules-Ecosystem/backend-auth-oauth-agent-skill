---
name: agent-rules-governance
description: Rules for managing shared team skills, repository write permissions, and Pull Request governance.
---

# Gobernanza y Seguridad de Reglas (`flutter-agent-rules`)

## 1. Protección de Repositorio Central (GitHub)
- **Repositorio Privado o Protegido:** El repositorio central de reglas (`flutter-agent-rules`) debe tener la rama `main` protegida contra pushes directos no autorizados.
- **Flujo de Pull Request (PR):** Si otros desarrolladores desean sugerir nuevas reglas o cambios en `.agents/`, deben hacer un PR que requiere tu aprobación explícita.
- **Prohibición de Push Automático en Equipos:** El agente nunca ejecutará `git push` a `origin/main` en entornos compartidos sin verificación de credenciales y autorización del propietario del repo.

> [!CRITICAL]
> REGLAS INVIOLABLES DE OPERACIÓN PARA CUALQUIER AGENTE (ANTIGRAVITY / GEMINI / CURSOR / CODEX / CLAUDE).
> ANTES DE RESPONDER O GENERAR CÓDIGO, DEBES CARGAR Y CUMPLIR ESTRICTAMENTE:
> 1. [core/communication.md](file:///c:/Users/termo/Documents/GitHub/flutter-agent-rules/core/communication.md) -> Modo Cavernícola, Ahorro de Tokens, Log 1 Línea.
> 2. [core/brain.md](file:///c:/Users/termo/Documents/GitHub/flutter-agent-rules/core/brain.md) -> Cambios Quirúrgicos, Protocolo 2 Fases, Contexto Flutter.

## CARGA Y SEPARACIÓN DE CONTEXTO

> [!TIP]
> Para cualquier duda sobre ubicaciones de archivos, consultar el mapa canónico: [core/path_map.md](file:///c:/Users/termo/Documents/GitHub/flutter-agent-rules/core/path_map.md).

### 1. Reglas Globales y Estáticas (Leídas desde el submódulo `.agents/`)
- **Obligatorio en cada respuesta:**
  - `.agents/core/path_map.md`
  - `.agents/core/communication.md`
  - `.agents/core/brain.md`
- **Bajo Demanda:**
  - `.agents/knowledge/architecture.md`
  - `.agents/knowledge/code_style.md`
  - `.agents/knowledge/release_checklist.md`

### 2. Memoria y Estado Local del Proyecto (Guardado en `overview/` en la raíz del proyecto)
- **Obligatorio al iniciar y finalizar sesión:**
  - `overview/session.md` (Memoria episódica)
  - `overview/tasks.md` (Backlog y tareas activas)
  - `overview/tracker.md` (Rastreador Mermaid de rutas/archivos)
