# Components

Names below are confirmed in the official `androidx.compose.material3` API index unless marked (spec) or
(verify). Many are behind `ExperimentalMaterial3ExpressiveApi` or internal in 1.4.0 stable; see
`versions-and-setup.md`.

## Buttons and actions

| Need | Component | Notes |
|------|-----------|-------|
| Sized button | `Button`, `FilledTonalButton`, `OutlinedButton`, `ElevatedButton`, `TextButton` with `ButtonDefaults` size helpers | Five sizes XS 32, S 40, M 56, L 96, XL 136 dp (spec). Default M. Larger sizes for the primary action |
| State shapes | `ButtonShapes`, `ButtonDefaults.shapes()` | Pressed and checked corners change |
| Toggle button | `ToggleButton`, `ElevatedToggleButton`, `FilledTonalToggleButton`, `OutlinedToggleButton`, `TonalToggleButton` | Checked state becomes rounder or squarer than unchecked. Use `ToggleButtonShapes` |
| Group | `ButtonGroup`, `ToggleButtonGroup` (verify exact name) | Connected buttons that reshape neighbours when pressed. Replaces SegmentedButton in Expressive |
| Split button | `SplitButtonLayout`, `SplitButtonShapes`, `SplitButtonDefaults` | Leading action plus trailing dropdown |
| Icon button | `IconButton`, `IconToggleButton`, `FilledIconButton`, `FilledTonalIconButton`, `OutlinedIconButton` + `IconButtonShapes` | Sizes and width options (narrow, default, wide) via `IconButtonDefaults` (verify) |
| FAB | `FloatingActionButton`, `SmallFloatingActionButton`, `LargeFloatingActionButton`, `ExtendedFloatingActionButton` | Add medium and large; extended sizes |
| FAB menu | `FloatingActionButtonMenu`, `FloatingActionButtonMenuItem`, `ToggleFloatingActionButton` | Replaces speed dial. Menu items stack above the toggling FAB |

## Toolbars and bars

| Need | Component |
|------|-----------|
| Floating toolbar | `HorizontalFloatingToolbar`, `VerticalFloatingToolbar` (actions, optional FAB slot, scroll-aware expand) |
| Top app bar | `MediumFlexibleTopAppBar`, `LargeFlexibleTopAppBar` (flexible: subtitle, taller, expressive title) |
| Bottom app bar | `FlexibleBottomAppBar` |
| Search | `AppBarWithSearch`, `SearchBar`, `ExpandedFullScreenSearchBar` |
| Short navigation bar | `ShortNavigationBar`, `ShortNavigationBarItem` (compact bottom bar, replaces NavigationBar) |
| Wide rail | `WideNavigationRail`, `WideNavigationRailItem`, `ModalWideNavigationRail` (collapsed or expanded, replaces drawer) |

## Content

| Need | Component |
|------|-----------|
| Carousel | `HorizontalMultiBrowseCarousel`, `HorizontalUncontainedCarousel`, `HorizontalCenteredHeroCarousel` (new in 1.4) with `CarouselState` |
| Lists | `SegmentedListItem`, `ListItemShapes`, `ListItemDefaults` (grouped lists with shaped segments) |
| Slider | `Slider`, `RangeSlider`, `VerticalSlider` (expressive thicker tracks, optional icon in handle) |
| Progress | `LinearWavyProgressIndicator`, `CircularWavyProgressIndicator` (wave amplitude and speed configurable) |
| Loading | `LoadingIndicator`, `ContainedLoadingIndicator` (shapes morph continuously, replaces short indeterminate circular) |
| Drag handle | `VerticalDragHandle` (1.4) |
| Text fields | `TextField`, `OutlinedTextField`, `SecureTextField` (1.4), state-based overloads with `TextFieldState` |

## Choosing

- Primary action: large Button or ExtendedFloatingActionButton. One per screen.
- Related choices in a row: `ButtonGroup`, not many separate buttons.
- Single or multi selection with few options: `ToggleButton` in a group.
- Long indeterminate wait under about 5 seconds: `LoadingIndicator`. Determinate or longer: wavy progress.
- Navigation: phone portrait `ShortNavigationBar`; medium and expanded widths `WideNavigationRail`.
- Quick actions near content: floating toolbar. Many actions behind one: FAB menu.

## Do not

- Do not mix old and expressive variants of the same component on one screen without a reason.
- Do not enlarge everything. Emphasis loses meaning when everything is emphasized.
- Do not remove labels from navigation items to look minimal. Research found labels help.
