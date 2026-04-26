# Tauri Skill Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [x]`) syntax for tracking.

**Goal:** Turn the Tauri skill into a project-agnostic app-building guide that links to the right official Tauri docs, lists useful commands, and removes material not directly useful for building Tauri apps.

**Architecture:** Use the skill entrypoint as the main routing page. Keep supporting references small and link-heavy: one official-link map, one command map, and one security/best-practice page. The skill must not mention any specific organization, repository, product, local workflow, or app architecture.

**Tech Stack:** Markdown skill files, official Tauri documentation links, Tauri CLI commands.

---

## Portability Rules

- Do not include organization names, repository names, product names, or private workflow rules.
- Do not assume `npm`, `pnpm`, `yarn`, `bun`, `deno`, or `cargo`; show variants and tell agents to use the target app's existing package manager.
- Do not assume React, Vue, Svelte, Solid, Leptos, or any other frontend framework.
- Do not assume a particular test runner or lint command; tell agents to inspect existing scripts.
- Do not include exact latest-version claims in reusable text.
- Only mention standard Tauri paths and concepts such as `src-tauri`, `Cargo.toml`, `tauri.conf.*`, `src-tauri/capabilities`, `package.json`, official plugins, and Tauri CLI commands.

## File Structure

- Modify: `SKILL.md`
  - Main app-building guide with inspection checklist, official docs, commands, best practices, and verification commands.
- Create: `references/app-building-links.md`
  - Categorized links to official Tauri docs only.
- Create: `references/commands.md`
  - Useful Tauri CLI and verification commands with npm/pnpm/yarn/bun/deno/cargo variants where relevant.
- Create or rewrite: `references/security.md`
  - Concise capabilities, permissions, scopes, CSP, file system, shell/process, updater, and sidecar guidance with links.
- Delete or rewrite old extracted references
  - Remove copied docs, site-source markup, incomplete examples, and anything not directly useful for building Tauri apps.

## Task 1: Rewrite `SKILL.md` as an App-Building Router

**Files:**
- Modify: `SKILL.md`

- [x] **Step 1: Replace frontmatter**

Use:

```markdown
---
name: tauri
description: Use when building or debugging Tauri apps with src-tauri, tauri.conf.json, capabilities, permissions, invoke, events, @tauri-apps/api, Rust commands, plugins, sidecars, WebView2, signing, updater, mobile, build, bundle, or desktop distribution.
---
```

- [x] **Step 2: Add the portability rule**

Add:

```markdown
## Portability

This skill is project-agnostic. Use the target app's existing package manager, framework, versions, scripts, test runner, and directory layout. Do not introduce organization-specific conventions or local-only commands.
```

- [x] **Step 3: Add first-inspect checklist**

Add:

```markdown
## First Inspect

Before editing, inspect the target app's existing choices:

- `package.json` and lockfile for package manager, scripts, frontend framework, and `@tauri-apps/*` versions.
- `src-tauri/Cargo.toml` for Tauri crates, plugins, Rust edition, and sidecar dependencies.
- `src-tauri/tauri.conf.*` for `build`, `app`, `bundle`, `plugins`, identifiers, windows, updater, and security.
- `src-tauri/capabilities/` for permissions and window/webview boundaries.
- Existing command modules, IPC wrappers, state, and tests.
```

- [x] **Step 4: Add official doc map**

Add:

```markdown
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
| Plugins | https://v2.tauri.app/plugin/ |
| File system plugin | https://v2.tauri.app/plugin/file-system/ |
| Sidecars | https://v2.tauri.app/develop/sidecar/ |
| Node.js sidecar | https://v2.tauri.app/learn/sidecar-nodejs/ |
| Distribution | https://v2.tauri.app/distribute/ |
| Windows signing | https://v2.tauri.app/distribute/sign/windows/ |
| v1 to v2 migration | https://v2.tauri.app/start/migrate/from-tauri-1/ |
```

- [x] **Step 5: Add command map**

Add:

```markdown
## Useful Commands

Use the package manager already present in the app.

| Need | npm | pnpm | yarn | cargo |
| --- | --- | --- | --- | --- |
| Dev app | `npm run tauri dev` | `pnpm tauri dev` | `yarn tauri dev` | `cargo tauri dev` |
| Build app | `npm run tauri build` | `pnpm tauri build` | `yarn tauri build` | `cargo tauri build` |
| Bundle existing build | `npm run tauri bundle` | `pnpm tauri bundle` | `yarn tauri bundle` | `cargo tauri bundle` |
| App/environment info | `npm run tauri info` | `pnpm tauri info` | `yarn tauri info` | `cargo tauri info` |
| Add plugin | `npm run tauri add <plugin>` | `pnpm tauri add <plugin>` | `yarn tauri add <plugin>` | `cargo tauri add <plugin>` |
| New capability | `npm run tauri capability new` | `pnpm tauri capability new` | `yarn tauri capability new` | `cargo tauri capability new` |
| List permissions | `npm run tauri permission ls` | `pnpm tauri permission ls` | `yarn tauri permission ls` | `cargo tauri permission ls` |
| Migrate v1 to v2 | `npm run tauri migrate` | `pnpm tauri migrate` | `yarn tauri migrate` | `cargo tauri migrate` |
```

- [x] **Step 6: Add best-practice reminders**

Add short bullets only:

```markdown
## App-Building Practices

- Use official plugins before custom native code when the feature exists.
- Use commands for request/response IPC; use events for lifecycle, progress, or broadcast updates.
- Keep privileged logic and secrets out of the WebView.
- Scope capabilities by window/webview and permission.
- Use scopes for file, shell, HTTP, and other sensitive access.
- Keep CSP as narrow as the app allows.
- Align Tauri Rust crates, npm packages, and plugin versions with the existing app unless explicitly upgrading.
- Run the target app's existing frontend checks, `cargo check --manifest-path src-tauri/Cargo.toml`, and the relevant Tauri build command after app changes.
```

## Task 2: Create Link and Command References

**Files:**
- Create: `references/app-building-links.md`
- Create: `references/commands.md`
- Create or rewrite: `references/security.md`

- [x] **Step 1: Create `app-building-links.md`**

Group official links under:

- Start and project structure.
- Frontend and JavaScript API.
- IPC and events.
- Config, security, and permissions.
- Plugins and native integrations.
- Sidecars.
- Build, signing, updater, and distribution.
- Migration.

- [x] **Step 2: Create `commands.md`**

Include package-manager variants for:

- `dev`
- `build`
- `bundle`
- `info`
- `add`
- `remove`
- `android`
- `ios`
- `migrate`
- `icon`
- `signer`
- `permission`
- `capability`

Include generic verification commands:

```bash
cargo check --manifest-path src-tauri/Cargo.toml
cargo test --manifest-path src-tauri/Cargo.toml
```

State that frontend checks must come from the target app's scripts.

- [x] **Step 3: Create or rewrite `security.md`**

Keep only Tauri app-building guidance:

- Link capabilities, permissions, scopes, and CSP.
- Prefer individual capability files under `src-tauri/capabilities`.
- Treat shell/process, filesystem, updater, HTTP, and remote URL access as sensitive.
- Prefer `BaseDirectory` and scoped file access.
- Do not place secrets in frontend code.

## Task 3: Remove Non-App-Building Content

**Files:**
- Existing reference files under `references/`

- [x] **Step 1: Delete or rewrite copied docs**

Remove reference files that are copied documentation dumps, malformed extractions, or broad background material. Keep only content that helps an agent build a Tauri app.

- [x] **Step 2: Search for forbidden artifacts**

Run this from the skill directory:

```bash
rg -n "```unknown|json title=|toml title=|@astrojs|@assets|<CardGrid|<LinkCard|<ShowSolution" .
```

Expected: no matches.

- [x] **Step 3: Search for project-specific content**

Run this from the skill directory. Replace the placeholder terms with names that should never appear in a reusable skill:

```bash
rg -n "<org-name>|<repo-name>|<product-name>|<absolute-home-path>|localhost:[0-9]+" .
```

Expected: no matches.

## Task 4: Verify The Skill Behavior

**Files:**
- `SKILL.md`
- `references/*.md`

- [x] **Step 1: Check length and link density**

Run:

```bash
wc -w SKILL.md references/*.md
rg -n "https://v2.tauri.app|npm run tauri|pnpm tauri|yarn tauri|cargo tauri" SKILL.md references
```

Expected: the skill is concise, link-heavy, command-focused, and free of copied docs.

- [x] **Step 2: Run portability pressure checks**

Use these prompts against the skill:

```text
Add a file picker and config-file read to an existing Tauri app.
```

Expected: agent checks package manager, `src-tauri/Cargo.toml`, config, capabilities, and links official dialog/fs docs before editing.

```text
Configure Windows signing and update release commands.
```

Expected: agent links official signing/distribution docs and uses generic `tauri build` / `tauri bundle` commands without app-specific assumptions.

```text
Add a Rust command and call it from the frontend.
```

Expected: agent links the official commands/`invoke` docs and inspects existing command organization before adding code.

## Task 5: Add Baseline Evals

**Files:**
- `tests/evals/`
- `README.md`
- `repo-map.json`

- [x] **Step 1: Copy the Promptfoo/OpenCode eval framework**

Copy the eval package layout, Promptfoo wrapper, OpenCode CLI provider, provider tests, coverage check, and Codex compatibility check from the shared engineering-skills eval harness.

- [x] **Step 2: Adapt the harness to this repository**

Rename package metadata for this plugin, keep Promptfoo state under `tests/evals/.promptfoo`, keep OpenCode state local while using the normal OpenCode provider/model data, and add repo-local ignore rules.

- [x] **Step 3: Add Tauri baseline scenarios**

Create a Tauri package with scenarios for Rust commands and `invoke`, filesystem capabilities/scopes, Windows signing and distribution, Node sidecars, and remote asset/IPC security.

- [x] **Step 4: Document eval commands**

Add eval commands to the README and repo map:

```bash
npm --prefix tests/evals run eval:tauri
npm --prefix tests/evals run eval:coverage
npm --prefix tests/evals run eval:codex-compatibility
```

- [x] **Step 5: Verify the eval harness**

Run the OpenCode provider unit test, deterministic eval gates, and the Tauri model-backed eval.
