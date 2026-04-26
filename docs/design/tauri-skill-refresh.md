# Tauri Skill Refresh Design

**Date:** 2026-04-26
**Status:** Proposed

## Context

The `tauri` skill should help agents build Tauri apps across many repositories. The useful behavior is not to mirror the Tauri docs; it is to route agents to the right official document, remind them which standard Tauri files to inspect, and provide the commands they are likely to need while implementing an app.

The current skill has too much copied documentation and extracted site noise. It also includes stale or risky snippets. That creates the wrong default: agents may copy local reference text instead of checking the target app and the current official Tauri docs.

## Goal

Make the skill a compact Tauri app-building guide that points agents to the right official docs and common commands for creating, modifying, debugging, securing, testing, and packaging Tauri apps.

## Portability Requirement

The skill must be project-agnostic. It must not include organization names, repository names, product names, private workflow rules, default package-manager assumptions, local-only scripts, or app-specific architecture decisions. It may reference standard Tauri paths and concepts such as `src-tauri`, `Cargo.toml`, `tauri.conf.*`, `src-tauri/capabilities`, `package.json`, official Tauri plugins, and Tauri CLI commands.

## Scope

Keep only content directly related to building applications with Tauri:

- Project creation and existing-app inspection.
- Frontend configuration for app UIs.
- Rust commands, JavaScript `invoke`, events, and state.
- `tauri.conf.*`, capabilities, permissions, scopes, and CSP.
- Official plugins used by apps, especially file system, shell/process, updater, logging, window state, CLI, dialogs, notifications, and sidecars.
- Development, debug, build, bundle, mobile, signing, and distribution commands.
- Verification commands that prove an app change works.

Remove or avoid:

- General Rust, Node, or backend standards not specific to Tauri app work.
- Long copied docs pages.
- Site implementation artifacts such as Astro components, image asset references, TODOs, and broken `unknown` code fences.
- Marketplace, plugin-repository, or organization-specific process details.
- Exact latest-version claims in reusable skill text.

## Design

### Entrypoint Role

`SKILL.md` should be the routing page. It should fit in one read and answer:

1. When should this skill load?
2. Which app files should the agent inspect first?
3. Which official doc should the agent open for this task?
4. Which commands are usually useful?
5. What Tauri-specific pitfalls should the agent avoid?

It should not carry a full local copy of the Tauri documentation.

### Frontmatter

Use trigger terms agents and users actually write:

```yaml
---
name: tauri
description: Use when building or debugging Tauri apps with src-tauri, tauri.conf.json, capabilities, permissions, invoke, events, @tauri-apps/api, Rust commands, plugins, sidecars, WebView2, signing, updater, mobile, build, bundle, or desktop distribution.
---
```

### First-Inspect Checklist

Before proposing edits, agents should inspect the target app:

- `package.json` for package manager, frontend scripts, and `@tauri-apps/*` packages.
- Lockfile (`package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`, or `deno.lock`) to avoid switching package managers.
- `src-tauri/Cargo.toml` for Tauri crate versions, plugins, sidecars, and Rust edition.
- `src-tauri/tauri.conf.json`, `tauri.conf.json5`, or `Tauri.toml` for `build`, `app`, `bundle`, `plugins`, `identifier`, `productName`, and `app.security`.
- `src-tauri/capabilities/` for permissions already granted to windows/webviews.
- Existing IPC wrappers, command modules, state management, and frontend test setup, without assuming names or framework choices.

### Official Doc Link Map

The skill should include a table like this instead of copied docs:

| Task | Link |
| --- | --- |
| Create or understand a Tauri project | https://v2.tauri.app/start/ |
| Frontend framework configuration | https://v2.tauri.app/start/frontend/ |
| CLI lifecycle commands | https://v2.tauri.app/reference/cli/ |
| Tauri configuration schema | https://v2.tauri.app/reference/config/ |
| JavaScript API reference | https://v2.tauri.app/reference/javascript/api/ |
| Rust commands and `invoke` | https://v2.tauri.app/develop/calling-rust/ |
| Events and frontend listeners | https://v2.tauri.app/develop/calling-frontend/ |
| Capabilities | https://v2.tauri.app/security/capabilities/ |
| Permissions | https://v2.tauri.app/security/permissions/ |
| Scopes | https://v2.tauri.app/security/scope/ |
| CSP | https://v2.tauri.app/security/csp/ |
| Official plugins and feature support | https://v2.tauri.app/plugin/ |
| File system plugin | https://v2.tauri.app/plugin/file-system/ |
| Sidecars | https://v2.tauri.app/develop/sidecar/ |
| Node.js sidecar recipe | https://v2.tauri.app/learn/sidecar-nodejs/ |
| Distribution | https://v2.tauri.app/distribute/ |
| Windows signing | https://v2.tauri.app/distribute/sign/windows/ |
| v1 to v2 migration | https://v2.tauri.app/start/migrate/from-tauri-1/ |

### Command Map

The skill should include short command recipes. Agents should adapt `npm run tauri` to the package manager already used by the app.

| Need | Commands |
| --- | --- |
| Inspect Tauri and environment | `npm run tauri info`, `cargo tauri info` |
| Start dev app | `npm run tauri dev`, `pnpm tauri dev`, `cargo tauri dev` |
| Build app and bundles | `npm run tauri build`, `cargo tauri build` |
| Generate bundles from an existing build | `npm run tauri bundle`, `cargo tauri bundle` |
| Add official plugin | `npm run tauri add <plugin>`, `cargo tauri add <plugin>` |
| Remove plugin | `npm run tauri remove <plugin>`, `cargo tauri remove <plugin>` |
| Create capability | `npm run tauri capability new`, `cargo tauri capability new` |
| Manage permissions | `npm run tauri permission ls`, `npm run tauri permission add`, `npm run tauri permission rm` |
| Initialize mobile targets | `npm run tauri android init`, `npm run tauri ios init` |
| Run mobile dev | `npm run tauri android dev`, `npm run tauri ios dev` |
| Build mobile | `npm run tauri android build`, `npm run tauri ios build` |
| Migrate v1 app | `npm run tauri migrate`, `cargo tauri migrate` |
| Generate icons | `npm run tauri icon <path>`, `cargo tauri icon <path>` |
| Signing helpers | `npm run tauri signer generate`, `npm run tauri signer sign` |

The skill should also remind agents to run local app tests:

- Frontend: use the app's existing script, for example `npm test`, `pnpm test`, `npm run test`, or `npm run lint`.
- Rust: `cargo check --manifest-path src-tauri/Cargo.toml` and `cargo test --manifest-path src-tauri/Cargo.toml`.
- End-to-end app build when packaging/config changes: the app's `tauri build` command.

### Best Practices To Encode

These should be concise reminders plus links:

- Prefer static frontend output for production; Tauri serves built app assets rather than a production SSR server. Link: https://v2.tauri.app/start/frontend/
- Use commands for request/response IPC and events for lifecycle or broadcast communication. Link: https://v2.tauri.app/develop/calling-rust/
- Keep privileged logic, secrets, file system access, shell/process access, and updater decisions in Rust or official plugins, not arbitrary frontend code.
- Capabilities belong in `src-tauri/capabilities`; keep them scoped by window/webview and permission. Link: https://v2.tauri.app/security/capabilities/
- Use scopes for granular plugin or command access; deny rules should be treated as higher priority than allow rules. Link: https://v2.tauri.app/security/scope/
- Configure CSP as narrowly as the app allows. Link: https://v2.tauri.app/security/csp/
- Prefer official plugins before custom native code when the feature exists. Link: https://v2.tauri.app/plugin/
- Match the app's current Tauri major/minor line unless the task is explicitly an upgrade.
- For file access, prefer `BaseDirectory` and scoped paths through the file system plugin rather than broad absolute access. Link: https://v2.tauri.app/plugin/file-system/
- For sidecars, use Tauri's sidecar packaging flow and avoid requiring users to install Node.js/Python separately. Links: https://v2.tauri.app/develop/sidecar/ and https://v2.tauri.app/learn/sidecar-nodejs/

## Proposed File Shape

### `SKILL.md`

Keep this as the only file most agents need for common tasks:

- Trigger frontmatter.
- First-inspect checklist.
- Doc link map.
- Command map.
- Best-practice reminders.
- Verification checklist.

Target length: 300-600 words plus tables.

### `references/app-building-links.md`

Optional compact reference for categorized official links. Keep it link-heavy and avoid copied examples.

### `references/commands.md`

Optional command reference with npm/pnpm/yarn/cargo variants and when to use each command.

### `references/security.md`

Optional concise guide for capabilities, permissions, scopes, CSP, and dangerous plugin surfaces. Link out for details.

## Validation

Run a content hygiene check so extracted docs do not return:

```bash
rg -n "```unknown|json title=|toml title=|@astrojs|@assets|<CardGrid|<LinkCard|<ShowSolution" skills/tauri
```

Expected result: no matches.

Run a portability check for organization-specific or local-machine content. Replace the placeholder terms with names that should never appear in a reusable skill:

```bash
rg -n "<org-name>|<repo-name>|<product-name>|<absolute-home-path>|localhost:[0-9]+" skills/tauri
```

Expected result: no matches.

## Acceptance Criteria

- The skill links to official Tauri docs for each common app-building task.
- The skill includes useful app lifecycle commands and package-manager variants.
- The skill tells agents what target app files to inspect before editing.
- The skill keeps best practices as short reminders with links.
- The skill no longer contains copied doc dumps or site-source artifacts.
- The skill avoids exact latest-version claims and stale snippets.
