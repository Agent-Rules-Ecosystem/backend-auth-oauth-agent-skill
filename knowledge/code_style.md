# REGLAS DE CÓDIGO Y ESTILO (FLUTTER / DART)

> [!IMPORTANT]
> **Estas reglas aplican a TODOS los proyectos.** No requiere copia local. Cargar bajo demanda cuando se vaya a escribir o refactorizar código Dart/Flutter. El agente puede agregar reglas nuevas aquí vía el Protocolo de Auto-Aprendizaje (Sección 5 de `core/brain.md`).

## CONVENCIONES DE ESTILO
- Usar `const` siempre que sea posible para optimizar el árbol de widgets.
- Límite estricto de ~250-300 líneas por archivo `.dart`.
- Evitar métodos `_buildX()` dentro de la clase que retornen Widgets; extraer a un nuevo `StatelessWidget`.
- Dispose obligatorio para `TextEditingController`, `AnimationController` y `StreamSubscription`.
- Manejo de estados centralizado vía Riverpod (`StateNotifier` / `NotifierProvider`).
