# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file web app (`index.html`) — a local text editor that reads/writes files directly via the File System Access API. No build step, no dependencies, no server required.

## Architecture

Everything lives in `index.html`: HTML structure, embedded `<style>`, and embedded `<script>`. There is no bundler, framework, or external JS.

**Key JS state:**
- `tabs[]` — array of `{ id, fileName, fileHandle, content, isDirty, scrollTop, selStart, selEnd }`
- `activeTabId` — currently displayed tab
- `hasFileAPI` — boolean, whether `window.showOpenFilePicker` is available

**Key functions:**
- `createTab / switchToTab / closeTab / renderTabs` — tab lifecycle
- `saveEditorToTab / loadTabIntoEditor` — sync between the `<textarea>` and the tab state array
- `loadFromHandle(handle)` — opens a `FileSystemFileHandle` into a tab (used by both Open button and D&D)
- `saveFile / saveAs` — write via `createWritable()` with `abort()` on error
- `updateUI / updateCursorPos / setStatus / showSnackbar` — UI updates

**Theme system:** An inline `<script>` in `<head>` applies `document.documentElement.dataset.theme` before CSS renders (FOUC prevention). Preference stored in `localStorage('theme')` as `'system'|'light'|'dark'`. CSS uses `[data-theme="dark"]` overrides.

**CSS variable layers:**
1. `:root` — Material Design 3 tokens (`--md-*`) + VS Code tab tokens (`--vscode-*`)
2. `[data-theme="dark"]` — dark overrides for both sets

**Keyboard shortcuts** are captured at `document` level with `{ capture: true }` to intercept browser-native shortcuts (e.g. Cmd+S).

**Drag & drop** is handled at `document` level (full-window drop zone), not scoped to the editor element. Multiple files open in separate tabs.

## Testing

Open `index.html` in Chrome 86+. No automated tests. Manual verification:
1. Open a file → edit → Cmd+S → confirm file changed on disk
2. Drop multiple files → each opens in a new tab
3. Close tab with unsaved changes → dialog appears
4. Toggle theme → persists on reload
