# Pantry

## Project

Grocery list and meal planner app. Flutter 3 for iOS and Android, English and Arabic.
State with flutter_bloc, DI with get_it and injectable, routing with go_router. Talks to a
REST API we don't own, so responses can change without notice.

## Commands

- Install: `flutter pub get`
- Run: `flutter run --flavor dev -t lib/main_dev.dart`
- Test: `flutter test`
- Test one file: `flutter test test/features/lists/list_bloc_test.dart`
- Lint: `flutter analyze`
- Format: `dart format lib test`
- Codegen: `dart run build_runner build --delete-conflicting-outputs`
- Translations: `flutter gen-l10n`

## Architecture

- `lib/core/`: theme tokens, network client, router, shared widgets.
- `lib/features/<name>/data/`: models, API and local sources, repository implementations.
- `lib/features/<name>/domain/`: entities, repository contracts, use cases.
- `lib/features/<name>/presentation/`: bloc, pages, widgets.
- All routes live in `lib/core/router/app_router.dart`.
- Strings live in `lib/l10n/app_en.arb` and `lib/l10n/app_ar.arb`.
- `*.g.dart` and `*.freezed.dart` are generated. Never edit them. Run codegen instead.

## Rules

Do:

- Use Bloc with events and states. No Cubit, no Provider, no setState for shared state.
- Return `Either<Failure, T>` from repositories. Don't throw from data or domain.
- Use `EdgeInsetsDirectional` and `AlignmentDirectional`, never left/right versions.
- Add every new string to both ARB files.
- Take colors and text styles from `lib/core/theme/`. No hex values in widgets.
- Dispose every controller, timer and stream subscription in `dispose()`.

Don't:

- Call the API from a widget or a bloc. Go through a use case.
- Add a package to `pubspec.yaml` without asking.
- Use `print`. Use the logger in `lib/core/log.dart`.

## Style

- Files in snake_case, one public widget per file.
- `const` constructors wherever the analyzer allows it.
- Comments explain why, not what. No commented-out code.

## Before you finish

1. `flutter analyze` prints "No issues found!".
2. `flutter test` passes.
3. If you touched `@freezed`, `@JsonSerializable` or `@injectable`, run codegen.
4. Open the changed screen in Arabic and check that it mirrors.
5. List the files you changed.

## Never

- Commit `.env`, `google-services.json`, `GoogleService-Info.plist` or `key.properties`.
- Change signing config, bundle IDs or Fastlane files.
- Force push or push to `main`.
