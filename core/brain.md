# Core Brain

## Ciclo

```mermaid
graph TD
    A[Trigger arranque] --> B{Existe overview/}
    B -- No --> C[Crear desde .agents/templates/]
    B -- Sí --> D[Cargar estado]
    C --> E[Discovery de proyecto]
    D --> E
    E --> F[Trabajar]
    F --> M{Autocheck modo cavernicola}
    M -- Falla --> R[Reescribir respuesta]
    R --> G[Validar]
    M -- OK --> G
    G --> H[Actualizar trackers y sesión]
    H --> F
```

## Triggers de arranque

Las siguientes señales disparan el protocolo completo de bootstrap (discovery + crear `overview/` si falta + mapear archivos existentes):

- Frase **"ejecuta .agents"** → dispara el Protocolo de Auditoría de Learning (ver abajo).
- Inicio de sesión en cualquier proyecto con `.agents/` presente.
- Mensaje del usuario que mencione "nuevo proyecto", "inicializar", "bootstrap" o similar.
- Ausencia de `overview/session.md` al comenzar cualquier tarea de código.
- Primer mensaje de una conversación cuando el proyecto tiene `.agents/` pero no tiene `overview/`.
- **Mensaje que comienza con `$`** → reconocer como $-comando y ejecutar protocolo definido en `core/commands.md` sin bootstrap completo previo.

## Protocolo "ejecuta .agents"

Cuando el usuario escribe **"ejecuta .agents"** (o variante como "corre .agents", "bootstrap .agents"):

1. **Leer el core completo**: `path_map.md`, `communication.md`, `brain.md`, `commands.md` y `AGENTS.md`.
2. **Auditar `overview/learning.md`**: por cada bullet en `## 📌 Propuestas de mejora`, verificar si ya está implementado en los archivos del core o en los archivos del proyecto.
3. **Promover las cumplidas**: mover cada propuesta verificada como implementada → al final de `## 📜 Histórico de mejoras aplicadas` con formato `- [YYYY-MM-DD] Descripción breve`.
4. **Conservar las pendientes**: dejar sin modificar los bullets que aún no están implementados en el core.
5. **Continuar con el flujo normal del core**: Inicio → Discovery → verificar `overview/` → trabajar.

## Inicio

- Ejecutar `git submodule status`.
- Leer core y `overview/session.md`, `overview/work.md`, `overview/trackers/progress.md`.
- Si falta `overview/` o archivos base, crearlos desde `.agents/templates/`.
- Si falta `overview/architecture.md`, crearlo desde plantilla antes de trabajar.
- **Registro preventivo previo a ejecución (Pre-execution Work Logging)**: Al recibir un requerimiento o bug, actualizar `overview/work.md` y `overview/session.md` INMEDIATAMENTE antes de ejecutar cualquier acción. En caso de reporte de bug, incluir una hipótesis breve de causa raíz (5-7 palabras). Derivar automáticamente 1 o 2 mejoras/tareas asociadas a los pendientes para garantizar tolerancia a desconexión, corte de luz o agotamiento de tokens.
- **Historial de Intentos firmado por Agente**: En `work.md` y trackers de bugs/tareas, mantener un registro incremental de intentos de resolución. Nunca borrar intentos previos. Reglas:
  - **Mismo día:** actualizar la entrada existente de esa fecha (sin duplicar).
  - **Diferente día:** crear nueva entrada con fecha + **firma del Agente** (modelo/versión) que ejecutó la prueba.
  - **Al resolver:** marcar estado como `hecho` indicando el Agente que logró la solución. Incluir nota concisa con (1) causa raíz exacta y (2) solución aplicada (código/configuración).
  - **Propósito:** ante problema similar futuro, consultar historial para reusar la solución exitosa o recomendar al agente que la resolvió.

### Discovery dinámico por framework

1. Identificar framework del proyecto (Flutter → `pubspec.yaml`; Node → `package.json`; etc.).
2. Comparar carpetas raíz contra las carpetas estándar conocidas del framework (para Flutter, consultar `.agents/knowledge/flutter_structure.md`).
3. Inspección recursiva automática de toda carpeta no estándar: identificar de forma estricta las carpetas estándar del framework detectado y procesar automáticamente cualquier otro directorio raíz (incluyendo subcarpetas anidadas) mediante inspección semántica de contenido para su relocalización a `overview/` sin omitir ninguna por ser no-estándar.
4. Relocalización activa de metadatos: no ignorar archivos sin categoría; extraer y relocalizar documentación, notas de negocio o trackers hallados en subdirectorios no estándar a `overview/context/` o al tracker canónico correspondiente para cero archivos huérfanos.
5. **Lectura activa de contexto (`overview/context/`)**: El protocolo de inicio debe inspeccionar y leer automáticamente los archivos de contexto guardados en `overview/context/` (changelogs, tablas de datos, reglas de negocio) para recuperar el estado histórico y checkpoints del proyecto al reanudar.
6. **Auto-inicialización de trackers de contenido externo (`content_*.md`)**: Al detectar manejo o extracción de datos de dominio (ej. catálogo/Gembook), el bootstrap debe crear e inicializar automáticamente los trackers `content_gemini.md`, `content_claude.md`, `content_gpt.md` y `content_verified.md` desde `.agents/templates/trackers/`.
7. **Exploración progresiva del sistema**: La cartografía del proyecto debe desarrollarse de forma incremental y contextual, evitando una revisión exhaustiva de todo el código en una sola pasada. Las zonas nuevas del mapa se incorporan conforme el trabajo las requiere, preservando una visión clara del alcance real de la tarea sin sobreexplorar el repositorio. **Guardrail de tokens en discovery inicial:** leer máx 5 archivos de código fuente en el primer sweep; expandir solo cuando la tarea lo requiera explícitamente.

### Reconocimiento de acrónimos estándar

Reconocer automáticamente sin listas rígidas: `i18n`, `l10n`, `auth`, `routes`, `api`, `dto`, `repo`, `vm`, `bloc`, `di`, `ioc`, `ci`, `cd`, `qa`, `ux`, `sdk`, `orm`, `rbac`, `jwt`, `ssr`, `csr`. Si aparece un acrónimo desconocido → buscar en contexto del proyecto antes de preguntar.

### Clasificación semántica por contenido

Al encontrar cualquier carpeta o archivo no mapeado al framework, inspeccionar su contenido interno independientemente del nombre de la carpeta:

| Señales en contenido | Clasificar como |
|---|---|
| Fechas, `## Sesión`, `## Objetivo` | `overview/history/` |
| `- [ ]`, `- [x]`, progreso, estado | `overview/trackers/` |
| Resúmenes ejecutivos, arquitectura | `overview/architecture.md` |
| Contexto de negocio, datos de dominio | `overview/context/` |
| Mejoras al core, candidatos | `overview/learning.md` |

### Normalización de rutas

- Todas las rutas de `overview/` siempre en minúsculas: `overview/`, `overview/trackers/`, `overview/history/`, `overview/context/`.
- Si existe colisión (`Overview/` vs `overview/`): mapear alias, usar ruta lowercase como canónica.
- En Linux/Mac (case-sensitive): verificar con `ls` antes de asumir que no existe.

### Política de relocalización activa y no ignorar

Ningún archivo de documentación, notas de negocio o tracker hallado en subdirectorios no estándar puede ignorarse silenciosamente o quedar huérfano. Opciones:

1. Mapeado a categoría conocida → relocalizar/consolidar en `overview/`, `overview/trackers/` u `overview/history/`.
2. Contexto de dominio o metadatos sueltos → extraer y relocalizar activamente a `overview/context/`.
3. Ambiguo → referenciar en `overview/work.md` con nota `[pendiente clasificar]`.

## Handoff de Agente

Cuando el Agente que retoma una sesión es distinto al que la inició (diferente modelo o proveedor):

1. **Identificar cambio**: comparar `Agente:` en `overview/session.md` con el modelo actual. Si difieren → activar protocolo de handoff.
2. **Validar estado previo**: leer `## Reanudar` de `session.md` y verificar que el `Contexto crítico` es coherente con el estado actual de los archivos mencionados. Si hay inconsistencia, anotar en `work.md` antes de continuar.
3. **No asumir correctitud**: el Agente entrante no da por válido el trabajo del anterior sin verificación. Inspeccionar el último cambio registrado en `## Cambios` y confirmar que el archivo/función afectado existe y compila.
4. **Registrar handoff**: al comenzar a trabajar, actualizar `session.md`:
   - `Agente que reanuda:` con la firma propia (formato `core/communication.md §3`).
   - Añadir bullet en `## Cambios`: `- Handoff de [Agente anterior] → [Agente actual].`
5. **Historial de intentos**: si hay bugs abiertos en `work.md`, revisar el historial de intentos antes de proponer solución — el agente anterior puede haber intentado el mismo enfoque.

> Propósito: evitar trabajo duplicado, detectar inconsistencias de estado y aprovechar el historial firmado para elegir el enfoque más efectivo.

## Arquitectura viva y Modularización

- **Arquitectura viva en `overview/architecture.md`**: El proyecto debe mantener un mapa operativo actualizado por sesión; cada cambio en pantallas, cards, modelos, estado o persistencia debe reflejarse en `overview/architecture.md` para conservar continuidad y visibilidad de conexiones entre flujo y datos.
- **Modularización de Trackers por Subcarpetas / Archivo Individual**: Para colecciones masivas de datos (ej. Gembook con 50+ gemas en orgánicas/, preciosas/, semipreciosas/, sintéticas/), los trackers de contenido deben modularizarse en directorios (`overview/trackers/content/<categoria>/<item>.md`) y el contenido verificado mapearse directamente a la estructura final en app (ej. `lib/pages/gembook/data/`).

## Cierre

- Ejecutar `flutter analyze` y `flutter test` cuando apliquen.
- Actualizar tracker correspondiente, sesión y trabajo. Si se resolvió un bug/tarea con historial de intentos, registrar firma del Agente resolvedor, causa raíz y solución en la entrada correspondiente de `work.md`.
- Si validación falla o no puede ejecutarse: marcar `no verificado`, indicar motivo; nunca presentar como validado.
- Archivar sesiones antiguas en `overview/history/` cuando dejen de ser útiles al contexto activo.
- Si hay mejora candidata al core: agregar bullet a `overview/learning.md` (lista limpia, sin fechas/estados).
- Una vez promovida al repo oficial: mover al Histórico como una línea. Eliminar el bullet activo.

## Calidad

- Cambios quirúrgicos. No mejorar código ajeno sin necesidad.
- Flutter: Firebase y manejo de estado dependen de cada proyecto.
- Archivos Dart idealmente <250 líneas; máximo 300.

## Contenido externo

- Usar trackers separados: Gemini, Claude y GPT.
- `verificado` = 2+ agentes coinciden, fuentes compatibles y sin conflicto abierto.
- Registrar resultado breve, fuentes y fecha. Si hay conflicto, marcar `conflicto`.

