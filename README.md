# mon_app_ios

App React Native + Expo (SDK 57), build iOS **non signé** via GitHub Actions, à re-signer avec Sideloadly ou AltStore.

## Workflow

Fichier : `.github/workflows/ios-unsigned.yml`

- Runner `macos-latest`, aucun secret Apple requis.
- `expo prebuild` → `xcodebuild` avec `CODE_SIGNING_ALLOWED=NO` → `unsigned.ipa` (dossier `Payload/`).
- Artefact `ios-unsigned-ipa` disponible 7 jours dans l'onglet Actions.

Déclenchement : push sur `main` ou bouton Run workflow.

## Utilisation

1. Push sur `main`.
2. GitHub → Actions → job → télécharger `ios-unsigned-ipa`.
3. Sideloadly (ou AltStore) → ouvrir `unsigned.ipa` → signer avec ton Apple ID gratuit → installer sur iPhone.

## Dev local

```bash
npm install
npx expo start
npx tsc --noEmit
```

## Config

- `app.json` : `ios.bundleIdentifier = com.monappios.app` (modifiable avant build si tu veux un autre ID).
- `eas.json` conservé pour un éventuel build EAS, mais non utilisé par ce workflow.
