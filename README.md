# 🚀 Flutter Agent Rules (`flutter-agent-rules`)

A centralized, agent-agnostic repository of workflow rules, system prompts, clean architecture guidelines, and persistent memory protocols for Flutter projects. 

Designed to be integrated as a **Git Submodule** (`.agents`) across all your Flutter codebases. Supports **Antigravity / Gemini CLI, Cursor IDE, GitHub Copilot, Codex, and Claude Code**.

---

## 🌟 Key Features

1. **Multi-Agent Compatibility & Path Map:** Universal entry point (`AGENTS.md`) and canonical path directory (`core/path_map.md`) compatible with all major AI coding assistants.
2. **Token Saver & Caveman Mode:** Directives in `core/communication.md` to force ultra-concise, code-first responses and single-line log output.
3. **2-Phase Workflow Protocol:** Bootstrap initialization & strict post-task verification (`flutter analyze` + Mermaid tracker update).
4. **Clean Architecture & File Limits:** Enforces maximum line counts (<250-300 lines) and modular widget extraction.
5. **Separate Dynamic Memory:** Keeps rules static in `.agents/` while storing project-specific memory in `overview/` at the project root.
6. **Mermaid Route Tracking:** Visual route & module progress diagrams rendering natively in VS Code / Cursor / GitHub.

---

## ⚙️ Quick Setup (Git Submodule)

In any Flutter project repository, run:

```bash
git submodule add https://github.com/tu-usuario/flutter-agent-rules.git .agents
```

---

## 🇪🇸 Versión en Español

### Descripción General
Repositorio centralizado e independiente de agente con reglas de flujo de trabajo, instrucciones del sistema, arquitectura limpia en Flutter y protocolos de memoria persistente.

### Características Principales
- **Compatibilidad Universal:** Funciona con Antigravity, Cursor, Copilot y Claude Code via `.agents/AGENTS.md`.
- **Modo Cavernícola & Ahorro de Tokens:** Respuestas directas al código, sin relleno y con log de 1 línea.
- **Protocolo de 2 Fases:** Inicio automatizado y fase de cierre con `flutter analyze` y actualización de Mermaid.
- **Límite de Líneas (<250-300 líneas):** Reglas para refactorizar y extraer widgets/diálogos independientes.
- **Memoria Separada por Proyecto:** Mantiene las reglas en `.agents/` y el estado dinámico en `overview/`.
