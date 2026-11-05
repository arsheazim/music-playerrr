# Offline Music Player for Android (with Shuffle Mode)

A modern, high-performance offline music player application built for Android in **Kotlin**. Designed to play audio files directly from device storage with **zero internet connection required**, featuring an intelligent **Shuffle Engine**, background foreground playback service with lock-screen notification controls, and a sleek Material 3 dark-themed user interface.

---

## 🌟 Key Features

1. **True Offline Playback**:
   - Scans and indexes local music tracks (`.mp3`, `.m4a`, `.wav`, `.flac`, `.aac`, `.ogg`) using Android's `MediaStore.Audio` content provider.
   - Automatically filters out short notification chimes, system sound effects, and ringtones (< 5s duration).
   - Real-time search by song title, artist, or album name.

2. **Smart Shuffle Mode (`Shuffle Engine`)**:
   - **Shuffle ON**: Generates a randomized non-repeating queue using the Fisher-Yates algorithm. If a track is already playing when shuffle is toggled, it remains playing seamlessly at index 0 while the remaining queue is randomized.
   - **Shuffle OFF**: Seamlessly transitions back to sequential alphabetical/album order without interrupting the currently playing track.
   - Quick **"Shuffle All"** button directly on the main header for instant 1-tap randomized playback.
   - Distinct visual state indicator (glows active green when enabled) on both the mini-player and full-screen player.

3. **Background & Lock Screen Playback**:
   - Dedicated foreground service (`MusicService`) with `mediaPlayback` foreground type.
   - Rich `MediaStyle` notification with Play/Pause, Next, and Previous controls.
   - Supports hardware and Bluetooth headset button controls.
   - Automatically pauses on phone calls or transient audio loss and resumes when finished (`AudioManager.OnAudioFocusChangeListener`).

4. **Modern UI & Bottom Sheet Player**:
   - Sticky bottom Mini-Player bar with live progress indicator.
   - Full-Screen Expandable Now Playing sheet with large album artwork, marquee scrolling song title, interactive scrubbing SeekBar, current/remaining timestamps, Shuffle toggle, Repeat toggle (Off / All / One), and Play/Pause controls.

5. **Up-to-Date Android Permissions**:
   - Android 13+ (API 33+): Uses `READ_MEDIA_AUDIO` and `POST_NOTIFICATIONS`.
   - Android 12 and below: Uses `READ_EXTERNAL_STORAGE`.

---

## 📂 Project Architecture

```
OfflineMusicPlayer/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml
│   │   ├── java/com/example/offlinemusicplayer/
│   │   │   ├── adapter/
│   │   │   │   └── SongAdapter.kt          # RecyclerView adapter with search filter & active track highlight
│   │   │   ├── model/
│   │   │   │   └── Song.kt                 # Data model with formatted time and ContentUri album art
│   │   │   ├── service/
│   │   │   │   └── MusicService.kt         # Foreground audio service, MediaPlayer, and Shuffle Engine
│   │   │   ├── ui/
│   │   │   │   └── MainActivity.kt         # UI controller, permissions handling, bottom sheet player
│   │   │   └── util/
│   │   │       └── MusicScanner.kt         # MediaStore query engine for local device audio
│   │   └── res/
│   │       ├── drawable/                   # Vector icons (shuffle, repeat, play, pause, next, prev)
│   │       ├── layout/
│   │       │   ├── activity_main.xml       # Main screen with header, list, and mini-player
│   │       │   ├── bottom_sheet_player.xml # Full-screen Now Playing bottom sheet
│   │       │   └── item_song.xml           # Song list item card
│   │       └── values/
│   │           ├── colors.xml              # Dark obsidian palette & accent colors
│   │           ├── strings.xml             # Localized UI strings
│   │           └── themes.xml              # Material 3 dark theme
│   └── build.gradle.kts
├── build.gradle.kts
├── settings.gradle.kts
└── gradlew.bat
```

---

## 🚀 How to Open and Run in Android Studio

1. **Open Android Studio**.
2. Select **File > Open...** and navigate to:
   ```
   C:\Users\Umair\Downloads\OfflineMusicPlayer
   ```
3. Allow Gradle to sync dependencies.
4. Connect an Android phone (with USB debugging enabled) or start an Android Emulator.
5. Click the green **Run (▶)** button (or press `Shift + F10`).
6. When prompted on the device, grant the **Audio Storage Permission**. The player will immediately scan your local storage and list all your offline songs!
