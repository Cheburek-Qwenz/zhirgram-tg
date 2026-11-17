---
name: material-3-expressive
description: >
  Build and review Material 3 Expressive (M3E) UI, Jetpack Compose first. Covers version gating of the
  Expressive APIs, MaterialExpressiveTheme, spring motion (MotionScheme), shape library and morphing,
  emphasized type, sized and toggle buttons, button groups, split buttons, FAB menu, floating toolbars,
  wavy progress, loading indicator, short navigation bar, wide rail, carousels, fallbacks, accessibility.
  Use when: "material 3 expressive", "M3E", "expressive", "MaterialExpressiveTheme", "MotionScheme",
  "MaterialShapes", "ButtonGroup", "LoadingIndicator", "wavy progress", "floating toolbar", "shape morph".
user-invokable: true
argument-hint: "[component|theme|motion|shape|audit|fallback] [description]"
---

# Material 3 Expressive

Material 3 Expressive (announced May 2025) is the newest layer of Material Design 3. It keeps the M3 token
system and adds bolder shape, spring-based motion, larger and more prominent controls, emphasized type and
stronger containment. Jetpack Compose is the primary implementation target.

This skill covers only what Expressive adds or changes. For base M3 (tokens, color roles, adaptive layout,
navigation patterns) use a general Material 3 skill together with this one.

## Workflow

1. Detect the stack and the exact `androidx.compose.material3` version (Gradle files, version catalog, BOM).
   Read `references/versions-and-setup.md`. State the version you assume. Expressive APIs are version-gated.
2. Decide what the task needs: theme, one component, a whole screen, or an audit.
3. Load only the matching reference:
   - theme, setup, version gate, fallback: `references/versions-and-setup.md`
   - shape tokens, MaterialShapes, morphing: `references/shape-and-morphing.md`
   - springs, MotionScheme, press and state animation: `references/motion.md`
   - component list, sizes, usage: `references/components.md`
   - ready patterns and the no-Expressive fallback code: `references/code-patterns.md`
   - principles, research findings, accessibility, review checklist: `references/principles-and-review.md`
4. Write real Material components with hoisted state. Never fake a component with boxes at fixed offsets.
5. Say honestly what was verified: syntax only, compiled, or run on a device. Never claim more.

## Core rules (always apply)

- Check the version first. If an Expressive API is internal or missing in the user's version, use the
  fallback in `references/code-patterns.md` and tell the user which parts are stand-ins.
- Do not invent API names. Use only names confirmed in the official API index (listed in
  `references/components.md`). If unsure, use the stable equivalent and add a one-line comment naming the
  Expressive component it stands in for.
- Colors come only from `MaterialTheme.colorScheme` roles with their matching on-roles. No hex in components.
- Movement, size and shape changes use spatial springs (may overshoot). Color and alpha use effects springs
  (never overshoot). Read specs from `MaterialTheme.motionScheme` when available.
- Pressed, selected and checked states change shape where the component supports it.
- One clear primary action, larger and more prominent than the rest. Keep text labels on actions that need them.
- Keep familiar patterns (lists, navigation, labels). Expressive does not mean replacing standard layouts.
- Touch targets at least 48dp, content descriptions on icon-only controls, color is never the only signal.
- Respect the system "remove animations" setting.

## Quick facts

| Topic | Fact |
|-------|------|
| Entry point | `MaterialExpressiveTheme(colorScheme, motionScheme = MotionScheme.expressive(), shapes, typography, content)` |
| Opt-in | `@OptIn(ExperimentalMaterial3ExpressiveApi::class)` where the annotation resolves |
| Shape tokens added | large increased 20dp, extra large increased 32dp, extra extra large 48dp |
| Shape library | `MaterialShapes` (about 35 shapes), convert with `.toShape()` |
| Button heights (spec) | XS 32, S 40, M 56, L 96, XL 136 dp |
| Type | 15 emphasized styles added to the type scale |
| Motion | spatial springs (move, resize, reshape) and effects springs (color, alpha), each fast, default, slow |
| Wavy progress | `LinearWavyProgressIndicator`, `CircularWavyProgressIndicator` |
| Loading | `LoadingIndicator`, `ContainedLoadingIndicator` (morphing shapes) |
| Navigation | `ShortNavigationBar`, `WideNavigationRail`, `ModalWideNavigationRail` |

## Sources

- Android Developers: Compose Material 3 release notes and API reference (package-summary index)
- Android Developers Blog, "What's new in Jetpack Compose", December 2025
- Google Design, Expressive Material Design research (46 studies, 18,000+ participants)
- m3.material.io for spec values
- Community summaries (skills.sh m3-expressive, composables.com) used only for version gating; verify against
  the release notes of the version in use.
