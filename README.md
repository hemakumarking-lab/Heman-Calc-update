# Heman's Calc (Android)

GST calculator (portrait) with a scientific calculator (landscape).
Web app in `www/index.html`, packaged with Capacitor. GitHub Actions builds the APK.

## 1. Quick start (debug APK, no setup)
1. Push this folder to a GitHub repository on the `main` branch.
2. Open the **Actions** tab, wait for "Build Android APK" to finish.
3. Download **hemans-calc-debug-apk** under Artifacts, unzip, install `app-debug.apk`.

## 2. Signed release APK
Create a keystore once on your computer (keep it safe, never upload it to the repo):

    keytool -genkeypair -v -keystore release.jks -alias heman -keyalg RSA -keysize 2048 -validity 10000

Convert it to text:

    Linux:  base64 -w0 release.jks
    Mac:    base64 -i release.jks

In the repository open Settings > Secrets and variables > Actions > New repository secret, and add:

| Secret | Value |
| --- | --- |
| KEYSTORE_BASE64 | the base64 text from above |
| KEYSTORE_PASSWORD | the keystore password |
| KEY_ALIAS | heman (the alias you used) |
| KEY_PASSWORD | the key password |

Push again (or run the workflow from the Actions tab). Download **hemans-calc-release-apk**.
Always sign updates with the same keystore, or phones will refuse to update the app.

## Offline fonts
The workflow copies the Poppins and Outfit fonts into the app, so it works without internet.

## App icon
Icons live in `assets/` (`icon-foreground.png`, `icon-background.png`, `icon-only.png`, 1024x1024).
The workflow turns them into all Android sizes. Replace those three files to change the icon.

## Change the app
Edit `www/index.html` and push. App ID is in `capacitor.config.json`.
