# Publication Play Store — Lecteur PDF

> Guide pas-à-pas, même chaîne que construction-site-tracker (Suivi Interventions).

## 1. Artefacts prêts

| Fichier | Usage |
|---|---|
| `android/app/build/outputs/bundle/release/app-release.aab` (3,4 Mo) | **upload Play Console** |
| `android/app/build/outputs/apk/release/app-release.apk` (3,5 Mo) | test hors Play |

Version 1.0.0 / versionCode 1, signés avec `~/keystores/lecteur-pdf-release.keystore` (alias `lecteur-pdf`, validité 30 ans, RSA 4096).

## 2. Play Console (côté utilisateur)

1. **Créer l'application** → nom « Lecteur PDF », langue Français, « Application » (pas jeu), gratuit.
2. ⚠️ **Nom de package** : saisir exactement `fr.rennesdev.lecteurpdf` (champ libre, non modifiable ensuite).
3. **Play App Signing** : laisser « Google gère la clé de signature de l'app » (recommandé — notre keystore reste la clé d'upload).
4. **Tests internes** : créer un test interne, uploader l'AAB.
5. **Déclaration données** : aucune donnée collectée (l'app n'a aucune permission réseau ni stockage) — cocher « Non, aucune donnée ».
6. **Fiche Play Store** : description courte, captures d'écran (installer l'APK sur un téléphone et faire des captures), catégorie « Outils ».
7. **Classifications du contenu**, audience, public cible : « 18+ » n'est pas requis — app tout public sans contenu sensible.
8. Publier en tests internes → quand validé, promotion vers production.

## 3. Nouvelle version

```bash
# 1. modifier android/app/build.gradle : versionCode +1, versionName "x.y.z"
# 2. rebuild
cd ~/projects/lecteur-pdf && npm install && npx cap sync android
cd android && ./gradlew bundleRelease assembleRelease
# 3. commit + tag + release GitHub (même procédure que suivi-interventions)
```

## 4. Signature — TRÈS IMPORTANT

- Keystore : `~/keystores/lecteur-pdf-release.keystore` + credentials `lecteur-pdf-credentials.txt` (root-only, HORS repo).
- ⚠️ **Sauvegarder le keystore + mot de passe hors VPS** (comme pour suivi-interventions). Sans eux, impossible de publier une mise à jour de l'app.
- Validité certificat : 30 ans.
