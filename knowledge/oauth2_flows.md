# Flujos OAuth2 Canónicos

## Authorization Code Flow (usuarios finales)

1. App redirige al usuario al Authorization Server con `client_id`, `redirect_uri`, `scope`, `state`.
2. Usuario se autentica y aprueba permisos.
3. Authorization Server redirige de vuelta con `code` y `state`.
4. Backend intercambia `code` por `access_token` y `refresh_token` (server-to-server).
5. Access token se usa para llamadas a APIs protegidas.

**Puntos de auditoría**: Verificar `state` CSRF, PKCE en clientes públicos, `redirect_uri` en lista blanca.

## Client Credentials Flow (machine-to-machine)

1. Servicio envía `client_id` + `client_secret` al Authorization Server.
2. Recibe `access_token` (sin refresh token).
3. Usa token para llamadas entre servicios.

**Puntos de auditoría**: Secretos en env vars, tokens cacheados y reutilizados hasta expiración.

## Antipatrones a Detectar

| Antipatrón | Severidad |
|---|---|
| JWT secret hardcodeado en código | Alta |
| Sin verificación de `state` en callback | Alta |
| Access token con vida > 1 hora | Media |
| Refresh token en localStorage | Alta |
| Sin rate limiting en `/login` | Media |
