# OscanRss

**A Feedly-style RSS feed reader written in [Oscan](https://github.com/lucabol/Oscan)**

OscanRss is a desktop RSS reader with a three-panel GUI: a treeview of groups and feeds, a post list, and a content viewer. It supports HTTP and HTTPS feeds, read/unread tracking, and persistent storage.

## Features

- **Group-based organization** — Organize feeds into groups (Coding, Health, News, etc.)
- **CRUD operations** — Create, edit, and delete groups and feeds
- **Read/unread tracking** — Posts are auto-marked as read when viewed; toggle with `m`
- **Unread filter** — Show all posts or unread-only with `u`
- **HTTP and HTTPS** — TLS built into Oscan (SChannel on Windows, BearSSL on Linux)
- **Persistent storage** — Groups, feeds, and read state saved to `%APPDATA%` / `$HOME`
- **Keyboard-driven** — Vim-inspired shortcuts for navigation
- **Dark theme** — Comfortable reading in any environment
- **Cross-platform** — Windows, Linux, macOS

## Prerequisites

- **[Oscan compiler](https://github.com/lucabol/Oscan)** — required
- **PowerShell** — for the build script

## Quick Start

```powershell
# Build and run
.\build.ps1 -Run

# Build only
.\build.ps1

# Verbose build
.\build.ps1 -V
```

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `j` / `k` | Navigate up/down |
| `Enter` | Select / expand group |
| `Tab` | Switch panel focus |
| `a` | Add group or feed |
| `e` | Edit selected item |
| `d` | Delete selected item |
| `r` | Refresh selected feed |
| `R` | Refresh all feeds |
| `u` | Toggle unread filter |
| `m` | Toggle read/unread |
| `M` | Mark all posts in feed as read |
| `?` | Toggle help overlay |
| `q` | Quit |

## Architecture

```
main.osc          Entry point, UI, event loop
├── url.osc       URL parsing
├── http.osc      HTTP/HTTPS client
├── rss_parse.osc RSS XML parser
├── storage.osc   Persistent file storage
└── libs/ui.osc   UI widget library
```

## Data Storage

Configuration and state are stored as flat files:

- `oscanrss_groups.txt` — Group definitions (pipe-delimited)
- `oscanrss_feeds.txt` — Feed subscriptions (pipe-delimited)
- `oscanrss_read.txt` — Read post GUIDs (one per line)

Files are stored in `%APPDATA%` on Windows or `$HOME` on Linux/macOS.

## Building from Source

```powershell
.\build.ps1              # Build
.\build.ps1 -Run         # Build and run
.\build.ps1 -Test        # Run tests
.\build.ps1 -Clean       # Remove build artifacts
.\build.ps1 -V           # Verbose output
```

## License

MIT
