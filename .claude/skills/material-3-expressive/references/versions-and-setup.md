# Versions and setup

## Check before writing code

Find `androidx.compose.material3` in `build.gradle(.kts)`, `libs.versions.toml` or the Compose BOM. Write down
the version and say it in the answer. Expressive availability depends on it and changes quickly. Confirm with
the official release notes: developer.android.com/jetpack/androidx/releases/compose-material3

## What is known (verify for the version in use)

| Version line | Expressive status |
|--------------|-------------------|
| 1.4.0 stable (Compose BOM 2025.12) | Community reports: most Expressive APIs are `internal`. `ShortNavigationBar` and `WideNavigationRail` are public. `ExperimentalMaterial3ExpressiveApi` is not visible, so the opt-in cannot be written. Official blog: 1.4 adds `HorizontalCenteredHeroCarousel`, `VerticalDragHandle`, `SecureTextField`, `TextFieldState`-based text fields |
| 1.5.0 alpha line | Expressive APIs are public. The official blog says they continue to be developed in the alpha releases. Reports say many became stable from alpha23, while some (for example `MaterialShapes`, `LoadingIndicator`, `ContainedLoadingIndicator`, `RoundedPolygon.toShape`) still needed an opt-in on later alphas |

Redundant `@OptIn` only gives an "unnecessary opt-in" warning, so it is safe to add where it resolves.

## Gradle (alpha line)

```kotlin
// libs.versions.toml: use the exact alpha the user's project allows
// androidx-compose-material3 = { module = "androidx.compose.material3:material3", version = "<1.5.0-alphaNN>" }
dependencies {
    implementation("androidx.compose.material3:material3:<version>")
    implementation("androidx.compose.material3:material3-window-size-class:<version>") // adaptive helpers
    implementation("androidx.graphics:graphics-shapes:<version>") // RoundedPolygon, Morph
}
```
Do not pin a version from memory. Ask the user or read their files. If they use the BOM, the alpha must be
set explicitly for material3, because the BOM maps to stable.

## Theme

```kotlin
@OptIn(ExperimentalMaterial3ExpressiveApi::class)
@Composable
fun AppTheme(darkTheme: Boolean = isSystemInDarkTheme(), content: @Composable () -> Unit) {
    val context = LocalContext.current
    val colors = when {
        Build.VERSION.SDK_INT >= 31 && darkTheme -> dynamicDarkColorScheme(context)
        Build.VERSION.SDK_INT >= 31 -> dynamicLightColorScheme(context)
        darkTheme -> darkColorScheme()
        else -> lightColorScheme()
    }
    MaterialExpressiveTheme(
        colorScheme = colors,
        motionScheme = MotionScheme.expressive(),
        content = content,
    )
}
```
Notes:
- Confirmed names in the official API index: `MaterialExpressiveTheme`, `MotionScheme`, `MaterialShapes`,
  `ExperimentalMaterial3ExpressiveApi`. Parameter lists can change between alphas; read the KDoc.
- Reports mention `expressiveLightColorScheme()` in newer versions. Confirm before using.
- Dynamic color (Android 12+) still applies. Provide a static fallback scheme for older devices.
- `MaterialTheme.motionScheme` gives the active `MotionScheme` inside the theme.

## Fallback decision

If the Expressive API is internal, missing, or the editor cannot resolve alpha artifacts: use `MaterialTheme`
with the same color roles, keep the component structure, and follow `references/code-patterns.md` section
"Without Expressive APIs". Tell the user which parts are stand-ins and which version unlocks the real ones.
