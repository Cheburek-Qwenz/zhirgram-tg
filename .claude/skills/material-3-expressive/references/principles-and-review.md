# Principles, research and review

## What Expressive is for

Google presented Expressive Material Design as the result of research across 46 studies over about three
years with more than 18,000 participants. Reported findings: expressive designs help people find key elements
up to four times faster; people of all ages respond well, with the gap between age groups shrinking; and
removing labels or familiar patterns for minimalism hurts usability. Treat these as the rationale, not a rule
to cite as proof for any single screen.

## Principles

1. Emphasis through contrast: size, shape, color and motion highlight what matters.
2. One hero per screen: a clear primary action.
3. Familiar patterns stay: lists, navigation, labels, standard gestures.
4. Shape expresses state and identity, not decoration.
5. Motion is physical and interruptible.
6. Color roles carry meaning; dynamic color is respected.
7. Accessibility is unchanged: contrast, targets, labels, text scaling, reduced motion.

## Accessibility

- Contrast 4.5:1 for body text, 3:1 for large text and UI components. Use on-roles.
- Touch targets 48dp minimum, including small visual controls.
- `contentDescription` for icon-only controls; `Role` and state semantics on custom toggles.
- Not color alone: pair with icon, shape or text.
- Text at 200% font scale must not clip; test it.
- Reduced motion: check `Settings.Global.ANIMATOR_DURATION_SCALE` or provide snap behaviour.
- Wavy and bouncy motion can be distracting; allow the user to calm it.

## Review checklist

Version and setup
- [ ] material3 version known and stated
- [ ] Every Expressive API exists in that version, or a labelled fallback is used
- [ ] `MaterialExpressiveTheme` (or `MaterialTheme` fallback) wraps the app, dynamic color has a static fallback

Visual
- [ ] One clear primary action
- [ ] Colors only from `colorScheme` roles with matching on-roles
- [ ] Shape scale used consistently, inner radius smaller than outer
- [ ] State shapes (pressed, selected) present on interactive components
- [ ] Emphasized type for headlines only, not body

Motion
- [ ] Spatial springs for movement, shape, size; effects springs for color and alpha
- [ ] No bouncy spring on color or alpha
- [ ] Reduced motion respected

Accessibility
- [ ] 48dp targets, descriptions, contrast, text scale 200%
- [ ] Labels kept on navigation and key actions

Code
- [ ] State hoisted, `Modifier` parameter present
- [ ] No invented API names; unsure names are commented
- [ ] Morph and path objects remembered; Morph creation guarded

## Reporting honesty

State what was checked: read only, syntax-checked, compiled, or run on a device and which device. Do not
claim visual or runtime correctness that was not observed.

## Sources

- developer.android.com/jetpack/androidx/releases/compose-material3
- developer.android.com/reference/kotlin/androidx/compose/material3/package-summary
- android-developers.googleblog.com, "What's new in Jetpack Compose" (December 2025)
- design.google / m3.material.io expressive research and specs
