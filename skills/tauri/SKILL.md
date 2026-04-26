---
name: tauri
description: Use when building or debugging Tauri apps with src-tauri, tauri.conf.json, capabilities, permissions, invoke, events, @tauri-apps/api, Rust commands, plugins, sidecars, WebView2, signing, updater, mobile, build, bundle, or desktop distribution.
---

# Tauri

Use this skill for project-agnostic Tauri app work. Route to official Tauri docs, inspect the target app's existing choices, and use the app's current package manager, framework, versions, scripts, test runner, and directory layout.

## First Inspect

Before editing, inspect:

- `package.json` and lockfile for package manager, scripts, frontend framework, and `@tauri-apps/*` versions.
- `src-tauri/Cargo.toml` for Tauri crates, plugins, Rust edition, and sidecar dependencies.
- `src-tauri/tauri.conf.*` for `build`, `app`, `bundle`, `plugins`, identifiers, windows, updater, and security.
- `src-tauri/capabilities/` for permissions and window/webview boundaries.
- Existing command modules, IPC wrappers, state, and tests.

## Official Docs

| Task | Official docs |
| --- | --- |
| Create or understand a project | https://v2.tauri.app/start/ |
| Frontend configuration | https://v2.tauri.app/start/frontend/ |
| CLI commands | https://v2.tauri.app/reference/cli/ |
| Configuration schema | https://v2.tauri.app/reference/config/ |
| JavaScript API | https://v2.tauri.app/reference/javascript/api/ |
| Commands and `invoke` | https://v2.tauri.app/develop/calling-rust/ |
| Events and listeners | https://v2.tauri.app/develop/calling-frontend/ |
| Capabilities | https://v2.tauri.app/security/capabilities/ |
| Permissions | https://v2.tauri.app/security/permissions/ |
| Scopes | https://v2.tauri.app/security/scope/ |
| CSP | https://v2.tauri.app/security/csp/ |
| Plugins and feature support | https://v2.tauri.app/plugin/ |
| File system plugin | https://v2.tauri.app/plugin/file-system/ |
| Sidecars | https://v2.tauri.app/develop/sidecar/ |
| Node.js sidecar | https://v2.tauri.app/learn/sidecar-nodejs/ |
| Distribution | https://v2.tauri.app/distribute/ |
| Windows signing | https://v2.tauri.app/distribute/sign/windows/ |
| v1 to v2 migration | https://v2.tauri.app/start/migrate/from-tauri-1/ |

## Useful Commands

Use the package manager already present in the app.

| Need | npm | pnpm | yarn | cargo |
| --- | --- | --- | --- | --- |
| Dev app | `npm run tauri dev` | `pnpm tauri dev` | `yarn tauri dev` | `cargo tauri dev` |
| Build app | `npm run tauri build` | `pnpm tauri build` | `yarn tauri build` | `cargo tauri build` |
| Bundle existing build | `npm run tauri bundle` | `pnpm tauri bundle` | `yarn tauri bundle` | `cargo tauri bundle` |
| App/environment info | `npm run tauri info` | `pnpm tauri info` | `yarn tauri info` | `cargo tauri info` |
| Add plugin | `npm run tauri add <plugin>` | `pnpm tauri add <plugin>` | `yarn tauri add <plugin>` | `cargo tauri add <plugin>` |
| Remove plugin | `npm run tauri remove <plugin>` | `pnpm tauri remove <plugin>` | `yarn tauri remove <plugin>` | `cargo tauri remove <plugin>` |
| New capability | `npm run tauri capability new` | `pnpm tauri capability new` | `yarn tauri capability new` | `cargo tauri capability new` |
| List permissions | `npm run tauri permission ls` | `pnpm tauri permission ls` | `yarn tauri permission ls` | `cargo tauri permission ls` |
| Android dev | `npm run tauri android dev` | `pnpm tauri android dev` | `yarn tauri android dev` | `cargo tauri android dev` |
| iOS dev | `npm run tauri ios dev` | `pnpm tauri ios dev` | `yarn tauri ios dev` | `cargo tauri ios dev` |
| Migrate v1 to v2 | `npm run tauri migrate` | `pnpm tauri migrate` | `yarn tauri migrate` | `cargo tauri migrate` |

## App-Building Practices

- Use official plugins before custom native code when the feature exists.
- Use commands for request/response IPC; use events for lifecycle, progress, or broadcast updates.
- Keep privileged logic and secrets out of the WebView.
- Scope capabilities by window/webview and permission.
- Use scopes for file, shell, HTTP, and other sensitive access.
- Keep CSP as narrow as the app allows.
- Align Tauri Rust crates, npm packages, and plugin versions with the existing app unless explicitly upgrading.
- Run the target app's existing frontend checks, `cargo check --manifest-path src-tauri/Cargo.toml`, and the relevant Tauri build command after app changes.

## References

- `references/app-building-links.md` - categorized official Tauri docs.
- `references/commands.md` - Tauri CLI and verification commands.
- `references/security.md` - capabilities, permissions, scopes, CSP, and sensitive plugin surfaces.
