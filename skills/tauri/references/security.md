# Tauri Security and Permissions

Use this page for app-building security decisions. Link to official docs for details instead of copying full examples.

## Core Links

- Capabilities: https://v2.tauri.app/security/capabilities/
- Permissions: https://v2.tauri.app/security/permissions/
- Scopes: https://v2.tauri.app/security/scope/
- Content Security Policy: https://v2.tauri.app/security/csp/
- Security overview: https://v2.tauri.app/security/

## Practices

- Keep privileged logic, secrets, file system access, shell/process access, and updater decisions out of arbitrary frontend code.
- Prefer official plugins before custom native code when the feature exists.
- Put reusable capability definitions in `src-tauri/capabilities/` and scope them by window or webview.
- Grant the narrowest permission set that supports the feature.
- Use scopes for file system, shell, HTTP, and other sensitive access.
- Treat deny rules as higher priority than allow rules when reviewing scopes.
- Configure CSP as narrowly as the app allows; only permit trusted asset and network sources.
- Match plugin permissions to the target platform. Avoid granting desktop-only or mobile-only permissions without checking support.

## Sensitive Surfaces

- File system: prefer `BaseDirectory` and scoped paths. Official docs: https://v2.tauri.app/plugin/file-system/
- Shell and process execution: require explicit scopes and avoid passing untrusted input. Official docs: https://v2.tauri.app/plugin/shell/
- HTTP and remote URLs: restrict origins and avoid broad wildcard access.
- Updater: validate signing, endpoints, and generated update artifacts. Official docs: https://v2.tauri.app/plugin/updater/
- Sidecars: package binaries through Tauri sidecar configuration so users do not need separate runtimes. Official docs: https://v2.tauri.app/develop/sidecar/
