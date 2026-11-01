# Live OCR Stitcher — Android Studio project

Native Android starter project for continuous screen OCR using MediaProjection and on-device ML Kit Text Recognition.

## Features
- Android system screen-sharing permission prompt.
- Foreground screen-capture service.
- OCR frames processed locally with ML Kit Latin text recognition.
- Recent-line deduplication to reduce repeated text while scrolling.
- Editable in-memory transcript in the activity.
- Copy all text and Android share-sheet handoff to ChatGPT or another app.
- No screenshot files, gallery writes, database, or app-level transcript persistence.

## Build an APK
1. Install Android Studio (current stable) on a computer.
2. Open this project folder in Android Studio.
3. Let Gradle sync and download dependencies.
4. Connect an Android phone with USB debugging enabled, or use an emulator.
5. Select **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
6. Install the generated debug APK from `app/build/outputs/apk/debug/`.

The first build needs internet access to download Gradle and ML Kit dependencies. OCR recognition itself uses the bundled ML Kit Latin model after installation.

## Use
1. Open Live OCR Stitcher.
2. Tap START SCREEN OCR.
3. Accept Android's screen-sharing prompt.
4. Switch to Chrome, UWorld, a PDF reader, or another app and scroll.
5. Return to Live OCR Stitcher to view/copy/share the transcript. The foreground capture service continues while the app is in the background.
6. Use PAUSE or STOP when finished.

## Privacy and Android limitations
- This project does not write captured frames or transcript text to persistent storage.
- Frames are held temporarily in memory and recycled after OCR completes.
- Android itself controls the screen-capture permission and displays a system capture indicator.
- Some apps (especially banking, DRM-protected, or secure-window apps) may block screenshots; this app cannot bypass that.
- The initial implementation uses Latin-script ML Kit OCR. It is not tuned for every language, mathematical notation, tables, or multi-column layouts.
- Deduplication is line-based and can occasionally omit repeated lines that are genuinely repeated in the source. Review important text.
- ChatGPT handoff uses Android's share sheet. The user chooses ChatGPT and confirms sending; a third-party app cannot silently inject text into an existing ChatGPT conversation.
- The app does not delete screenshots that the user previously created with the phone's camera or screenshot function. It simply does not create its own screenshot files.
- For production release, review Android foreground-service and notification behaviour on the target Android version/device and add a persistent capture-state indicator in the UI.

## Project details
- Package: `com.example.liveocr`
- Min SDK: 26 (Android 8.0)
- Target SDK: 35


## Build the APK without Android Studio (GitHub Actions)
1. Create a new GitHub repository.
2. Upload the complete contents of this project folder (including the hidden `.github` folder).
3. Open the repository's **Actions** tab.
4. Select **Build Live OCR Stitcher APK** and click **Run workflow**, or push to `main`/`master`.
5. When the workflow finishes, open its run and download the `LiveOCRStitcher-debug-apk` artifact.
6. Extract the downloaded artifact on your phone and install `app-debug.apk`. You may need to allow installation from your browser or file manager.

This workflow builds a debug APK. It is not a Play Store release-signed APK. The build has not been run or verified in this environment.
