# memo

A single-file text editor that lets you edit local files directly from the browser.

![screenshot](screenshot.png)

## Usage

Just open `index.html` in Chrome — no installation or server required.

```
open index.html
```

## Features

- **Multi-tab** — Open and switch between multiple files at once
- **Read/write files** — Overwrite files directly from the browser via the File System Access API
- **Drag & drop** — Drop files from your desktop onto the window (supports multiple files)
- **Themes** — Light / Dark / System (3 options)
- **Font size** — Adjust with `−`/`+` in the status bar or keyboard shortcuts
- **Auto-reload** — Detects external file changes (e.g. iCloud Drive sync) every 3 seconds and reloads automatically

## Shortcuts

| Action | Shortcut |
|---|---|
| New tab | `Ctrl/Cmd + N` |
| Open file | `Ctrl/Cmd + O` |
| Save | `Ctrl/Cmd + S` |
| Save as | `Ctrl/Cmd + Shift + S` |
| Close tab | `Ctrl/Cmd + W` |
| Increase font | `Ctrl/Cmd + =` |
| Decrease font | `Ctrl/Cmd + -` |
| Switch tabs | `←` / `→` (while tab is focused) |

## Requirements

Chrome 86+ (browsers with File System Access API support).

Other browsers support file reading and drag & drop, but not overwrite saving.
