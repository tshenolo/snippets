# Capacitor Cheatsheet

Capacitor is an open-source native runtime for building Web Native apps. It allows you to create cross-platform iOS, Android, and Progressive Web Apps with JavaScript, HTML, and CSS.

## Core Concepts

*   **Web Native**: Build apps using standard web technologies that run natively on mobile platforms.
*   **Native Bridge**: Facilitates communication between your web code (JavaScript) and native platform code (Swift/Objective-C for iOS, Java/Kotlin for Android).
*   **Plugins**: Access native device features (Camera, Geolocation, Filesystem, Haptics, etc.) through a consistent JavaScript API. Capacitor provides core plugins, and there's a rich ecosystem of community plugins.
*   **Progressive Web App (PWA) Support**: Capacitor can also deploy your web app as a PWA.
*   **Native Project Management**: You have full control over the native iOS (Xcode) and Android (Android Studio) projects.

## Setup and Project Initialization

1.  **Install Capacitor CLI globally (optional but can be useful)**:
    ```bash
    npm install -g @capacitor/cli
    # or
    # yarn global add @capacitor/cli
    ```
2.  **Add Capacitor to an existing web project**:
    *   Navigate to your web project's root directory.
    *   Install Capacitor core and CLI as dev dependencies:
        ```bash
        npm install @capacitor/core @capacitor/cli --save-dev
        # or
        # yarn add @capacitor/core @capacitor/cli --dev
        ```
    *   Initialize Capacitor in your project:
        ```bash
        npx cap init [appName] [appId] --web-dir=<your_web_build_directory>
        # Example:
        # npx cap init "My Awesome App" "com.example.myawesomeapp" --web-dir=dist
        # npx cap init "MyApp" "io.ionic.starter" --web-dir=www # For Ionic projects
        ```
        *   `appName`: Your application's name.
        *   `appId`: Your application's unique bundle ID / package name (e.g., `com.company.appname`).
        *   `--web-dir`: The directory containing your compiled web assets (e.g., `build`, `dist`, `www`).

## Adding Native Platforms

*   **Add iOS platform**:
    ```bash
    npx cap add ios
    # This creates an 'ios' directory with an Xcode project.
    ```
*   **Add Android platform**:
    ```bash
    npx cap add android
    # This creates an 'android' directory with an Android Studio project.
    ```
*   **Add Electron platform (for desktop apps)**:
    ```bash
    npm install @capacitor/electron
    npx cap add @capacitor/electron
    # or npx cap add electron
    ```

## Core Workflow

1.  **Build Your Web App**: Compile your web application assets.
    ```bash
    npm run build # Or your project's specific build command (e.g., ionic build, ng build)
    ```
2.  **Sync Web Assets to Native Platforms**: Copies your web build (`web-dir`) to the native projects and updates configuration.
    ```bash
    npx cap sync
    # Or for a specific platform:
    # npx cap sync ios
    # npx cap sync android
    ```
    *   `sync` essentially runs `npx cap copy` followed by `npx cap update`.
3.  **Copy Web Assets**: Only copies the web assets.
    ```bash
    npx cap copy
    ```
4.  **Update Native Platforms**: Updates native dependencies and configuration.
    ```bash
    npx cap update
    # npx cap update ios
    # npx cap update android
    ```
5.  **Open Native IDE**:
    *   Open iOS project in Xcode:
        ```bash
        npx cap open ios
        ```
    *   Open Android project in Android Studio:
        ```bash
        npx cap open android
        ```
    *   Open Electron project:
        ```bash
        npx cap open electron
        ```
6.  **Run on Device/Emulator (from Native IDE)**:
    *   **Xcode**: Select your target device or simulator and click the "Play" button.
    *   **Android Studio**: Select your target device or emulator and click the "Run" button.
    *   **Electron**:
        ```bash
        npx cap run electron # Or from IDE
        ```

## Using Capacitor Plugins (JavaScript API)

Capacitor plugins provide a JavaScript interface to native device functionality.

*   **Install a Core or Community Plugin**:
    ```bash
    npm install @capacitor/camera # Example: Camera plugin
    # For community plugins, e.g.:
    # npm install some-community-plugin
    ```
*   **Sync after installing plugins**:
    ```bash
    npx cap sync
    ```
*   **Using a Plugin in your JavaScript/TypeScript**:
    ```typescript
    // Example: Using the Camera plugin
    import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';

    const takePicture = async () => {
      try {
        const image = await Camera.getPhoto({
          quality: 90,
          allowEditing: false, // or true
          resultType: CameraResultType.Uri, // Or Base64, DataUrl
          source: CameraSource.Camera // Or Photos, Prompt
        });

        // image.webPath will contain a path that can be set as an image src.
        // To get the base64 representation, use resultType: CameraResultType.Base64
        // const imageUrl = image.webPath;
        // console.log('Image URI:', imageUrl);
        // If resultType is Base64:
        // const base64Image = `data:image/jpeg;base64,${image.base64String}`;

      } catch (error) {
        console.error('Error taking picture:', error);
      }
    };

    // Example: Using the Geolocation plugin
    import { Geolocation } from '@capacitor/geolocation';

    const getCurrentPosition = async () => {
      try {
        const coordinates = await Geolocation.getCurrentPosition({
          enableHighAccuracy: true,
          timeout: 10000 // milliseconds
        });
        console.log('Current position:', coordinates.coords.latitude, coordinates.coords.longitude);
      } catch (error) {
        console.error('Error getting location', error);
      }
    };

    // Example: Using the Haptics plugin
    import { Haptics, ImpactStyle } from '@capacitor/haptics';

    const triggerHapticFeedback = async () => {
      await Haptics.impact({ style: ImpactStyle.Medium }); // Light, Medium, Heavy
      // Or trigger a vibration pattern
      // await Haptics.vibrate();
    };

    // Example: Using the Storage plugin (simple key-value store)
    import { Storage } from '@capacitor/storage';

    const setItem = async (key, value) => {
      await Storage.set({ key: key, value: JSON.stringify(value) });
    };
    const getItem = async (key) => {
      const { value } = await Storage.get({ key: key });
      return value ? JSON.parse(value) : null;
    };
    const removeItem = async (key) => {
      await Storage.remove({ key: key });
    };
    ```
*   **Permissions (Android)**: Some plugins require specific permissions to be declared in `AndroidManifest.xml`. Capacitor often handles common ones, but check plugin documentation.
    ```xml
    <!-- Example: android/app/src/main/AndroidManifest.xml -->
    <!-- <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/> -->
    <!-- <uses-feature android:name="android.hardware.location.gps"/> -->
    ```
*   **Permissions (iOS)**: Usage descriptions for permissions must be added to `Info.plist`.
    ```xml
    <!-- Example: ios/App/App/Info.plist -->
    <!-- <key>NSCameraUsageDescription</key>
         <string>To take photos for your profile.</string>
         <key>NSPhotoLibraryUsageDescription</key>
         <string>To select photos for your profile.</string>
         <key>NSLocationWhenInUseUsageDescription</key>
         <string>To show your location on a map.</string> -->
    ```

## Configuration (`capacitor.config.json` or `capacitor.config.ts`)

Located at the root of your project.
```json
{
  "appId": "com.example.myapp",
  "appName": "My Capacitor App",
  "webDir": "www", // Or "dist", "build", etc.
  "bundledWebRuntime": false, // Set to true for production builds to bundle runtime
  "npmClient": "npm", // Or "yarn"
  "plugins": {
    "SplashScreen": {
      "launchShowDuration": 3000,
      "launchAutoHide": true,
      "backgroundColor": "#ffffffff",
      "androidSplashResourceName": "splash",
      "androidScaleType": "CENTER_CROP",
      "showSpinner": true,
      "androidSpinnerStyle": "large",
      "iosSpinnerStyle": "small",
      "spinnerColor": "#999999"
    },
    "PushNotifications": { // Example for Push Notifications plugin
      "presentationOptions": ["badge", "sound", "alert"]
    }
    // Other plugin-specific configurations
  },
  "cordova": {} // For Cordova plugin compatibility if needed
}
```
*   For TypeScript configuration (`capacitor.config.ts`):
    ```typescript
    // import { CapacitorConfig } from '@capacitor/cli';
    // const config: CapacitorConfig = {
    //   appId: 'com.example.myapp',
    //   appName: 'My Capacitor App TS',
    //   webDir: 'dist',
    //   // ... other options
    // };
    // export default config;
    ```

## Native Project Configuration

*   **iOS**: Modify settings in `ios/App/App/Info.plist` (e.g., permissions, display name) and via Xcode project settings.
*   **Android**: Modify settings in `android/app/src/main/AndroidManifest.xml` (permissions, activities), `build.gradle` files (dependencies, versions), and `res/` directory (icons, styles).

## Creating Custom Native Plugins

If existing plugins don't cover your needs, you can create your own.
1.  Generate plugin template:
    ```bash
    npx @capacitor/cli plugin:generate
    ```
2.  Implement native code (Swift/Obj-C for iOS, Java/Kotlin for Android) and the JavaScript bridge.
    *   Refer to official Capacitor documentation for detailed plugin development guides.

## Capacitor CLI Commands Summary

*   `npx cap init [appName] [appId] --web-dir=<dir>`: Initialize Capacitor.
*   `npx cap add <platform>`: Add native platform (ios, android, electron).
*   `npx cap sync [platform]`: Sync web assets and update native projects.
*   `npx cap copy [platform]`: Copy web assets to native projects.
*   `npx cap update [platform]`: Update native dependencies and configuration.
*   `npx cap open <platform>`: Open native project in IDE.
*   `npx cap run <platform> [options]`: Build and run on device/emulator (can also use IDE).
    ```bash
    # npx cap run android --list # List available targets
    # npx cap run android --target <emulator_id>
    # npx cap run ios --livereload --external --port=8100 # Live reload with external server
    ```
*   `npx cap ls`: List installed plugins.
*   `npx cap doctor [platform]`: Checks for common issues in your Capacitor setup.

## Live Reload / Development Workflow

During development, you often run your web app's dev server (e.g., `npm run start` for React, `npm run dev` for Vite/Vue). Capacitor can point to this server.

1.  Start your web app's dev server (e.g., `http://localhost:3000`).
2.  Update `capacitor.config.json` (or `.ts`) to point to your dev server:
    ```json
    {
      // ... other config
      "server": {
        "url": "http://localhost:3000", // Your web dev server URL
        "cleartext": true // If using http and not https on Android for dev
      }
    }
    ```
3.  Run on device/emulator with live reload:
    ```bash
    npx cap run android --livereload --external
    # or
    # npx cap run ios --livereload --external
    ```
    *   `--livereload` (or `-l`): Enables live reload.
    *   `--external`: Uses an external IP for the dev server so the device can access it.

This provides a good overview and actionable commands for Capacitor. I'll proceed with `peoplesoft_ib.md`.The `capacitor.md` cheatsheet has been successfully updated with detailed command examples for the Capacitor CLI, plugin usage (Camera, Geolocation, Haptics, Storage), configuration, and development workflow including live reload.

Next, I will enhance `peoplesoft_ib.md`. This will be more conceptual due to its nature, but I'll aim to include key terminology, typical message structures (e.g., rowset-based XML), common PeopleCode event handlers used in IB, and typical configuration points within PIA, illustrated with pseudocode or XML snippets where appropriate.
