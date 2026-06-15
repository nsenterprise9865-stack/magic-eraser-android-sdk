# 🪄 Magic Eraser Android SDK

![JitPack](https://img.shields.io/jitpack/version/com.github.nsenterprise9865-stack/magic-eraser-android-sdk)
![Platform](https://img.shields.io/badge/platform-Android-green.svg)
![API](https://img.shields.io/badge/API-24%2B-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.9-brightgreen.svg)

Bring powerful, fully offline AI image erasing to your Android application.

The Magic Eraser SDK provides state-of-the-art on-device ML segmentation, text recognition, LaMa inpainting, and EdgeSAM smart detection so your users can remove unwanted objects and text from photos instantly — without sending their private images to the cloud.

---

## 🌟 Features

*   **100% On-Device Processing:** Zero cloud API costs, total user privacy.
*   **EdgeSAM Smart Detection:** Tap any object for pixel-perfect AI segmentation (v1.0.9).
*   **Dual AI Inpainting Modes:** Fast (MIGAN v2) and Deep AI (LaMa) — user-selectable.
*   **Smart Object Selection:** ML Kit subject segmentation with color flood-fill fallback.
*   **Text Erasing:** One-tap text detection and removal via ML Kit OCR.
*   **Manual Brushing & Lasso:** Custom brush sizes + freehand polygon selection.
*   **Full Undo/Redo Stack:** Up to 15 history steps.
*   **Ready-to-Use UI:** Polished Jetpack Compose editor screen.
*   **Headless / Custom UI API:** Full control via `MagicEraserCore` — no SDK screens needed.

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
    implementation 'com.github.nsenterprise9865-stack:magic-eraser-android-sdk:1.0.9'
}
```

---

## 🚀 Quick Start

### 1. Initialization (License Key Required)
Initialize the SDK once — typically in `Application.onCreate()`.

```kotlin
import com.nsenterprise.magiceraser.sdk.MagicEraserSDK

class YourApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        lifecycleScope.launch(Dispatchers.IO) {
            MagicEraserSDK.initialize(this@YourApplication, "YOUR_LICENSE_KEY_HERE")
        }
    }
}
```

### 2. Built-in Editor Screen (Jetpack Compose)
Pass a photo `Uri` and the SDK handles everything:

```kotlin
MagicEraserScreen(
    onBack        = { /* close editor */ },
    initialImageUri = selectedImageUri,
    onSaveSuccess = { resultBitmap -> /* do something with result */ }
)
```

---

## 🎨 Custom UI / Headless API

For full control over branding and UX, use `MagicEraserCore` directly — no SDK activities or screens are launched.

### Brush Erase
```kotlin
val result: Bitmap = MagicEraserCore.eraseWithBrush(
    context      = context,
    source       = myBitmap,
    points       = brushPoints,       // List<PointF> in image coordinates
    brushSize    = 40f,
    accurateMode = true,              // true = LaMa (Deep AI), false = MIGAN v2 (Fast)
    onProgress   = { p -> /* 0.0 → 1.0 */ }
)
```

### Lasso Erase
```kotlin
val result: Bitmap = MagicEraserCore.eraseWithLasso(
    context      = context,
    source       = myBitmap,
    lassoPoints  = polygonPoints,
    accurateMode = true,
    onProgress   = { p -> }
)
```

### EdgeSAM Smart Detect (v1.0.9)
Tap any object for pixel-perfect AI segmentation:

```kotlin
// Step 1 — Pre-warm the EdgeSAM encoder when entering Detect mode
// (do this once per image; subsequent taps are instant)
MagicEraserCore.prepareForDetect(context, sourceBitmap)

// Step 2 — On user tap, get the (mask, highlight) pair
val maskPair: Pair<Bitmap, Bitmap>? = MagicEraserCore.buildDetectMask(
    context = context,
    source  = sourceBitmap,
    tapX    = imgX,   // image coordinates
    tapY    = imgY
)

// Step 3 — Apply the mask to erase
if (maskPair != null) {
    val result = MagicEraserCore.applyMask(
        context      = context,
        source       = sourceBitmap,
        mask         = maskPair.first,
        accurateMode = true
    )
}
```

> **Detection pipeline:** EdgeSAM (on-device encoder/decoder) → MLKit Subject Segmentation → Color Flood-Fill fallback. All three tiers run automatically — your code stays the same.

### AI Inpainting Modes
| Mode | `accurateMode` | Model | Quality |
|---|---|---|---|
| **Fast** | `false` | MIGAN v2 | ⚡ Faster |
| **Deep AI** | `true` | LaMa | 🎯 Highest quality |

---

## 📋 Changelog

### v1.0.9 — 2026-06-15
- ✅ **EdgeSAM Smart Detect** exposed to the Headless API via `MagicEraserCore.prepareForDetect()` and upgraded `buildDetectMask()` — custom UIs now use the same 3-tier detection pipeline as the built-in screen
- ✅ Custom editor sample app updated to pre-warm EdgeSAM on Detect mode switch
- ✅ Compiler fix: `SamHelper` import added to `MagicEraserCore`

### v1.0.8 — 2026-06-12
- ✅ MIGAN v2 Fast AI inpainting mode added
- ✅ EdgeSAM encoder/decoder integrated into built-in SDK screen
- ✅ Accumulative multi-tap detection with Undo/Redo

### v1.0.7
- ✅ Headless API (`MagicEraserCore`) introduced
- ✅ Custom UI sample app added

---

## 💰 Pricing & Licensing

Our SDK uses a fair, flat-rate pricing model. Everything runs on-device — no per-image fees.

*   **Indie Plan:** $19 / month (or $149 / year) — Solo developers.
*   **Pro Plan:** $49 / month (or $399 / year) — Startups and teams.
*   **Enterprise:** Custom pricing for large-scale applications.

To purchase a license key: **contact.nsenterprise@gmail.com**

---
*© 2026 NS Enterprise. All rights reserved.*
