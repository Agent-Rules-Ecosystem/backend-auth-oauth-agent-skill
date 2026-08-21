# Motor de Decisiones — Auth/OAuth2

## Flujo

```mermaid
graph TD
    A["Trigger (auth)"] --> B["Audit — Escanear"]
    B --> C{¿Hallazgos?}
    C -- No --> D["✅ Conforme"]
    C -- Sí --> E["Alta/Media/Baja"]
    E --> F["Fix — Remediar"]
    F --> G["Re-auditoría"]
```

## Matriz de Decisión

| Situación | Prioridad | Acción |
|---|---|---|
| Vulnerabilidad crítica del dominio | Alta | Fix inmediato |
| Violación de convención | Media | Corrección planificada |
| Mejora opcional | Baja | Sugerencia documentada |
