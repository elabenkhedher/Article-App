# 📖 Compose Article App

[![Kotlin](https://img.shields.io/badge/Kotlin-2.2.10-blue.svg?logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-BOM%202026.02.01-4285F4.svg?logo=android&logoColor=white)](https://developer.android.com/jetpack/compose)
[![Material 3](https://img.shields.io/badge/Material%203-Enabled-7B1FA2.svg?logo=materialdesign&logoColor=white)](https://m3.material.io)
[![Min SDK](https://img.shields.io/badge/Min%20SDK-24%20(Nougat)-brightgreen.svg)](https://developer.android.com)
[![Target SDK](https://img.shields.io/badge/Target%20SDK-37-orange.svg)](https://developer.android.com)
[![License](https://img.shields.io/badge/License-Apache%202.0-lightgrey.svg)](LICENSE)

A modern Android application developed as part of Google's **Android Basics with Compose** curriculum. The app showcases declarative UI development with Jetpack Compose by presenting a clean, beautifully formatted tutorial article about Jetpack Compose itself.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [UI Layout & Anatomy](#-ui-layout--anatomy)
- [Key Features](#-key-features)
- [Tech Stack & Architecture](#-tech-stack--architecture)
- [Project Structure](#-project-structure)
- [Deep Dive: Composable Implementation](#-deep-dive-composable-implementation)
- [Prerequisites & Getting Started](#-prerequisites--getting-started)
- [Building & Testing](#-building--testing)
- [Key Concepts Learned](#-key-concepts-learned)
- [Author & Acknowledgments](#-author--acknowledgments)

---

## 🌟 Overview

The **Article App** demonstrates the core fundamentals of building native user interfaces on Android using **Jetpack Compose** and **Material Design 3**.

Instead of traditional XML layouts, the application uses declarative Kotlin functions to define visual components and their layout hierarchies. It highlights how Compose simplifies UI construction through modular composables, modifier chains, responsive padding, and adaptive theming.

---

## 🎨 UI Layout & Anatomy

The screen is arranged as a single cohesive article layout within a vertical `Column`:

```
+---------------------------------------------------+
|                                                   |
|           [ Header Banner Image ]                 |
|             (fillMaxWidth, nodpi)                 |
|                                                   |
+---------------------------------------------------+
|  Jetpack Compose tutorial                         |  <- Title (24sp, 16dp padding)
+---------------------------------------------------+
|  Jetpack Compose is a modern toolkit for          |  <- Lead Summary
|  building native Android UI. Compose simplifies   |     (16dp start & end padding,
|  and accelerates UI development on Android with   |      TextAlign.Justify)
|  less code, powerful tools, and intuitive...      |
+---------------------------------------------------+
|  In this tutorial, you build a simple UI          |  <- Body Content
|  component with declarative functions. You call   |     (16dp all-around padding,
|  Compose functions to say what elements you want  |      TextAlign.Justify)
|  and the Compose compiler does the rest...        |
+---------------------------------------------------+
```

### Banner Asset
The banner graphic illustrates Compose components and is located at:
`app/src/main/res/drawable-nodpi/bg_compose_background.png`

---

## ✨ Key Features

- **100% Declarative UI**: Crafted entirely with Jetpack Compose composable functions—no XML layouts.
- **Material Design 3 (M3)**: Built with the latest Material 3 styling components, type scales, and color schemes.
- **Dynamic Color Support**: Seamlessly utilizes Material You dynamic theming on Android 12+ (API level 31+), with graceful fallback to custom light and dark color schemes on older Android versions.
- **Modern Edge-to-Edge Design**: Integrates `enableEdgeToEdge()` for an immersive full-screen presentation beneath system bars.
- **Precise Typography & Alignment**: Utilizes `TextAlign.Justify` and proportional typographic scale (`24.sp` heading, structured body text).
- **Interactive Tooling & Preview**: Includes `@Preview` annotations for immediate visual layout inspection inside Android Studio without running an emulator.
- **Gradle Version Catalog**: Dependency management organized through `gradle/libs.versions.toml`.

---

## 🛠️ Tech Stack & Architecture

| Layer / Tool | Technology | Purpose |
| :--- | :--- | :--- |
| **Language** | [Kotlin 2.2.10](https://kotlinlang.org/) | Modern, concise language for Android development |
| **UI Toolkit** | [Jetpack Compose (BOM 2026.02.01)](https://developer.android.com/jetpack/compose) | Declarative UI framework |
| **Design System** | [Material 3 (M3)](https://m3.material.io/) | Next-generation Material Design components |
| **Activity Architecture** | `ComponentActivity` + Compose `setContent` | Single-activity Compose host |
| **Build System** | Gradle (Kotlin DSL `.kts`) + AGP 9.4.1 | Automated build pipeline and dependency catalog |
| **Min SDK** | API 24 (Android 7.0 Nougat) | Wide device compatibility |
| **Target / Compile SDK** | API 37 | Modern Android capabilities and platform optimizations |

---

## 📂 Project Structure

```text
Article/
├── app/
│   ├── build.gradle.kts                # App-level build configuration & dependencies
│   ├── src/
│   │   ├── androidTest/                # Instrumented UI tests
│   │   ├── test/                       # Local unit tests
│   │   └── main/
│   │       ├── AndroidManifest.xml     # Application manifest & activity declaration
│   │       ├── java/com/example/article/
│   │       │   ├── MainActivity.kt     # Main entry point & Article composables
│   │       │   └── ui/theme/
│   │       │       ├── Color.kt        # Color definitions (Light & Dark palettes)
│   │       │       ├── Theme.kt        # MaterialTheme configuration & dynamic color
│   │       │       └── Type.kt         # Typography configurations
│   │       └── res/
│   │           ├── drawable/           # App launcher vector backgrounds
│   │           ├── drawable-nodpi/     # Header image (bg_compose_background.png)
│   │           └── values/             # App name and resource definitions
├── gradle/
│   ├── libs.versions.toml              # Version catalog for dependencies and plugins
│   └── wrapper/                        # Gradle wrapper files
├── build.gradle.kts                    # Root build script
├── settings.gradle.kts                 # Project repository settings
└── README.md                           # Documentation
```

---

## 🔍 Deep Dive: Composable Implementation

The central UI component is `Article()`, defined in [`MainActivity.kt`](app/src/main/java/com/example/article/MainActivity.kt):

```kotlin
@Composable
fun Article(modifier: Modifier = Modifier) {
    Column {
        Image(
            painter = painterResource(id = R.drawable.bg_compose_background),
            contentDescription = null,
            modifier = Modifier.fillMaxWidth()
        )
        Text(
            text = "Jetpack Compose tutorial",
            fontSize = 24.sp,
            modifier = Modifier.padding(16.dp)
        )
        Text(
            text = "Jetpack Compose is a modern toolkit for building native Android UI...",
            modifier = Modifier.padding(start = 16.dp, end = 16.dp),
            textAlign = TextAlign.Justify
        )
        Text(
            text = "In this tutorial, you build a simple UI component with declarative functions...",
            modifier = Modifier.padding(16.dp),
            textAlign = TextAlign.Justify
        )
    }
}
```

### Why this design matters:
- **Composable Decomposition**: Components are assembled declaratively; properties describe *how* it should look rather than imperative mutation steps.
- **Modifier Ordering & Scoping**: Demonstrates fine-grained control over layout margins and padding (`Modifier.padding(16.dp)` vs `Modifier.padding(start = 16.dp, end = 16.dp)`).
- **Resource Loading**: Uses `painterResource()` for zero-friction resource bundling from drawable directories.

---

## 🚀 Prerequisites & Getting Started

### Prerequisites
- **Android Studio**: Ladybug (2024.2.1+) or newer recommended.
- **JDK**: Java Development Kit 11 or higher.
- **Android SDK**: API level 37 installed via SDK Manager.

### Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/elabenkhedher/Article-App-Android-Google-Course.git
   cd Article-App-Android-Google-Course
   ```

2. **Open in Android Studio**
   - Launch Android Studio.
   - Select **Open**, navigate to the cloned folder, and click **OK**.
   - Wait for Gradle sync to complete and download required dependencies.

3. **Run on Device or Emulator**
   - Select an Android Virtual Device (AVD) running API 24 or newer.
   - Click the green **Run** button (`Shift + F10`) or choose **Run 'app'**.

---

## 🏗️ Building & Testing

You can build and test the project via the Gradle wrapper from the terminal:

- **Build Debug APK**:
  ```bash
  ./gradlew assembleDebug
  ```
  The generated APK will be available at `app/build/outputs/apk/debug/app-debug.apk`.

- **Run Unit Tests**:
  ```bash
  ./gradlew test
  ```

- **Run Instrumented Android Tests**:
  ```bash
  ./gradlew connectedAndroidTest
  ```

- **Lint / Code Analysis**:
  ```bash
  ./gradlew lint
  ```

---

## 📚 Key Concepts Learned

This project reinforces several essential Android Jetpack Compose fundamentals:
1. **The Declarative Paradigm**: Defining UI as a function of state and structure rather than manipulating view hierarchies directly.
2. **Standard Layout Composables**: Positioning children vertically with `Column` and managing spacing using `Modifier`.
3. **Typography & Styling**: Applying font sizes (`sp`), text justification (`TextAlign.Justify`), and standard Material theme styling.
4. **Static Asset Rendering**: Loading raster images into Compose using `Image` and `painterResource`.
5. **Modern Android Tooling**: Managing project dependencies with Gradle Version Catalogs (`libs.versions.toml`).

---

## 👨‍💻 Author & Acknowledgments

- **Developer**: [elabenkhedher](https://github.com/elabenkhedher) (Ela Ben Khedher)
- **Course**: [Android Basics with Compose](https://developer.android.com/courses/android-basics-compose/course) by Google Developers Training.

---

## 📄 License

This project is open-source and created for educational purposes as part of the Google Android Basics with Compose learning pathway.
