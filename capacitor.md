# Capacitor Cheatsheet

*   **Purpose**: Cross-platform native runtime for web apps (alternative to Cordova). Allows web apps to run as native iOS, Android, and PWA.
*   **Core Concepts**:
    *   Web View: Renders your web application.
    *   Native Bridge: Communication between web code and native code.
    *   Plugins: Access native device features (Camera, Geolocation, Filesystem, etc.).
*   **Setup**:
    *   Install: `npm install @capacitor/core @capacitor/cli`.
    *   Initialize: `npx cap init [appName] [appId] --web-dir=www` (or your web app's build directory).
    *   Add Platforms: `npx cap add ios`, `npx cap add android`.
*   **Workflow**:
    1.  Build your web app (e.g., `npm run build`).
    2.  Sync web assets to native platforms: `npx cap sync` (copies web dir, updates config).
    3.  Open native IDE: `npx cap open ios`, `npx cap open android`.
    4.  Build and run from native IDE (Xcode for iOS, Android Studio for Android).
*   **Plugins**:
    *   Core Plugins: Bundled with Capacitor (e.g., `App`, `SplashScreen`, `StatusBar`, `Keyboard`, `Geolocation`).
    *   Community/Custom Plugins.
    *   Usage (JavaScript/TypeScript):
        ```typescript
        import { Camera, CameraResultType } from '@capacitor/camera';
        const takePicture = async () => {
          const image = await Camera.getPhoto({
            quality: 90,
            allowEditing: true,
            resultType: CameraResultType.Uri
          });
        };
        ```
*   **Configuration (`capacitor.config.json` or `.ts`)**: App ID, app name, web directory, plugin preferences.
*   **Native API Access**: Use plugins or create custom native code.
*   **Deployment**: Build native binaries through Xcode (IPA for iOS) and Android Studio (APK/AAB for Android). PWAs are deployed like any web app.
*   **Updating**: `npx cap update` (updates native dependencies).
