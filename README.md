# yt-tui 🎬

**yt-dlp Terminal User Interface** — Download YouTube videos & playlists from your terminal with a clean curses TUI.

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Curses](https://img.shields.io/badge/UI-curses-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## ✨ Features

- 🎯 **Single video & playlist** — auto-detect, overview, multi-select, range
- 🎵 **MP3 mode** — download as audio with one key (`m`)
- 📁 **Folder browser** — navigate, pick, or create new folders
- 📊 **Live progress** — real-time progress bar, speed, ETA
- 🔄 **Auto-merge** — video-only formats automatically merged with best audio
- 📋 **Download history** — track what you've downloaded
- ⚙️ **Settings** — configurable format, directory, history size
- 🪶 **Lightweight** — single `.py` file, no heavy frameworks

---

## 📦 Installation

### One-liner (Linux / macOS / Termux)

```bash
curl -sSL https://raw.githubusercontent.com/Twilight0/yt-tui/main/install.sh | bash
```

This installs yt-dlp, downloads YT-TUI, and sets up the `yt-tui` command automatically.

### Windows

```bash
pipx install yt-tui
```

Or install manually:

```bash
pip install yt-tui
python -m yt_tui
```

### Prerequisites

- Python 3.8+
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) (installed automatically by the one-liner)

---

## 🎮 Usage

```
Main Menu
├── Download URL        → Paste link, select format, pick folder
├── Batch Download      → Download from a .txt list of URLs
├── Download History    → Browse & re-download previous downloads
├── Settings            → Default format, directory, max history
└── Exit
```

### Controls

Keys are context-dependent — the same key can do different things on
different screens (`p`, `t`, `d`, `n` and `q` in particular).

**Main menu**

| Key | Action |
|-----|--------|
| `↑` / `↓` | Navigate |
| `Enter` | Confirm / Enter |
| `?` | Help |
| `t` | Toggle dark/light theme |
| `q` / `Esc` | Quit |

**Search**

| Key | Action |
|-----|--------|
| type, `Backspace` | Query text |
| `Enter` | Start search |
| `Ctrl+V` | Paste URL from clipboard (recommended over long-press paste) |
| `Ctrl+U` | Clear input field |
| `Esc` | Go back |

**Search results**

| Key | Action |
|-----|--------|
| `↑` / `↓` | Move |
| `PgUp` / `PgDn`, `Home` / `End` | Page / jump to ends |
| `Tab` / `t` | Flip Videos ↔ Playlists |
| `p` | Play highlighted item (termux-open / xdg-open / open / startfile) |
| `Enter` | Open details — or Load-more on the `>>` row |
| `n` | New search |
| `Esc` | Back |

**Format list**

| Key | Action |
|-----|--------|
| `↑` / `↓` | Navigate |
| `Enter` / `d` | Select format (download) |
| `p` | Quality presets (⚠️ different `p` than on search results) |
| `r` | Refresh formats |
| `Esc` | Go back |

**Subtitles**

| Key | Action |
|-----|--------|
| `↑` / `↓`, `←` / `→` / `Tab` | Move, switch manual/auto column |
| `Space` | Toggle language |
| `a` / `n` | All / none |
| `Enter` | Confirm, `Esc` skip |

**Download folder**

| Key | Action |
|-----|--------|
| `↑` / `↓`, `Enter` | Browse directories |
| `n` | Create new folder |
| `d` | Download here |
| `Esc` | Back |

**Download progress**

| Key | Action |
|-----|--------|
| `q` | Cancel download |
| after done: `n` / `h` / `q` / `Esc` | New download / home / quit / back |

**History**

| Key | Action |
|-----|--------|
| `↑` / `↓` | Navigate |
| `r` | Re-download entry |
| `d` | Delete entry |
| `C` (shift) | Clear all history |
| `Esc` | Back |

**Playlist**

| Key | Action |
|-----|--------|
| `↑` / `↓`, `Enter` | Choose Download-all / Select / Range |
| `m` | MP3 mode toggle |
| picker: `Space`, `a` (toggle all), `n` (none), `d` | Select videos, download |
| range: type `1,3,5-10`, `Enter` | Range download |
| `Esc` | Back |

> **Note:** Use `Ctrl+V` to paste URLs instead of long-press paste. Long-press paste can drop special characters like `?` in some terminal emulators. `Ctrl+V` reads the clipboard directly via Android API (requires `termux-api` on Termux).

---

## 🗂️ Project Structure

```
yt-tui/
├── install.sh            # One-liner installer
├── pyproject.toml        # Python packaging
├── yt_tui.py             # Main application (single file)
├── requirements.txt      # Python dependencies
└── README.md             # This file
```

Runtime config is stored at `~/.config/yt-tui/`:
```
~/.config/yt-tui/
├── config.json          # Default format, last directory, etc.
└── history.json         # Download history
```

---

## 🔧 Technical

- **Single-file Python** app using built-in `curses` library
- **No web framework** — pure terminal UI
- **yt-dlp** invoked as subprocess with custom progress templates
- Works on Termux (Android), Linux, macOS, WSL

---

## 📝 License

MIT — use it, modify it, share it.

---

> Built with ❤️ for Termux 📱
