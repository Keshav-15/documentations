# Firebase Setup for Multiple Flavors in Flutter

This guide outlines the steps to configure a Flutter app for multiple flavors (Development, Production, Staging) with distinct Firebase configurations. It also addresses common issues encountered with `flutterfire`.

---

## Table of Contents

1. [Understanding Firebase Flavors](#1-understanding-firebase-flavors)
2. [Configuring Firebase for Multiple Flavors](#2-configuring-firebase-for-multiple-flavors)
   - [DEV Environment](#dev-environment)
   - [PROD Environment](#prod-environment)
   - [STAGE Environment](#stage-environment)
3. [Integrating Firebase in Xcode](#3-integrating-firebase-in-xcode)
4. [Troubleshooting Common Issues](#4-troubleshooting-common-issues)
5. [Summary](#5-summary)

---

## 1. Understanding Firebase Flavors

In Flutter, flavors allow you to maintain separate builds of your app for different environments like **Development**, **Production**, and **Staging**. Each environment requires its own Firebase configuration:

- **iOS**: `GoogleService-Info.plist`
- **Android**: Corresponding configuration file.

---

## 2. Configuring Firebase for Multiple Flavors

Use the `flutterfire` CLI to generate Firebase configuration files for each environment. Follow the commands below, replacing `com.application.bundleId` with your app's actual bundle ID.

### DEV Environment

```bash
flutterfire configure \
  --project=ukm-dev-a060a \
  --out=lib/firebase_options_dev.dart \
  --ios-bundle-id=com.application.bundleId-dev \
  --ios-out=ios/Runner/Firebase/dev/GoogleService-Info.plist \
  --android-app-id=com.application.bundleId.dev
```

### PROD Environment

```bash
flutterfire configure \
  --project=ukm-dev-a060a \
  --out=lib/firebase_options.dart \
  --ios-bundle-id=com.application.bundleId \
  --ios-out=ios/Runner/Firebase/prod/GoogleService-Info.plist \
  --android-app-id=com.application.bundleId
```

### STAGE Environment

```bash
flutterfire configure \
  --project=ukm-dev-a060a \
  --out=lib/firebase_options_stage.dart \
  --ios-bundle-id=com.application.bundleId-stage \
  --ios-out=ios/Runner/Firebase/stage/GoogleService-Info.plist \
  --android-app-id=com.application.bundleId.stage
```

> **Important:** Double-check that your bundle IDs match exactly as defined in your Firebase project settings.

---

## 3. Integrating Firebase in Xcode

After running the commands, add the Firebase configuration files to your Xcode project:

1. Open your project in Xcode.
2. Navigate to **File > Add Files to "Runner"**.
3. Select the `ios/Runner/Firebase` folder and include the generated `GoogleService-Info.plist` files for each flavor.

---

## 4. Troubleshooting Common Issues

### **Error: `flutterfire` not found**

If you encounter errors like `flutterfire bundle-service-file` or `flutterfire upload-crashlytics-symbols`, ensure the `flutterfire_cli` is properly activated.

#### Fix:

1. Add this line to your build script:
   ```bash
   dart pub global activate flutterfire_cli 0.3.0-dev.20 --overwrite
   ```
2. Example script:
   ```bash
   PATH=${PATH}:$FLUTTER_ROOT/bin:$HOME/.pub-cache/bin
   dart pub global activate flutterfire_cli 0.3.0-dev.20 --overwrite
   flutterfire bundle-service-file
   ```

---

## 5. Summary

By following this guide, you can successfully configure Firebase for multiple environments in your Flutter app. Key takeaways:

- Use distinct configuration files for each flavor.
- Always verify bundle IDs to avoid misconfigurations.
- Address common `flutterfire` issues by activating the CLI and updating scripts.

For further details, refer to:

- [Firebase Documentation](https://firebase.google.com/docs)
- [FlutterFire Documentation](https://firebase.flutter.dev/docs/overview)

---

## Highlights

- **Replace `com.application.bundleId`**: Always substitute with your app's actual bundle ID.
- **Double-check Configurations**: Ensure that files are added to the correct paths in Xcode.
- **Resolve Errors Promptly**: Follow the troubleshooting steps if issues arise.
