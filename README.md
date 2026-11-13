# NOVA

**A bilingual media experience for Android and iOS, built with Flutter.**

[Download for Android](https://github.com/novastremio/nova-mobile/releases/latest) · [Watch Party](docs/watch-party/README.md) · [Shared collections](docs/shared-collections/README.md)

## Discover and watch

NOVA brings catalogs, add-ons, playback, and your library together on phones and tablets. Browse in Arabic or English, connect the services you use, and customize the experience for your profile.

- **Discover** movies, series, anime, and live TV through installed add-ons and catalogs, with search, recommendations, and a calendar.
- **Play your way** with audio and subtitle selection, chapter and skip markers, and configurable playback settings. Android Core supports Media3 and libmpv; iOS uses libmpv.
- **Bring your sources** using add-ons, supported Debrid services, or local torrent playback. Availability depends on the platform and source.
- **Keep your library together** with watch history, Continue Watching, watchlists, custom lists, and optional linked services including Trakt, Simkl, AniList, MyAnimeList, MDBList, and Letterboxd.
- **Watch together** in a shared room with synchronized playback, chat, and optional source locking. A full NOVA account and active profile are required.
- **Share collections** with other accounts and manage member permissions.
- **Make it yours** with profiles, Kids features, light and dark themes, optional OLED mode, and Arabic RTL and English layouts.

NOVA uses Supabase Auth and an active profile for the app. Account and profile data sync through Supabase; provider credentials are kept in secure on-device storage. NOVA does not host or distribute media.

## Download

Download the latest Android APK from [GitHub Releases](https://github.com/novastremio/nova-mobile/releases/latest). Android checks for updates using the manifest in this repository.

iOS builds require macOS and Xcode. The Codemagic workflow produces an unsigned IPA for signing with iLoader; an installable iOS update destination is not currently configured.

## Development

The repository root is the Flutter project. CI uses Flutter `3.49.0-0.2.pre` at revision `38ec981bad973156ad05bdef0aa8e82d1a58905b` and Java 17.

```sh
git clone https://github.com/novastremio/nova-mobile.git
cd nova-mobile
flutter pub get
flutter run
```

Run the analyzer and tests with:

```sh
flutter analyze --no-pub
flutter test --no-pub
```

Build Android release packages with:

```sh
flutter build apk --release
flutter build appbundle --release
```

Android uses the signing credentials in `android/key.properties` when configured. Without them, the build falls back to a debug signing key. An update installed over an existing app must use the same signing certificate.

For iOS, use macOS with Xcode and prepare the local torrent framework before building. The project targets iOS 18 and later.

```sh
bash tool/prepare_ios_torrent.sh
flutter pub get
flutter build ios --release --no-codesign
```

The app has default Supabase project settings. For a separate backend, provide `NOVA_SUPABASE_URL` and `NOVA_SUPABASE_PUBLISHABLE_KEY` as Flutter `--dart-define` values and configure the backend described in [Supabase setup](supabase/README.md).

## Project structure

| Path | Contents |
| --- | --- |
| `lib/core/` | API clients, models, state, authentication, sync, playback services, and theme |
| `lib/features/` | App screens and feature-specific logic |
| `lib/shared/` | Reusable widgets |
| `lib/l10n/` | Arabic and English translations |
| `android/`, `ios/` | Native platform projects |
| `packages/` | Local Flutter and native packages |
| `supabase/` | Database migrations, functions, and deployment notes |
| `cloudflare/watch-party/` | Optional Watch Party relay worker |
| `prototype/` | Interactive React design prototype |
| `test/` | Flutter unit and widget tests |

More information is available in the [Watch Party guide](docs/watch-party/README.md), [shared collections guide](docs/shared-collections/README.md), [Letterboxd guide](docs/letterboxd/README.md), and [prototype README](prototype/README.md).
