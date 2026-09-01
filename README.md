KMP Project

A Kotlin Multiplatform (KMP) project that shares common business logic across multiple platforms while allowing platform-specific implementations where needed.

📱 Supported Platforms
Android
iOS
Desktop
Other platforms supported by Kotlin Multiplatform, as needed
🏗️ Project Structure
project/
├── composeApp/          # Shared UI and application code
├── iosApp/              # iOS application
├── shared/               # Shared Kotlin Multiplatform logic
│   └── src/
│       ├── commonMain/   # Code shared across all platforms
│       ├── commonTest/   # Shared tests
│       ├── androidMain/  # Android-specific implementation
│       └── iosMain/      # iOS-specific implementation
├── gradle/
├── build.gradle.kts
├── settings.gradle.kts
└── README.md

🚀 Getting Started
Prerequisites

Make sure you have:

Android Studio
Kotlin Multiplatform support
JDK 17 or later
Xcode for iOS development
Gradle
Clone the Project
git clone <repository-url>
cd <project-directory>

Run Android

Open the project in Android Studio and select the Android configuration.

Alternatively:

./gradlew :composeApp:assembleDebug


Install the generated APK on an emulator or physical device.

Run iOS

Open the iOS project in Xcode:

iosApp/iosApp.xcodeproj


Select an iOS simulator or connected device and run the application.

🔄 Kotlin Multiplatform Architecture

The project separates shared and platform-specific code.

commonMain

Contains code that can be used by all supported platforms:

class Greeting {
    fun message(): String = "Hello from Kotlin Multiplatform!"
}

Platform-Specific Code

When platform-specific functionality is required, use expect/actual:

// commonMain
expect class Platform {
    val name: String
}

// androidMain
actual class Platform {
    actual val name: String = "Android"
}

// iosMain
actual class Platform {
    actual val name: String = "iOS"
}

🧩 Technologies
Kotlin
Kotlin Multiplatform
Jetpack Compose / Compose Multiplatform
Gradle
Coroutines
Kotlin Serialization
Ktor
Android SDK
iOS / Swift
📦 Dependencies

Shared dependencies should generally be declared in the appropriate source set.

Example:

commonMain.dependencies {
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:<version>")
}


Platform-specific dependencies belong in their respective source sets:

androidMain.dependencies {
    implementation("...")
}

iosMain.dependencies {
    implementation("...")
}

🧪 Testing

Run all tests with:

./gradlew test


Shared tests should be placed in:

shared/src/commonTest/


Example:

class GreetingTest {

    @Test
    fun greetingIsCorrect() {
        assertEquals(
            "Hello from Kotlin Multiplatform!",
            Greeting().message()
        )
    }
}

🛠️ Build

Build the project using:

./gradlew build


For Android:

./gradlew :composeApp:assembleDebug


For a release build, configure the appropriate signing and distribution settings for each platform.

📐 Architecture

A recommended architecture is:

UI
 │
 ▼
ViewModel / Presentation
 │
 ▼
Use Cases
 │
 ▼
Repository
 │
 ├── Remote Data Source
 └── Local Data Source


Shared business logic should live in the KMP module whenever possible. Platform-specific code should only be introduced when a feature depends on platform APIs.

🔐 Configuration

Do not commit sensitive information such as:

API keys
Passwords
Signing credentials
Private certificates
Production secrets

Use environment variables, local configuration files, or an appropriate secrets-management solution.

🤝 Contributing
Create a new branch:
git checkout -b feature/my-feature

Make your changes.
Run tests:
./gradlew test

Verify the Android and iOS builds.
Commit your changes:
git commit -m "Add my feature"

Push the branch and create a pull request.
📄 License

Add the project's license information here.

📚 Useful Resources
Kotlin Multiplatform Documentation
Kotlin Documentation
Compose Multiplatform
Ktor
