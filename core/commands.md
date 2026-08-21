# $-Comandos de Auth/OAuth2

| Comando | Acción | Descripción |
|---|---|---|
| `$auth` | Bootstrap | Inicializa la skill y carga contexto del dominio. |
| `$auth:audit` | Auditoría | Escanea el proyecto y genera reporte de hallazgos. |
| `$auth:fix` | Remediación | Aplica mejoras del último `$auth:audit`. |
| `$auth:fix [ruta]` | Puntual | Aplica fix a un archivo o directorio específico. |
| `$auth:secrets` | Escaneo | Detecta secretos hardcodeados en archivos de auth. |
| `$auth:flow [tipo]` | Guía | Describe el flujo canónico para `authorization_code`, `client_credentials` o `refresh`. |
