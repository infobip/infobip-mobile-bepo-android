# Infobip Mobile Bepo Android

Library provides Infobip branded [Android Material Design 3](https://m3.material.io) Compose components.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Integration](#integration)
- [BepoTheme](#bepotheme)
- [Naming Conventions](#naming-conventions)
- [Color Variants](#color-variants)
- [Components](#components)
    - [Buttons](#buttons)
    - [Input](#input)
    - [Selection](#selection)
    - [Cards](#cards)
    - [Dialogs](#dialogs)
    - [Feedback](#feedback)
    - [Pickers](#pickers)
    - [Display](#display)
    - [Layout](#layout)
- [MVI Architecture Pattern](#mvi-architecture-pattern)
- [Utils](#utils)

---

## Overview

Infobip Mobile Bepo Android is an [Android Jetpack Compose](https://developer.android.com/compose)
UI component library that implements the Infobip brand on top
of [Material Design 3](https://m3.material.io). It provides a complete set of themed, ready-to-use
composables — from buttons and text fields to dialogs, pickers, and progress indicators — all
prefixed with `Bepo` and styled via a unified theming system.

The library is designed for Infobip product teams but can be customized for any brand by overriding
the `BepoTheme` sub-systems (colors, typography, shapes, alpha).

## Features

- **25+ composable components** — buttons, text fields, switches, cards, dialogs, snackbars, toasts,
  pickers, badges, progress indicators, and more
- **Unified theming** — `BepoTheme` extends Material 3 with custom color schemes, typography,
  shapes, and alpha values
- **Semantic color variants** — most components support Brand, Info, Success, Warning, and Danger
  variants
- **Date/time integration** — text fields with built-in picker dialogs and generic type converters
- **MVI architecture utilities** — base ViewModel, contract classes, and event processor for clean
  unidirectional data flow
- **Compose utilities** — keyboard controller, color alpha extensions, text style modifiers, window
  insets helpers, dialog edge-to-edge support
- **Customizable defaults** — each component has a corresponding `Defaults` object for fine-grained
  styling
- **Dark mode** — full light and dark color scheme support
- **API documentation** — Dokka-generated Javadoc published to Maven Central for IDE auto-complete

## Requirements

| Requirement       | Version    |
|-------------------|------------|
| Android minSdk    | 23         |
| Android compileSdk| 36         |
| Kotlin            | 2.0.20     |
| Compose BOM       | 2026.03.01 |
| Java (toolchain)  | 17         |

## Integration

Add the dependency to your `build.gradle(.kts)`:

```kotlin
implementation("com.infobip:infobip-mobile-bepo-android:1.0.0")
```

## BepoTheme

`BepoTheme` is the main entry point for applying the Infobip brand to your Compose application. It
ensures a consistent look and feel across all components prefixed with `Bepo`.

`BepoTheme` is a wrapper around the Material3 theme
and [extends Material3 sub-systems](https://developer.android.com/develop/ui/compose/designsystems/custom#replacing-systems)
with its own:

- `BepoColorScheme` - defines the color palette used by Bepo components.
- `BepoTypography` - defines the typography styles used by Bepo components.
- `BepoShapes` - defines the shapes used by Bepo components.
- `BepoAlpha` - defines the alpha values used by Bepo components.

You can customize all sub-systems if the defaults do not fit your needs:

```kotlin
@Composable
fun MyApp() {
    BepoTheme(
        colorScheme = BepoColorScheme(),
        typography = BepoTypography(),
        shapes = BepoShapes(),
        alpha = BepoAlpha()
    ) {
        // Your content here
    }
}
```

## Naming Conventions

Component names use Android naming with the `Bepo` prefix, e.g., `BepoButton` or `BepoTextField`.
If a component has more sub-types, library follows Bepo naming conventions as it is unified naming
convention between designers and engineers across Infobip. Using Bepo naming conventions streamlines
communication and component understanding across teams, enabling faster UI implementation from Figma
designs.

In following example of `BepoButton` you can see mapping between Android sub-type naming and the
Bepo naming:

| `BepoButton` Component Type | [Android Compose Button Component](https://m3.material.io/components/buttons/overview#501bf0cf-fbb5-45b5-abc1-c3bae35c0e6a) |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Primary                     | Filled button                                                                                                               |
| Secondary                   | Outlined button                                                                                                             |
| Tertiary                    | Text button                                                                                                                 |

> **Warning:**
> The term `primary` can be confusing. Both Android and Bepo use it, but it has different meaning in
> both.
> In Android, `primary` is a color name for the app's main color.
> In Bepo, `primary` is both a color and a component type (e.g., `BepoButton.Primary()`).
>
> ```kotlin
> BepoTheme.color.brand == MaterialTheme.color.primary
> ```

## Color Variants

Many Bepo components support multiple color variants. The most common variants include:

- Primary
- Secondary
- Brand
- Info
- Warning
- Success
- Danger

## Components

All components are built on Material 3, themed via `BepoTheme`, and follow Bepo design conventions.
Each component has a corresponding `Defaults` object for customizing colors, shapes, and typography.

### Buttons

Action triggers for user interactions. Supports filled, outlined, text, icon-only, and navigation
button styles with semantic color variants (Brand, Info, Success, Warning, Danger).

| Component    | Description                                          |
|--------------|------------------------------------------------------|
| `BepoButton` | Primary, Secondary, Tertiary, Icon, and Nav buttons |

### Input

Text entry components with built-in validation support, labels, placeholders, and error states. Date
and time fields integrate with their respective picker dialogs.

| Component              | Description               |
|------------------------|---------------------------|
| `BepoTextField`        | Text input with variants and validation |
| `BepoDateTextField`    | Date input field          |
| `BepoTimeTextField`    | Time input field          |
| `BepoDateTimeTextField`| Combined date-time input field |

### Selection

Components for choosing between options. Each supports semantic color variants.

| Component        | Description                |
|------------------|----------------------------|
| `BepoSwitch`     | Toggle switch with variants |
| `BepoRadioButton`| Radio button with variants |
| `BepoChip`       | Chip and InputChip         |

### Cards

Content containers for grouping related information.

| Component  | Description                          |
|------------|--------------------------------------|
| `BepoCard` | Primary and Secondary card containers |

### Dialogs

Modal overlays for alerts, confirmations, and user input.

| Component    | Description              |
|--------------|--------------------------|
| `BepoDialog` | Alert and custom dialogs |

### Feedback

Components that communicate status, results, or system state to the user. Supports semantic variants
(Info, Success, Warning, Danger).

| Component          | Description                                          |
|--------------------|------------------------------------------------------|
| `BepoSnackbar`     | Snackbar notifications with variants                 |
| `BepoSnackbarHost` | Snackbar host container and state management         |
| `BepoSnackbarNow`  | Extension functions for immediate snackbar display   |
| `BepoToast`        | Toast notifications with variants                    |
| `BepoMessage`      | Message cards with semantic variants                 |
| `BepoError`        | Error and empty state displays                       |
| `BepoHelperText`   | Helper text with semantic variants                   |

### Pickers

Dedicated selection dialogs for dates, times, and list items.

| Component              | Description                            |
|------------------------|----------------------------------------|
| `BepoDatePicker`       | Date picker dialog                     |
| `BepoTimePicker`       | Time picker dialog                     |
| `BepoBottomSheetPicker`| Bottom sheet picker with selectable items |

### Display

Visual indicators, badges, avatars, and progress components for presenting information.

| Component              | Description                                      |
|------------------------|--------------------------------------------------|
| `BepoBadge`            | Dot and text badges                              |
| `BepoBadgedBox`        | Container with badge overlay                     |
| `BepoInitials`         | Avatar with initials                             |
| `BepoStatusDot`        | Status indicator dot                             |
| `BepoMenuItem`         | Menu item with icon or initials                  |
| `BepoProgressIndicator`| Linear, Circular, and Infobip pulse indicators   |
| `BepoPullToRefreshBox` | Pull-to-refresh container                        |

### Layout

Structural components for page-level layout and navigation.

| Component       | Description                        |
|-----------------|------------------------------------|
| `BepoScaffold`  | Scaffold wrapper with Bepo theming |
| `BepoTopAppBar` | Top app bar and centered variant   |

## MVI Architecture Pattern

The `com.infobip.mobile.bepo.compose.mvi` package provides foundational classes and interfaces for
implementing the Model-View-Intent (MVI) architecture in Compose applications. MVI promotes clean
code and clear separation of concerns by organizing logic into Model, View, and Intent components.
Its unidirectional data flow simplifies state management, improves predictability, and enhances
testability, making it a robust choice for building scalable and maintainable Android apps.

`MviViewModel` is a base class for your `ViewModel` that implements the MVI architecture pattern. It
offers self-explanatory methods:

- `updateState(State.() -> State)`
- `sentEvent(Event)`
- `executeAction(Action)`
- `procesViewAction(ViewAction)` - abstract functions you are supposed to implement in
  your `ViewModel`.

`MviContract` defines the contract base classes for MVI components, including:

- `ViewState`
- `ViewEvent`
- `ViewAction`

`MviEventProcessor` is a utility class that offers a composable function of the same name, designed
to handle events emitted by your ViewModel in safe manner.

Example usage of MVI architecture pattern in Compose:

```kotlin
class MyScreenContract {

    @Immutable
    data class State(
        val data: String = "",
    ) : ViewState()

    sealed class Event : ViewEvent() {
        data object JobDone : Event()
    }

    sealed class Action : ViewAction() {
        data class FetchData(val id: String) : Action()
    }
}

class MyViewModel(
    private val myUseCase: MyUseCase
) : MviViewModel<MyScreenContract.State, MyScreenContract.Event, MyScreenContract.Action>(MyScreenContract.State()) {

    override fun processViewAction(viewAction: MyScreenContract.Action) {
        when (viewAction) {
            is MyScreenContract.Action.FetchData -> {
                viewModelScope.launch {
                    // Fetch data logic
                    updateState { copy(data = "Fetched data for ${viewAction.id}") }
                    sentEvent(MyScreenContract.Event.JobDone)
                }
            }
        }
    }
}

@Composable
fun MyScreen(
    viewModel: MyViewModel = viewModel(factory = MyViewModelFactory(myUseCase))
) {
    val viewState by viewModel.viewStateFlow.collectAsStateWithLifecycle()

    MviEventProcessor(viewModel.viewEventsFlow) { event ->
        when (event) {
            is MyScreenContract.Event.JobDone -> {
                // Show snackbar or do navigation
            }
        }
    }

    Button(
        onClick = { viewModel.executeAction(MyScreenContract.Action.FetchData("id")) }
    ) {
        Text("Click me")
    }
}
```

## Utils

The `com.infobip.mobile.bepo.compose.utils` package offers utility classes and Compose helper
functions:

| Utility                       | Description                                                            |
|-------------------------------|------------------------------------------------------------------------|
| `Color.alpha()`               | Apply alpha transparency to a color                                    |
| `rememberKeyboardController()`| Keyboard show, hide, and clear focus controller                        |
| `TextStyle` extensions        | `.bold()`, `.semiBold()`, `.medium()`, `.light()`, and more            |
| `WindowInsets` helpers        | `WindowInsets.none`, `WindowInsets.isNotZero`, `PaddingValues.isNotZero()` |
| `EnabledDialogEdgeToEdge()`   | Edge-to-edge support for dialogs                                       |
