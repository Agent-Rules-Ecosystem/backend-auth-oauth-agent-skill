---
name: backend-auth-oauth-agent-skill
description: Auditoría e implementación de autenticación y autorización OAuth2/JWT/OIDC en backends.
---

# Backend Auth Oauth Skill Directive

## Bootstrap de la Habilidad

Al detectar triggers de Auth/OAuth2 (`$auth`, `auth audit`, `oauth patterns`, `jwt audit`):

1. `.skill/backend-auth-oauth-agent-skill/SKILL.md` ← Directiva principal
2. `.skill/backend-auth-oauth-agent-skill/core/commands.md` ← $-Comandos
3. `.skill/backend-auth-oauth-agent-skill/core/brain.md` ← Motor de decisiones

## Reglas Canónicas de Auth/OAuth2

- **Secretos en variables de entorno**: JWT secrets, client_id y client_secret nunca en código fuente.
- **JWT expiración corta**: Access tokens con vida útil máxima de 15 minutos; refresh tokens en HttpOnly cookies.
- **Validación server-side**: Nunca confiar en claims de tokens sin verificar firma y expiración en el servidor.
- **HTTPS obligatorio**: Toda ruta de autenticación debe operar exclusivamente sobre HTTPS.
- **Rate limiting en endpoints de auth**: `/login`, `/token`, `/refresh` deben tener rate limiting para prevenir fuerza bruta.
