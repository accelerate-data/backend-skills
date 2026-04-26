# Tauri Commands

Use the package manager and scripts already present in the target app. If the app wraps Tauri in custom scripts, prefer those scripts.

## Lifecycle

| Need | npm | pnpm | yarn | bun | deno | cargo |
| --- | --- | --- | --- | --- | --- | --- |
| Dev app | `npm run tauri dev` | `pnpm tauri dev` | `yarn tauri dev` | `bun tauri dev` | `deno task tauri dev` | `cargo tauri dev` |
| Build app | `npm run tauri build` | `pnpm tauri build` | `yarn tauri build` | `bun tauri build` | `deno task tauri build` | `cargo tauri build` |
| Bundle existing build | `npm run tauri bundle` | `pnpm tauri bundle` | `yarn tauri bundle` | `bun tauri bundle` | `deno task tauri bundle` | `cargo tauri bundle` |
| App/environment info | `npm run tauri info` | `pnpm tauri info` | `yarn tauri info` | `bun tauri info` | `deno task tauri info` | `cargo tauri info` |

## Plugins, Permissions, and Capabilities

| Need | npm | pnpm | yarn | cargo |
| --- | --- | --- | --- | --- |
| Add plugin | `npm run tauri add <plugin>` | `pnpm tauri add <plugin>` | `yarn tauri add <plugin>` | `cargo tauri add <plugin>` |
| Remove plugin | `npm run tauri remove <plugin>` | `pnpm tauri remove <plugin>` | `yarn tauri remove <plugin>` | `cargo tauri remove <plugin>` |
| New capability | `npm run tauri capability new` | `pnpm tauri capability new` | `yarn tauri capability new` | `cargo tauri capability new` |
| List permissions | `npm run tauri permission ls` | `pnpm tauri permission ls` | `yarn tauri permission ls` | `cargo tauri permission ls` |
| Add permission | `npm run tauri permission add` | `pnpm tauri permission add` | `yarn tauri permission add` | `cargo tauri permission add` |
| Remove permission | `npm run tauri permission rm` | `pnpm tauri permission rm` | `yarn tauri permission rm` | `cargo tauri permission rm` |

## Mobile

| Need | npm | pnpm | yarn | cargo |
| --- | --- | --- | --- | --- |
| Android init | `npm run tauri android init` | `pnpm tauri android init` | `yarn tauri android init` | `cargo tauri android init` |
| Android dev | `npm run tauri android dev` | `pnpm tauri android dev` | `yarn tauri android dev` | `cargo tauri android dev` |
| Android build | `npm run tauri android build` | `pnpm tauri android build` | `yarn tauri android build` | `cargo tauri android build` |
| iOS init | `npm run tauri ios init` | `pnpm tauri ios init` | `yarn tauri ios init` | `cargo tauri ios init` |
| iOS dev | `npm run tauri ios dev` | `pnpm tauri ios dev` | `yarn tauri ios dev` | `cargo tauri ios dev` |
| iOS build | `npm run tauri ios build` | `pnpm tauri ios build` | `yarn tauri ios build` | `cargo tauri ios build` |

## Migration and Assets

| Need | npm | pnpm | yarn | cargo |
| --- | --- | --- | --- | --- |
| Migrate v1 to v2 | `npm run tauri migrate` | `pnpm tauri migrate` | `yarn tauri migrate` | `cargo tauri migrate` |
| Generate icons | `npm run tauri icon <path>` | `pnpm tauri icon <path>` | `yarn tauri icon <path>` | `cargo tauri icon <path>` |
| Generate signing key | `npm run tauri signer generate` | `pnpm tauri signer generate` | `yarn tauri signer generate` | `cargo tauri signer generate` |
| Sign update package | `npm run tauri signer sign` | `pnpm tauri signer sign` | `yarn tauri signer sign` | `cargo tauri signer sign` |

## Verification

Use the target app's existing frontend scripts for tests, linting, and type checks. For the Rust side, these are usually safe checks:

```bash
cargo check --manifest-path src-tauri/Cargo.toml
cargo test --manifest-path src-tauri/Cargo.toml
```

For configuration, packaging, plugin, signing, updater, or sidecar changes, run the relevant Tauri `build` or `bundle` command for the target app and platform.
