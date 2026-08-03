# Core Brain & Decision Logic

## 1. Protocolo de Trabajo en 2 Fases (Bootstrap vs Validación)

```mermaid
graph TD
    classDef phase fill:#1565c0,stroke:#fff,color:#fff;
    classDef check fill:#2e7d32,stroke:#fff,color:#fff;

    A[Fase 1: Bootstrap / Inicio]:::phase --> B{¿Existe overview/?}
    B -- No --> C[Crear carpeta overview/ y plantillas .md]
    B -- Sí --> D[Verificar archivos de memoria]
    C --> E[Carga Obligatoria: .agents/AGENTS, comms, brain + overview/session, tasks]
    D --> E
    E --> F[Ejecución de Tareas (Cambios Quirúrgicos)]
    F --> G[Fase 2: Validación / Cierre]:::phase
    G --> H[Ejecutar flutter analyze / test]
    H --> I[Actualizar overview/tracker.md y memorias]
    I --> J[Resumen de Cierre en Consola (1 Línea)]:::check
```

### 1.1 Fase 1: Bootstrap y Carga Inicial
Antes de modificar código en cualquier proyecto Flutter:
- **Verificación de Submódulo Actualizado:** Ejecutar la verificación silenciosa de Git (`git submodule status`) para saber si `.agents/` está en la última versión de `main`.
- **Directorio Canónico:** Consultar `.agents/core/path_map.md` para resolver la ubicación exacta de cada archivo.
- Leer reglas globales desde `.agents/core/`.
- Cargar memoria activa local desde `overview/session.md` y `overview/tasks.md`. Si `overview/` no existe en el proyecto, **crearla inmediatamente**.

### 1.2 Fase 2: Validación y Cierre de Sesión
Al concluir modificaciones de código:
- Ejecutar linter/tests (`flutter analyze`, `flutter test`).
- Actualizar nodos en `overview/tracker.md` (Mermaid) cambiando estados de `:::pending` a `:::done`.
- Registrar resumen en `overview/session.md` y actualizar `overview/tasks.md`.

## 2. Cambios Quirúrgicos & Calidad
- Tocar solo lo estrictamente necesario. No inventar funciones extras.
- No "mejorar" código adyacente que ya funciona.
- Límite de ~250-300 líneas por archivo `.dart`. Extraer subwidgets si excede.
- Si algo se puede hacer con 50 líneas en vez de 200, simplificar a 50.

## 3. Contexto del Proyecto Base
- Tecnologías: Flutter + Cloud Firestore (Firebase).
- Enfoque: SaaS Control de Producción (Clientes, Productos, Bitácora).
- Arquitectura: Riverpod (StateNotifier).

## 4. Checklist Obligatorio de Finalización
- [ ] `flutter analyze` ejecutado sin errores introducidos.
- [ ] Diagrama Mermaid en `overview/tracker.md` actualizado (`:::done`).
- [ ] `overview/session.md` actualizado con el último nodo trabajado.
- [ ] Archivos Dart verificados (< 250-300 líneas).
- [ ] Log de 1 línea al final de la respuesta.

## 5. Protocolo de Aprendizaje Bajo Confirmación (User Approval)
- **Registro de Aprendizaje Local:** Cuando el agente detecte una optimización, regla o corrección clave durante la sesión, la preparará localmente pero **NO enviará ningún push automático a GitHub**.
- **Notificación al Usuario:** Al finalizar la sesión o al ser consultado ("¿has aprendido algo?"), el agente resumirá el nuevo patrón y preguntará:
  > *"He identificado el patrón X para optimizar Y. ¿Deseas guardar y subir esta regla al repositorio principal `.agents`?"*
- **Ejecución de Push tras Aprobación Explicita:** Solo tras el "Sí" o aprobación explícita del usuario, el agente ejecutará los comandos de Git:
  1. Commit en submódulo: `git -C .agents commit -am "feat(rules): nueva regla aprendida"`
  2. Push a repositorio central: `git -C .agents push origin main`
  3. Actualización de referencia local: `git commit -am "chore: update .agents reference"`
