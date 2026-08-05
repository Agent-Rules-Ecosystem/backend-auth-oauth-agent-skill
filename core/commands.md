# Comandos del Core ($-commands)

Cuando el usuario escribe un comando con prefijo `$`, el agente lo reconoce como instrucción explícita y ejecuta el protocolo correspondiente **inmediatamente**, sin esperar bootstrap automático.

> Propósito: compensar los casos donde el bootstrap automático fue incompleto o no se disparó.

---

## Referencia rápida

| Comando | Acción |
|---|---|
| `$boot` | Bootstrap completo del proyecto |
| `$status` | Mostrar estado actual en resumen |
| `$close` | Protocolo de cierre de sesión |
| `$learn [texto]` | Registrar aprendizaje candidato |
| `$learnagnostico [texto]` | Abstraer a términos genéricos y registrar |
| `$work [descripción]` | Registrar nueva tarea/bug |

---

## Definición de cada comando

### `$boot`

Dispara el bootstrap completo. Equivalente a **"ejecuta .agents"** pero más corto.

Pasos que el agente debe ejecutar:
1. Leer `core/path_map.md`, `core/communication.md`, `core/brain.md`, `core/commands.md`.
2. Verificar si existe `overview/` — si no, crear desde `templates/`.
3. Cargar `overview/session.md`, `overview/work.md`, `overview/trackers/progress.md`.
4. Detectar si el `Agente:` en `session.md` difiere del modelo actual → si difiere, activar protocolo `## Handoff de Agente` de `brain.md`.
5. Alias divergentes: si alias y canónico coexisten con contenido distinto → flag `[consolidar alias]` en `work.md`.
6. `session.md` legado: si faltan `Agente:`, `## Reanudar` o `## Cambios` → reportar `session legado` (sin migrar automático).
7. Auditoría de líneas: listar archivos de código fuente >250L; sugerir IDs `deuda` en `work.md`.
8. Auditar `overview/learning.md`: promover mejoras ya implementadas al Histórico.
9. Reportar en 5 líneas máximo: agente anterior, nodo activo, tareas pendientes, estado validación, flags (alias/session/líneas), próximo paso.

---

### `$status`

Mostrar el estado actual del proyecto sin modificar ningún archivo.

El agente debe leer y reportar en formato compacto:
```
Agente activo : [firma]
Nodo activo   : [id de progress.md]
Validación    : [verificado | no verificado | no aplica]
Tareas abiertas: [IDs y resumen de work.md con estado ≠ hecho]
Próximo paso  : [## Reanudar de session.md]
```

---

### `$close`

Protocolo de cierre de sesión. El agente debe:
1. Ejecutar `flutter analyze` si aplica. Suite de tests: ausente → `no aplica`; presente y no corrida/fallida → `no verificado` + motivo.
2. Actualizar `overview/work.md` con cambios de la sesión.
3. Actualizar `overview/session.md`:
   - Registrar `Agente:` con firma propia.
   - Completar `## Cambios` con lo trabajado.
   - Completar `## Reanudar` con el siguiente nodo y contexto crítico.
4. Actualizar `overview/trackers/progress.md`.
5. Si hay sesiones antiguas irrelevantes → archivar en `overview/history/`.
6. Si hay mejora candidata identificada → agregar a `overview/learning.md`.
7. Reportar: `Sesión cerrada. Próximo: [nodo]. Estado: [verificado/no verificado/no aplica].`

---

### `$learn [texto]`

Registrar un aprendizaje candidato en `overview/learning.md`.

El agente debe:
1. Validar el texto con el **Filtro Agnóstico** (`brain.md`): rechazar código específico, snippets de UI o comandos CLI rígidos. Si contiene código o comandos, abstraer a regla o proceso de diagnóstico agnóstico.
2. Abrir `overview/learning.md`.
3. Agregar bajo `## 📌 Propuestas de mejora` un bullet con el texto agnóstico.
4. Si el archivo no existe, crearlo desde `templates/learning.md`.
5. Confirmar: `Aprendizaje registrado en overview/learning.md.`

Ejemplo de uso:
```
$learn Siempre inicializar GoRouter fuera del widget tree para evitar rebuilds
```

---

### `$learnagnostico [texto]`

Abstraer un aprendizaje candidato descontextualizando el proyecto antes de registrar.

El agente debe:
1. Sustituir nombres propios de app/módulo/ruta por términos genéricos de arquitectura (entidad, flujo, capa, inventario, persistencia, navegación, etc.).
2. Eliminar IDs de negocio, pantallas concretas y paths de proyecto.
3. Aplicar **Filtro Agnóstico** (`brain.md`) al texto resultante.
4. Registrar el bullet abstraído en `overview/learning.md` bajo `## 📌 Propuestas de mejora` (crear desde plantilla si falta).
5. Confirmar: `Aprendizaje agnóstico registrado.` + mostrar una línea con el texto final.

Ejemplo:
```
$learnagnostico En JoyasApp el flujo Oro→Inventario→Fundición debe documentarse aparte de architecture
```
→ bullet: `Documentar flujos de dominio (entidad → inventario → transformación) en overview/workflows/, no en architecture.md.`

---

### `$work [descripción]`

Registrar una nueva tarea o bug en `overview/work.md`.

El agente debe:
1. Determinar tipo: `tarea` (mejora/feature), `bug` (comportamiento inesperado) o `deuda`.
2. Generar el próximo ID correlativo (ej. `w4` si el último es `w3`).
3. Agregar fila **solo** en la tabla principal de `work.md` con estado `pendiente` (nunca en alias `tasks.md`).
4. Si es un bug: agregar entrada vacía en `## 📋 Historial de Intentos` con header `### [ID] [descripción]`.
5. Confirmar: `Registrado como [ID] en work.md.`

Ejemplo de uso:
```
$work bug: el drawer no cierra al navegar con GoRouter en iOS
```

---

## Reglas de parsing

- El prefijo `$` debe ser el **primer carácter** del mensaje o estar en línea propia para ser reconocido como comando.
- Si el `$`-comando va acompañado de texto adicional (ej. `$learn texto aquí`), el texto después del comando es el argumento.
- Si el argumento falta donde es requerido, el agente debe pedirlo en una sola línea.
- Los comandos son **case-insensitive**: `$Boot`, `$BOOT` y `$boot` son equivalentes.
- Si el agente no reconoce el comando, responder: `Comando desconocido. Disponibles: $boot $status $close $learn $learnagnostico $work`.
