# 🪄 Magic Eraser Android SDK

![JitPack](https://img.shields.io/jitpack/version/com.github.nsenterprise9865-stack/magic-eraser-android-sdk)
![Platform](https://img.shields.io/badge/platform-Android-green.svg)
![API](https://img.shields.io/badge/API-24%2B-blue.svg)

Bring powerful, fully offline AI image erasing to your Android application. 

The Magic Eraser SDK provides state-of-the-art on-device ML segmentation, text recognition, and LaMa inpainting so your users can remove unwanted objects and text from photos instantly, without sending their private images to the cloud.

---

## 🌟 Features

*   **100% On-Device Processing:** Zero cloud API costs, total user privacy.
*   **Smart Object Selection:** Tap objects/subjects to automatically mask them with ML Kit.
*   **Text Erasing:** One-tap text detection and removal via ML Kit OCR.
*   **Advanced Inpainting:** High-quality background reconstruction using LaMa.
*   **Manual Brushing & History:** Custom brush sizes with full Undo/Redo stack support.
*   **Ready-to-Use UI:** A polished, gesture-ready Jetpack Compose editor screen.

---

## 📦 Installation

The SDK is distributed securely via JitPack. 

### Step 1: Add the JitPack repository
Add it in your root `settings.gradle` or root `build.gradle` at the end of repositories:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

### Step 2: Add the dependency
In your app-level `build.gradle`:

```gradle
dependencies {
    implementation 'com.github.nsenterprise9865-stack:magic-eraser-android-sdk:1.0.3'
}
```

---

## 🚀 Quick Start

### 1. Initialization (License Key Required)
You must initialize the SDK with your unique License Key before using any features. This validates your subscription and enables the SDK features.

```kotlin
import com.nsenterprise.magiceraser.sdk.MagicEraserSDK

class YourApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        
        // Initialize the SDK with your unique license key
        MagicEraserSDK.initialize(this, "YOUR_LICENSE_KEY_HERE")
    }
}
```

### 2. Launching the Editor
The SDK uses Jetpack Compose and is designed to integrate flawlessly into your existing UI. You control the photo selection (e.g., using the modern Android Photo Picker) and pass the `Uri` to the SDK:

```kotlin
// Example launching the SDK editor after a user picks a photo
if (selectedImageUri != null) {
    MagicEraserScreen(
        onBack = { 
            selectedImageUri = null // Close the editor
        },
        initialImageUri = selectedImageUri
    )
}
```

---

## 💰 Pricing & Licensing

Our SDK uses a fair, flat-rate pricing model compared to expensive pay-per-image cloud APIs. Because everything runs on-device, you pay a predictable monthly or yearly fee regardless of how many images your users edit.

*   **Indie Plan:** $19 / month (or $149 / year) - Best for solo developers.
*   **Pro Plan:** $49 / month (or $399 / year) - Best for startups and teams.
*   **Enterprise:** Custom tailored for large-scale applications.

To purchase a license key or view full details, please contact **nsenterprise9865@gmail.com**.

---
*© 2026 NS Enterprise. All rights reserved.*
