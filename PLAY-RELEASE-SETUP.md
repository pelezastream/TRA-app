# TRA Android — Google Play release checklist

**Canonical repository:** https://github.com/pelezastream/TRA-app
**Android package:** `za.co.theretrenchmentadventures.app`
**Website:** https://www.the-retrenchment-adventures.co.za/

This project is distinct from the Peleza Stream Android app. Do not reuse its package name or upload key.

## 1. Test the existing debug APK

1. In this repository, open **Actions > Build TRA Android APK + AAB > Run workflow** on `main`.
2. Download artifact `TRA-Android-v1.0.0`, extract it and install the *debug APK* on a physical Android device.
3. Verify splash screen, Home, Products, Events, Gallery, Book, login, account cookies, booking and upload forms, downloads, external links, Android back navigation and offline recovery.
4. Check layout and system-bar visibility on Android 16. Test at least a small-screen phone and a recent Android phone.

The normal workflow's release AAB is **unsigned**; it is **not** a Play upload file.

## 2. Create a permanent TRA upload key

On a trusted computer with the Java JDK, run:

~~~sh
keytool -genkeypair -v -keystore tra-upload-key.jks -alias tra-upload -keyalg RSA -keysize 4096 -validity 10000
~~~

Choose strong passwords. Back up the original JKS securely and offline. Do **not** commit it, disclose it in a chat, or upload it as an ordinary repository file.

To create the Base64 value locally (macOS/Linux):

~~~sh
base64 < tra-upload-key.jks | tr -d '\n' > tra-keystore-base64.txt
~~~

Go to **Settings > Secrets and variables > Actions > New repository secret** and add:

| Secret | Content |
|---|---|
| `ANDROID_KEYSTORE_BASE64` | Entire single-line Base64 content of your TRA JKS |
| `ANDROID_KEYSTORE_PASSWORD` | JKS store password |
| `ANDROID_KEY_ALIAS` | `tra-upload` |
| `ANDROID_KEY_PASSWORD` | Upload key password |

The secrets are needed for a signed build and must not be exposed in logs or pull requests.

## 3. Build the signed release APK and Google Play App Bundle

Once `.github/workflows/tra-signed-release.yml` is merged into `main` and signing secrets are configured:

1. Open **Actions > Build Signed TRA Play Store Release > Run workflow**.
2. For the first Play upload, use version code `1` and version name `1.0.0` **only if this application ID has never been uploaded to Play before**; otherwise use a higher unused version code.
3. Download the `TRA-Play-...` artifact and extract the signed `.aab` file.
4. The artifact now contains both a signed release APK for direct installation and a signed AAB for Google Play. Verify the certificate fingerprint matches the permanent TRA upload key.\n5. Preserve the signing key and passwords for future updates.

A successful workflow verifies digital signatures for the APK and AAB; it does **not** prove that Google Play will accept the app.

## 4. Google Play Console

1. Create a separate app **The Retrenchment Adventures** under your Play developer account.
2. Complete Play App Signing setup and upload the TRA signed AAB to **Internal testing** first.
3. Complete the store listing with actual in-app screenshots, 512×512 icon, 1024×500 feature graphic, app descriptions, contact information and a functioning privacy policy URL.
4. Complete the Data safety, Ads, Content rating, Target audience and other App content declarations accurately. Provide account deletion information if the app allows account creation.
5. Test the signed app via Google Play and fix any defects or policy issues.
6. For personal developer accounts created after November 13, 2023, run a **closed test with at least 12 testers opted in for 14 consecutive days**, then request production access.
7. Only publish to production after approval and verification of the app's functionality, policy compliance, and privacy disclosures.

Reference: https://support.google.com/googleplay/android-developer/answer/14151465

## 5. Quality gates before launch

- Mobile website pages are live, functional and accessible within the Android app.
- The WebView does not show an error, blank screen, hidden controls or clipped navigation.
- Real device tests cover login, reservations, checkout/payment if present, form uploads, links and connectivity.
- If the website collects personal data, privacy practices and Play Data safety disclosures match real behavior.
- Confirm permission to use all TRA brand assets.
- Never upload the TRA upload key itself to the Play Console or to a public repository.
