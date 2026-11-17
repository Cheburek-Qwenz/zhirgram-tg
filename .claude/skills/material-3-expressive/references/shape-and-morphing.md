# Shape and morphing

## Corner scale

M3 corner tokens: none 0, extra small 4, small 8, medium 12, large 16, extra large 28, full (pill/circle).
Expressive adds: large increased 20, extra large increased 32, extra extra large 48. In Compose these appear
as `Shapes.largeIncreased`, `Shapes.extraLargeIncreased`, `Shapes.extraExtraLarge` (reported internal in 1.4.0,
public in the alpha line; verify).

Rules:
- Pick radius by element size. Small controls use small radius, big containers use large or increased radius.
- Nested shapes: inner radius = outer radius minus the gap, so corners stay concentric.
- Do not make every element the same rounded rectangle. Vary shape with purpose.

## MaterialShapes

`MaterialShapes` is a library of about 35 decorative `RoundedPolygon` shapes: circle, square, slanted, arch,
fan, arrow, semicircle, oval, pill, triangle, diamond, clam shell, pentagon, gem, sunny, very sunny, cookie
(4, 6, 7, 9, 12 sided), clover (4, 8 leaf), burst, soft burst, boom, soft boom, flower, puffy, puffy diamond,
ghost-ish, pixel circle, pixel triangle, bun, heart. Property names are Kotlin-style (for example
`MaterialShapes.Cookie9Sided`, `MaterialShapes.SoftBurst`); read the class for the exact list.

```kotlin
@OptIn(ExperimentalMaterial3ExpressiveApi::class)
@Composable
fun Avatar() {
    Box(
        Modifier.size(64.dp).clip(MaterialShapes.Cookie9Sided.toShape())
            .background(MaterialTheme.colorScheme.primaryContainer),
    )
}
```
Use for avatars, emphasis, loading, hero art, empty states. Do not use for dense lists or text containers.
`toShape()` is composable (it remembers); call it inside a composable scope, not in a top-level val.

## Morphing

The graphics-shapes library provides `RoundedPolygon` and `Morph`. A morph interpolates between two polygons
with a progress value 0..1 (drive it with a spatial spring).

Gotchas:
- Creating `Morph(a, b)` can throw for some pairs (for example "FloatMapping - Progress repeats a value").
  Wrap creation in try/catch, cache failures, and fall back to no animation or a cross-fade.
- Morph progress from a bouncy spring can leave 0..1. Clamp when sampling if the API requires it.
- Convert a morph to a `Path` with the library helper (`Morph.toPath`, may need opt-in) or draw cubics.

## State shapes

Pressed, selected and checked states change shape. Prefer built-in options:
- `ButtonDefaults.shapes()`, `IconButtonDefaults.shapes()`, `ToggleButtonDefaults.shapes()` (names from the
  official index: `ButtonShapes`, `IconButtonShapes`, `ToggleButtonShapes`, `SplitButtonShapes`, `ListItemShapes`).
- If unavailable, animate the corner radius by hand (see `references/code-patterns.md`).
