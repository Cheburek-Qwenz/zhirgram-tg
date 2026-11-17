# Motion

Expressive motion is physics-based: springs, not fixed duration and easing curves, for most UI changes.

## Two spring families

`MotionScheme` exposes both families, each in fast, default and slow speeds:

| Family | Use for | May overshoot |
|--------|---------|---------------|
| Spatial | position, size, scale, rotation, shape/corner changes | yes (expressive scheme bounces) |
| Effects | color, alpha, elevation fades, other non-spatial properties | no |

Rules:
- Never animate color or alpha with a bouncy spring. It flashes or goes out of range.
- Use fast for small elements, default for most, slow for large or full-screen changes.
- Read specs from the theme so the whole app follows the scheme:

```kotlin
val scheme = MaterialTheme.motionScheme
val size by animateDpAsState(target, scheme.defaultSpatialSpec(), label = "size")
val tint by animateColorAsState(color, scheme.defaultEffectsSpec(), label = "tint")
```
Function names (`defaultSpatialSpec`, `fastSpatialSpec`, `slowSpatialSpec`, `defaultEffectsSpec`,
`fastEffectsSpec`, `slowEffectsSpec`) follow the `MotionScheme` interface; confirm in the KDoc for the version.
`MotionScheme.standard()` is the calmer scheme, `MotionScheme.expressive()` the bouncy one. Reported spring
values (verify in source): expressive spatial damping about 0.6 to 0.8 with stiffness 800, 380, 200; effects
damping 1.0 with stiffness 3800, 1600, 800.

## Transitions between screens

Classic duration and easing tokens still fit enter, exit and shared-axis transitions: emphasized 500ms,
emphasized decelerate 400ms (entering), emphasized accelerate 200ms (leaving), standard 300ms.

## Practical guidance

- Press feedback: change shape and slight scale on press, spring back on release.
- Interruptions: springs keep velocity, so reversing mid-animation feels natural. Do not restart from zero.
- Do not animate everything. Motion should explain state change, not decorate.
- Respect reduced motion: when animations are disabled, snap to the final value.
