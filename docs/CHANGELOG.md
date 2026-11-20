# Changelog

## v1.2.0 (2026-11-20)

### Features

- **Interactive Terminal & Browser Playback (`PlayOptionsScreen`):** Pressing `p` on a search result now lets you choose between **Play Audio Only (Terminal)**, **Play Video + Audio (`mpv`)**, and **Open in Default Web Browser**.
- **Audio Output Detection:** Uses PipeWire/PulseAudio default or enumerated `pactl` sinks when active, and falls back to detecting **BlueALSA** Bluetooth sinks (`bluealsa-cli`) and **ALSA** PCM devices (`aplay -L`) on headless setups.
- **Playback Controls & Live Streams:** Added `PlaybackManager` supporting `mpv` (with JSON IPC) and `yt-dlp` + `ffmpeg` + `aplay` fallback, **Pause/Resume (`Space`)**, **Restart from `0:00` (`0`)**, **Stop (`s`)**, and live stream playback (`-reconnect`).
- **Pre-Playback Quality / Codec Selector:** Cycle presets (`Best Available (DASH/HLS)`, `1080p`, `720p`, `480p`, `Best Audio`, `Opus`, `AAC`) in `PlayOptionsScreen` (persisted in `play_format`).
- **Headless Video Guard:** Automatically disables video playback when neither `WAYLAND_DISPLAY` nor `DISPLAY` is set on Linux.
- **Search History:** Persists past search queries in `~/.config/yt-tui/search_history.json` (`↑`/`↓` to recall, `Ctrl+L` to clear), with **Search History** (`on`/`off`) and **Max Search History Items** configurable in **Settings**.

### Bug Fixes

- **Light Theme Contrast:** Updated `THEME_LIGHT` to use explicit `COLOR_WHITE` background with `stdscr.bkgd()`, fixing invisible black-on-black text on dark terminals.
- **Fresh Playback Start:** Added `--no-resume-playback` to `mpv` so tracks start from `0:00` instead of resuming from `watch_later`.

## v1.0.1 (2026-07-28)

### Bug Fixes

- **`?` character lost during URL paste** — Global `?` → HelpScreen handler in `App.run()` was intercepting `?` characters before they reached the active screen. During paste, `?` would open HelpScreen and the next character would be consumed by HelpScreen's pop handler. Moved `?` handler to `MainMenu.handle_key()` only.
- **YouTube Music Mix playlist timeout** — Auto-generated Mix playlists have many pages. yt-dlp needs to fetch all pages to determine total video count. Increased timeout from 30s to 60s in `PlaylistDetect._check()` and `FormatSelector._fetch()`.
- **YouTube Music URL support** — Added `normalize_url()` to auto-convert `music.youtube.com` to `www.youtube.com` to avoid HTTP 403 errors from yt-dlp.

### Features

- **Ctrl+V paste guidance** — URLInput now shows explicit Ctrl+V paste hint in status bar and instruction text.
- **Debug logging** — URL flow is logged to `/tmp/yt-tui_debug.log` for troubleshooting.

### Technical

- `normalize_url()` applied at 9 points: URLInput, PlaylistDetect (x2), FormatSelector, DownloadProgress, BatchDownload, BatchProgress, PlaylistProgress, clipboard detection.
- Cleaned stale `__pycache__/` bytecode caches.

## v1.0.0 (2026-07-22)

Initial release with full feature set:

- Main Menu with 6 options: Search, Download URL, Batch Download, History, Settings, Exit
- YouTube search via `ytsearch:` with results display
- URL input with playlist auto-detection
- Playlist Overview with Download All / Select Videos / Range options
- Multi-select playlist video picker with checkboxes
- Format Selector with all available formats + 6 quality presets
- Subtitle language picker (manual & auto-generated)
- Folder browser with create-new-folder
- Live download progress bar (gradient), speed, ETA, fragment tracking
- Sequential playlist download with per-video progress
- Batch download from `.txt` file
- Download history with re-download
- Settings: default format, directory, history limit, theme
- Dark/Light theme toggle (keyboard + mouse)
- Single-file Python curses app
