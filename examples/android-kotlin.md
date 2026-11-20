# Trailmark

## Project

Android app for logging hikes offline and syncing later. Kotlin, Jetpack Compose,
MVVM with Hilt, Room for local data, Retrofit for the API. Min SDK 26.

## Commands

- Build debug: `./gradlew assembleDebug`
- Install on device: `./gradlew installDebug`
- Unit tests: `./gradlew testDebugUnitTest`
- One test class: `./gradlew testDebugUnitTest --tests "*.HikeRepositoryTest"`
- Instrumented tests: `./gradlew connectedDebugAndroidTest`
- Lint: `./gradlew lintDebug`
- Kotlin lint: `./gradlew ktlintCheck`
- Format: `./gradlew ktlintFormat`

## Architecture

- `app/`: application class, navigation graph, DI setup.
- `core/data/`: Room database, DAOs, Retrofit services, repositories.
- `core/ui/`: theme, shared composables.
- `feature/<name>/`: screens, ViewModels and UI state for one feature.
- Dependency versions live in `gradle/libs.versions.toml`.
- Room schemas are exported to `core/data/schemas/`. Don't edit them.

## Rules

Do:

- Expose UI state from ViewModels as `StateFlow`. Collect with `collectAsStateWithLifecycle()`.
- Keep composables stateless. Hoist state to the ViewModel.
- Use `viewModelScope` for coroutines in ViewModels. No `GlobalScope`.
- Put strings in `res/values/strings.xml`. No hardcoded text in composables.
- Use `start` and `end` for padding and alignment, never `left` and `right`.
- Write a Room migration for every schema change and bump the version.

Don't:

- Call Retrofit from a ViewModel. Go through a repository.
- Use `!!`. Handle the null.
- Add a library without asking. If approved, add it to `libs.versions.toml`.
- Use `Log.d` for anything with user data.

## Style

- One public composable per file, named after the file.
- Preview every screen composable with `@Preview` in light and dark.
- ktlint handles formatting.

## Before you finish

1. `./gradlew ktlintCheck lintDebug` passes with no new warnings.
2. `./gradlew testDebugUnitTest` passes.
3. `./gradlew assembleDebug` succeeds.
4. If you changed a screen, run it on an emulator in light and dark mode.
5. List the files you changed.

## Never

- Commit `local.properties`, `google-services.json`, keystores or `keystore.properties`.
- Change `applicationId`, signing config or release build types.
- Force push or push to `main`.
