# Copilot Instructions for ChatGPT Desktop App

## Project Overview
- **Architecture:** Cross-platform desktop app using [Tauri](https://tauri.app/) (Rust backend, React/TypeScript frontend). UI logic is in `src/`, backend in `src-tauri/`.
- **Major Components:**
  - `src/App.tsx`, `main.tsx`: Entry points, route to views based on Tauri webview label.
  - `src/view/`: Main UI views (`Ask.tsx`, `Titlebar.tsx`, `Settings.tsx`).
  - `src/components/`: Reusable UI elements (icons, titlebar, etc).
  - `src-tauri/src/core/`: Rust backend modules for commands, config, window management.

## Key Workflows
- **Build/Run:**
  - Frontend: `pnpm dev` or `npm run dev` (uses Vite).
  - Full app: `pnpm tauri dev` or `npm run tauri` (starts Tauri backend + frontend).
  - Build: `pnpm build` (frontend only), `pnpm tauri build` (full desktop app).
- **Debugging:**
  - Use Tauri's dev tools for backend; React/Vite for frontend.
  - Hotkeys: `Ctrl+Enter`/`Cmd+Enter` to send chat (see `Ask.tsx`).

## Communication Patterns
- **Frontend <-> Backend:**
  - Use Tauri `invoke` API to call Rust commands (see `src-tauri/src/core/cmd.rs`).
  - Example: `invoke('ask_send', { message })` triggers backend chat logic.
  - Backend commands update config, window state, and trigger frontend JS via webview eval.

## Project-Specific Conventions
- **View Routing:**
  - Main React app renders views based on Tauri webview label (`App.tsx`).
- **Config Management:**
  - App config is loaded/amended via Rust (`AppConf` in `src-tauri/src/core/conf.rs`).
- **UI State:**
  - State hooks and hotkeys are used for chat input and window controls.
- **Styling:**
  - Uses Tailwind CSS (`base.css`, `tailwind.config.js`).

## Integration Points
- **Tauri Plugins:**
  - OS, Shell, Dialog plugins enabled in backend (`main.rs`).
- **External APIs:**
  - Chat logic is abstracted; see `cmd.rs` for backend command triggers.

## Examples
- **Add a new backend command:**
  - Implement in `src-tauri/src/core/cmd.rs`, register in `main.rs`.
  - Call from frontend via `invoke('your_command', { ... })`.
- **Add a new view:**
  - Create in `src/view/`, add to `viewMap` in `App.tsx`.

## References
- `README.md`: High-level project info.
- `package.json`: Scripts and dependencies.
- `src-tauri/src/core/cmd.rs`: Backend command patterns.
- `src/view/Ask.tsx`, `Titlebar.tsx`: UI logic and Tauri integration.

---
_Keep instructions concise and focused on current codebase patterns. Update this file if major workflows or architecture change._
