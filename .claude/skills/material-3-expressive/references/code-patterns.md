# Code patterns

Compile-check these against the user's version; API shapes shift between alphas.

## Expressive toggle button group (alpha line)

```kotlin
@OptIn(ExperimentalMaterial3ExpressiveApi::class)
@Composable
fun SortToggle(options: List<String>, selected: Int, onSelect: (Int) -> Unit) {
    Row(horizontalArrangement = Arrangement.spacedBy(ButtonGroupDefaults.ConnectedSpaceBetween)) {
        options.forEachIndexed { i, label ->
            ToggleButton(
                checked = selected == i,
                onCheckedChange = { onSelect(i) },
                shapes = ToggleButtonDefaults.shapes(),
            ) { Text(label) }
        }
    }
}
```
If `ButtonGroupDefaults.ConnectedSpaceBetween` or `ToggleButtonDefaults.shapes()` is unresolved, check the KDoc
for the exact name in your version, or use the fallback below.

## Loading and progress

```kotlin
@OptIn(ExperimentalMaterial3ExpressiveApi::class)
@Composable
fun Loading(progress: Float?) {
    if (progress == null) LoadingIndicator()
    else LinearWavyProgressIndicator(progress = { progress })
}
```

## Without Expressive APIs (fallback)

Use stable `MaterialTheme`, keep the same roles, and add the expressive behaviour by hand.

Shape change on press:
```kotlin
@Composable
fun PressShapeButton(onClick: () -> Unit, content: @Composable RowScope.() -> Unit) {
    val source = remember { MutableInteractionSource() }
    val pressed by source.collectIsPressedAsState()
    val corner by animateDpAsState(if (pressed) 12.dp else 28.dp, spring(0.6f, 800f), label = "corner")
    val scale by animateFloatAsState(if (pressed) 0.96f else 1f, spring(0.6f, 800f), label = "scale")
    Button(
        onClick = onClick,
        interactionSource = source,
        shape = RoundedCornerShape(corner),
        modifier = Modifier.graphicsLayer { scaleX = scale; scaleY = scale },
        content = content,
    )
}
```
Stable stand-ins:
- `ShortNavigationBar` missing: `NavigationBar` with items that keep labels.
- `ButtonGroup`: `Row` of `ToggleButton`-like `FilledTonalButton`s with `RoundedCornerShape` that rounds only outer ends.
- Wavy or loading indicator: `CircularProgressIndicator` / `LinearProgressIndicator`.
- FAB menu: `FloatingActionButton` plus an `AnimatedVisibility` column of small FABs.
- Shapes: `RoundedCornerShape(n.dp)` with the corner scale in `shape-and-morphing.md`; `GenericShape` for custom paths.
Add a comment on each stand-in naming the Expressive component it replaces.

## Code rules

- Hoist state; components take `value` and `onValueChange`.
- `Modifier` is the first optional parameter, applied to the root.
- No hard-coded colors, no raw `dp` for text. Use theme tokens.
- One `@OptIn` per function that needs it, not file-wide, when practical.
- `remember` heavy objects (Morph, Path); never allocate in draw lambdas.
- Never fake a Material component with absolutely positioned boxes. Use real components or real layouts.
- Previews: `@Preview` with light and dark, and a large font scale.
