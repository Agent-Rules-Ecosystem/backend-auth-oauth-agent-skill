---
name: backend-auth-oauth-agent-skill
description: Auditoría e implementación de autenticación y autorización OAuth2/JWT/OIDC en backends.
---

# Backend Auth Oauth Skill Matrix

## Capacidades

```mermaid
graph LR
    A[AUTH] --> B[Auditoría de Dominio]
    A --> C[Patrones Canónicos]
    A --> D[Detección de Antipatrones]
    A --> E[Remediación Guiada]
```

## Protocolo de Auditoría (`$auth:audit`)

1. Detectar archivos del dominio en el proyecto
2. Evaluar cumplimiento de patrones canónicos
3. Identificar antipatrones y deuda técnica
4. Reporte por severidad (Alta / Media / Baja)
5. Remediación con `$auth:fix`
