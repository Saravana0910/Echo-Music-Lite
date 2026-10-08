# Echo Lite — YouTube-compatible Android prototype

A deliberately small Android music-player prototype:

**Search → YouTube video ID → audio stream resolution → Media3/ExoPlayer**

## Important architecture choice

The first working build uses the unauthenticated Piped-compatible API as the YouTube-facing adapter. Piped documents `/search` and `/streams/{videoId}` endpoints and returns `audioStreams` containing direct stream URLs. This avoids Google account cookies, OAuth, and session handling in the prototype.

This is **not the official YouTube API** and public Piped instances can change availability/rate-limit behavior. The resolver is isolated in `PipedApi.kt` so it can later be replaced by another backend without changing the UI/player.

## Debug-first UI

The app intentionally shows:

- API endpoint
- search request/result count
- selected YouTube video ID
- stream resolution result
- selected audio quality/bitrate/mime type
- Media3 player state
- Media3 player errors
- exception messages

This makes the first device tests much easier to diagnose.

## Build in GitHub Actions

1. Create a GitHub repository.
2. Upload this project.
3. Push to `main`.
4. Open **Actions → Android Debug APK**.
5. Download the generated `EchoLite-debug.apk` artifact.
6. Install it on a physical Android device.

No Android Studio is required for the GitHub build.

## Local command

With a JDK 17 + Gradle environment:

```bash
gradle assembleDebug
```

The APK is:

```text
app/build/outputs/apk/debug/app-debug.apk
```

## Next upgrades

1. Thumbnail images in results.
2. Queue / next / previous.
3. Background `MediaSessionService`.
4. Notification controls.
5. Persistent cache.
6. Configurable/failover Piped instances.
7. A second resolver implementation if needed.
8. Proper release signing with a user-owned keystore.

## Legal / service note

This project is intended as a technical prototype for public content. It does not include Google account cookies, private-content access, or credential handling.
