# Repository Guidelines

## Project Structure & Module Organization
This repository is a single Noctalia Shell plugin. Core UI and recording logic live in top-level QML files: `Main.qml` handles IPC and process control, `Panel.qml` and `Settings.qml` expose configuration, `BarWidget.qml` shows recorder status, and `RegionSelector.qml` manages area selection. Plugin metadata lives in `manifest.json`, persisted defaults in `settings.json`, translations in `i18n/*.json`, and the helper script in `select_region.sh`. Shader sources are `dimming.frag` and the compiled `dimming.frag.qsb`.

## Build, Test, and Development Commands
There is no standalone build system in this repo; development is done by loading the plugin in Noctalia Shell.

- `qs -c noctalia-shell ipc call plugin:wl-screenrec toggle` opens the plugin panel.
- `qs -c noctalia-shell ipc call plugin:wl-screenrec startRecording` starts monitor recording.
- `qs -c noctalia-shell ipc call plugin:wl-screenrec startRegionRecording` starts region capture.
- `qs -c noctalia-shell ipc call plugin:wl-screenrec stopRecording` stops the active session.

If you update `dimming.frag`, recompile `dimming.frag.qsb` with Qt's `qsb` tool before committing.

## Coding Style & Naming Conventions
Follow the existing style: two-space indentation in QML and JSON, concise inline comments only where behavior is non-obvious, and semicolon-terminated JavaScript statements inside QML blocks. Use `camelCase` for properties, functions, and JSON keys (`selectedRegionGeometry`, `recordingStartTime`). Keep user-facing strings in `i18n/en.json` and `i18n/zh-CN.json` instead of hardcoding them.

## Testing Guidelines
There is no automated test suite yet. Validate changes manually inside Noctalia Shell: start and stop monitor recording, test region selection, confirm settings persist, and verify translated strings still resolve. When changing `select_region.sh`, also test the dependency path for `slurp` and `gpu-screen-recorder`.

## Commit & Pull Request Guidelines
Recent history uses short Conventional Commit prefixes such as `feat:`, `fix:`, and `chore:`. Keep that pattern and write imperative summaries, for example `fix: preserve selected region after panel reopen`. Pull requests should describe the user-visible change, note any dependency or manifest updates, and include screenshots or short recordings for UI changes. Link the related issue when applicable.
