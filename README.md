# Lecteur PDF

Lecteur de PDF Android **simple, gratuit, sans publicité, 100 % hors ligne**.

- 📄 Ouvre n'importe quel PDF depuis le téléphone
- 🔍 Zoom 7 niveaux (−/＋), défilement fluide page par page
- 🌙 Mode sombre (mémorisé)
- 🔒 **Aucune publicité, aucun tracker, aucune permission réseau** — le PDF ne quitte jamais le téléphone

## Technique

- WebView Capacitor 8 (`fr.rennesdev.lecteurpdf`), rendu **PDF.js 4** embarqué dans `www/pdfjs/` (aucun CDN, fonctionne hors ligne)
- Palette maxSdk = aucune permission Android demandée (pas d'Internet, pas de stockage : le file chooser du WebView suffit)
- Build : JDK 21 + SDK Android 36 (`/opt/android-sdk`), Gradle 8.14.3, AGP 8.13
- Signature release : keystore hors repo (`~/keystores/lecteur-pdf-release.keystore`), `android/keystore.properties` gitigné

## Build

```bash
npm install
npx cap sync android
cd android && ./gradlew bundleRelease assembleRelease
```

Artefacts :
- `android/app/build/outputs/bundle/release/app-release.aab` → Play Console
- `android/app/build/outputs/apk/release/app-release.apk` → test direct (sideload)

Voir `PLAY-STORE.md` pour la publication.
