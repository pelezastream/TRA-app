# The Retrenchment Adventures Android App — v1.0.0

This is the Android application for The Retrenchment Adventures, now hosted at **[pelezastream/TRA-app](https://github.com/pelezastream/TRA-app)**. It is independent of the Peleza Stream Android application.

## Final app behaviour

- No native top toolbar.
- The normal TRA website header remains visible.
- The WordPress website footer is hidden inside the Android app by default.
- Native bottom navigation: Home, Products, Events, Gallery, Book.
- Original TRA logo is used for the startup intro.
- Launcher icon is made directly from the original TRA logo.
- WordPress login/account cookies are retained.
- Profile and booking file uploads use the Android file picker.
- Downloads use Android Download Manager.
- External web, telephone, email, SMS, maps and Play Store links open the appropriate app.
- Trusted TRA links stay inside the app.
- WebView renderer failure is handled without crashing the entire Activity.
- No payment/subscription code is added by the Android wrapper.

## Live website

https://www.the-retrenchment-adventures.co.za/

Native bottom navigation uses the current live pages:

- Home: `/`
- Products: `/service-booking/`
- Events: `/events-list-style-with-search-box/`
- Gallery: `/gallery/`
- Book: `/contact-us/`

## Android identity

- Application ID: `za.co.theretrenchmentadventures.app`
- Version: `1.0.0`
- Version code: `1`
- Minimum Android: API 26
- Target/compile API: 36
- Java: 17
- Android Gradle Plugin: 8.13.2
- Gradle: 8.13

## GitHub repository

The transfer to **pelezastream/TRA-app** is complete. Do not create a replacement repository or upload this project into the Peleza Stream Android project.

For signing, testing, and Google Play publishing instructions, see [PLAY-RELEASE-SETUP.md](PLAY-RELEASE-SETUP.md).

## Build the first APK

From the transferred repository:

1. Open **Actions**.
2. Choose **Build TRA Android APK + AAB**.
3. Run the workflow.
4. Download the `TRA-Android-v1.0.0` artifact.
5. Install `The-Retrenchment-Adventures-1.0.0-debug.apk` on the phone.

Because this is a new version-code sequence, uninstall older experimental TRA debug APKs before testing v1.0.0.

## Google Play

After the debug APK is tested successfully, set up the TRA-specific upload key and GitHub secrets using [PLAY-RELEASE-SETUP.md](PLAY-RELEASE-SETUP.md). Merge the signed-release workflow into `main`, then run **Build Signed TRA Play Store Release**.

Use the generated `.aab` for Google Play.
