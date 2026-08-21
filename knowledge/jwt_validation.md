# Validación Correcta de JWT

## Checklist de Validación (server-side)

Antes de confiar en cualquier JWT, verificar:

1. **Firma**: Verificar con la clave pública/secreta correcta.
2. **Algoritmo**: Verificar que `alg` del header coincide con el esperado. Rechazar `alg: none`.
3. **Expiración (`exp`)**: Verificar que el token no ha expirado.
4. **`iat` (issued at)**: Verificar que no es un token emitido en el futuro.
5. **`iss` (issuer)**: Verificar que el emisor es el Authorization Server correcto.
6. **`aud` (audience)**: Verificar que el token fue emitido para este servicio.

## Antipatrones a Detectar

| Antipatrón | Severidad |
|---|---|
| Aceptar `alg: none` | Alta (CVE clásico) |
| No verificar `exp` | Alta |
| No verificar `iss` y `aud` | Media |
| Decodificar sin verificar firma | Alta |
