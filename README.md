# 🔐 Backend Auth OAuth Agent Skill

> **Skill especializada** — Auditoría e implementación de autenticación OAuth2/JWT/OIDC en backends.
> Skill de tipo **Especializada Backend** (requiere `backend-agent-rules` como base).

---

## 📌 Propósito y Alcance

1. 🔍 **Auditar** implementaciones de JWT, OAuth2 y sesiones en el backend.
2. 🛠️ **Detectar** vulnerabilidades de autenticación (secretos hardcodeados, tokens inseguros).
3. 📐 **Validar** flujos OAuth2 (Authorization Code, Client Credentials, PKCE).
4. 🔧 **Guiar** la implementación de refresh token rotation y revocación.
5. 📋 **Reportar** deuda de seguridad en la capa de autenticación.

---

## ⚡ $-Comandos

| Comando | Acción |
|---|---|
| `$auth` | Bootstrap |
| `$auth:audit` | Auditoría completa de auth |
| `$auth:fix` | Remediación post-audit |
| `$auth:secrets` | Escaneo de secretos hardcodeados |
| `$auth:flow [tipo]` | Guía de flujo OAuth2 |

---

## 📦 Instalación

```bash
git submodule add https://github.com/xolotl-hub/backend-auth-oauth-agent-skill.git .skill/backend-auth-oauth-agent-skill
```
