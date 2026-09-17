# My Application

一个基于 **Kotlin + Jetpack Compose** 构建的原生 Android 应用（Android Studio 默认「Empty Activity」模板项目）。应用启动后使用 Material 3 显示一句简单的问候语 `Hello Android!`。

## 功能特性

- 使用 Jetpack Compose 声明式 UI 编写界面
- Material 3 组件与主题（`Scaffold`、`MaterialTheme`）
- 支持深色 / 浅色主题，并在 Android 12+ 上启用动态取色（Material You）
- 边到边显示（`enableEdgeToEdge`）
- 使用 Gradle Version Catalog（`libs.versions.toml`）统一管理依赖

## 技术栈

| 类别 | 版本 |
| --- | --- |
| 语言 | Kotlin 2.2.10 |
| UI | Jetpack Compose (Material 3) |
| Compose BOM | 2026.02.01 |
| Android Gradle Plugin (AGP) | 9.3.0 |
| Gradle | 9.5.0 |
| compileSdk / targetSdk | 37 |
| minSdk | 24（Android 7.0） |
| Java | 11 |

## 环境要求

- Android Studio（支持 AGP 9.3.0 的最新稳定版）
- JDK 11 或更高版本
- Android SDK（`compileSdk 37` 已包含在 SDK 平台中）

> 项目使用 Gradle Wrapper，构建时会自动下载对应版本的 Gradle，无需手动安装。

## 构建与运行

### 使用 Android Studio（推荐）

1. 用 Android Studio 打开项目根目录（`D:\AndroidStudio_activity`）。
2. 等待 Gradle 同步完成。
3. 连接设备或启动模拟器，点击 **Run ▶** 即可编译并安装。

### 使用命令行

Windows：

```bash
# 编译 Debug APK
gradlew.bat assembleDebug

# 安装到已连接的设备/模拟器
gradlew.bat installDebug
```

macOS / Linux：

```bash
./gradlew assembleDebug
./gradlew installDebug
```

构建产物位于 `app/build/outputs/apk/debug/app-debug.apk`。

> 首次构建前，请确认 `local.properties` 中的 `sdk.dir` 指向本机 Android SDK 路径（例如 `sdk.dir=D:\\sdk`）。该文件由 Android Studio 自动生成，通常无需手动修改，也不应提交到版本库。

## 项目结构

```
.
├── app/                                # 应用主模块
│   ├── build.gradle.kts                # 模块构建脚本（依赖与 SDK 配置）
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml     # 应用清单
│       │   ├── java/com/fjnu/myapplication/
│       │   │   ├── MainActivity.kt     # 入口 Activity 与 Greeting 组件
│       │   │   └── ui/theme/           # 主题（Color / Theme / Type）
│       │   └── res/                    # 资源（图标、字符串、样式等）
│       ├── test/                       # 本地单元测试
│       └── androidTest/                # 仪器化测试
├── gradle/
│   ├── libs.versions.toml              # 依赖版本目录（Version Catalog）
│   └── wrapper/                        # Gradle Wrapper
├── build.gradle.kts                    # 项目级构建脚本
├── settings.gradle.kts                 # 项目设置
└── gradle.properties                   # Gradle 配置
```

## 核心代码说明

应用入口为 `MainActivity`，在 `setContent` 中使用 `MyApplicationTheme` 包裹 `Scaffold`，并调用 `Greeting("Android")` 在屏幕上渲染问候语：

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MyApplicationTheme {
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                    Greeting(
                        name = "Android",
                        modifier = Modifier.padding(innerPadding)
                    )
                }
            }
        }
    }
}
```

主题定义位于 `ui/theme/` 目录，包含浅色/深色配色方案，并在支持动态取色的设备上启用 Material You。

## 应用信息

| 项 | 值 |
| --- | --- |
| 应用名称 | My Application |
| 包名 / applicationId | `com.fjnu.myapplication` |
| 版本号 versionName | 1.0 |
| 版本代码 versionCode | 1 |
