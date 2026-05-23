# Magic Eraser SDK
Welcome to the Magic Eraser SDK distribution repository.

## Installation

Add it in your root `build.gradle` at the end of repositories:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

Step 2. Add the dependency

```gradle
dependencies {
    implementation 'com.github.nsenterprise9865-stack:magic-eraser-android-sdk:1.0.3'
}
```

## Initialization

You must initialize the SDK with your unique License Key before using any features. This requires an internet connection for validation.

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

## Documentation
Please refer to the official documentation provided to you upon purchase for detailed instructions on launching the UI and using the SDK features.
