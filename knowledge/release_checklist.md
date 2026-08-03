# INSTRUCCIONES DE BUILD & PRE-RELEASE (FLUTTER)

## DISPARADORES (Triggers)
Cuando el usuario diga cualquiera de estas frases, ejecutar el **Checklist Previo** y al terminar **mostrar el comando correspondiente** para que el usuario lo ejecute manualmente:
- *"voy a hacer el aab"*
- *"voy a hacer el apk"*
- *"revisa antes de compilar"*
- *"revisa todo antes de hacer el build"*
- *"prepara el release"*

> [!IMPORTANT]
> El agente **SOLO corre el checklist y muestra el comando**. NO ejecuta el build. El usuario compila manualmente en su terminal.

---

## CHECKLIST PREVIO (OBLIGATORIO antes de cualquier build)
El agente revisa cada ítem y reporta el resultado:

- [ ] `flutter analyze` ejecutado -> Sin errores ni warnings nuevos.
- [ ] `flutter test` -> Todos los tests en verde (si existen).
- [ ] Sin `print()` o `debugPrint()` olvidados en archivos modificados.
- [ ] Verificar `google-services.json` (Android) y `GoogleService-Info.plist` (iOS) presentes.
- [ ] Verificar `android/key.properties` existe y **no está trackeado en git** (`git check-ignore android/key.properties`).
- [ ] `overview/tracker.md` -> Nodos del ciclo actual en `:::done` (si aplica).

---

## BUILD .AAB (Play Store)

```bash
flutter clean
flutter pub get
flutter build appbundle --release
```
Archivo generado: `build/app/outputs/bundle/release/app-release.aab`

---

## BUILD .APK (Distribución Directa / Pruebas)

```bash
flutter build apk --release --split-per-abi
```
Archivos generados en `build/app/outputs/flutter-apk/`:
- `app-arm64-v8a-release.apk` ← Dispositivos modernos (preferido)
- `app-armeabi-v7a-release.apk` ← Dispositivos 32-bit

---

## BUILD .IPA (iOS / App Store)

```bash
flutter build ipa --release
```
Luego: Xcode -> **Product -> Archive** -> TestFlight / App Store Connect.

---

## POST-BUILD (Opcional, solo para releases a tienda)
- [ ] Instalar `.apk` en dispositivo físico y probar flujo crítico.
- [ ] Verificar que Firebase Crashlytics recibe eventos del build firmado.
- [ ] Registrar en `overview/session.md`: versión y fecha de compilación.

> [!CAUTION]
> `key.properties` y el `.jks` NUNCA deben subirse a GitHub.
