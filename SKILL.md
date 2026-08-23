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


---

## 📝 Persistencia y Salida Activa (`overview/work/skill/`)

Al ejecutar esta skill (mediante `$auth` o `$auth:audit`), es **obligatorio crear o actualizar su reporte activo** dentro del proyecto cliente en la ruta:

`overview/work/skill/backend-auth-oauth.md`

### Estructura Requerida del Reporte:

```markdown
# 📋 Registro Activo de Tareas — Backend Auth OAuth Agent Skill

> **Generado por**: `backend-auth-oauth-agent-skill` (`$auth:audit`)  
> **Última actualización**: YYYY-MM-DD  

## 🎯 Tareas Pendientes Accionables

| ID | Tipo | Estado | Resumen | Evidencia/Ruta | Acción Requerida |
|---|---|---|---|---|---|
| OAUTH-01 | Fix / Refactor | Pendiente | <Resumen breve> | `<ruta:línea>` | <Remediación recomendada> |

## 📝 Observaciones y Detalles de Revisión
- Detalle técnico, evidencia o contexto extendido proporcionado por la revisión de la skill.
```
