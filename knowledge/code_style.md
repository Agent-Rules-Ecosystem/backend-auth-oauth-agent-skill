# Estilo Flutter / Dart

- Usar `const` cuando aplique.
- Mantener archivos Dart idealmente bajo 250 líneas; máximo 300.
- Extraer widgets o diálogos extensos de pantallas principales.
- Liberar `TextEditingController`, `AnimationController` y `StreamSubscription`.
- Centralizar estado con patrón elegido por proyecto. Si usa Riverpod, separar vista de providers/notifiers.
- En `DropdownButtonFormField`, usar `initialValue`; evitar `value` deprecado.
