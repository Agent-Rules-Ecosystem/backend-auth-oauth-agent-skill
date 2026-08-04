# Checklist pre-release Flutter

Cuando usuario pida APK, AAB, IPA o revisión de build: ejecutar checklist, mostrar comando; no ejecutar build sin solicitud explícita.

- [ ] `flutter analyze` sin errores nuevos.
- [ ] `flutter test` verde, si hay tests.
- [ ] Sin `print()`/`debugPrint()` olvidados en cambios.
- [ ] Configuración Firebase presente, si proyecto la usa.
- [ ] Claves de firma presentes y no trackeadas, si aplica.
- [ ] `overview/trackers/progress.md` y tracker correspondiente actualizados.

## AAB

```bash
flutter clean
flutter pub get
flutter build appbundle --release
```

## APK

```bash
flutter build apk --release --split-per-abi
```

## IPA

```bash
flutter build ipa --release
```
