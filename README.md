# Backend Skills

Backend coding standards for Rust, Tauri, and Node sidecar architecture.

## Skills

| Skill | Description |
|-------|-------------|
| `tauri` | Project-agnostic Tauri app-building guide with official docs, useful commands, IPC, capabilities, plugins, sidecars, build, signing, updater, and distribution links |

## Rules

Always-on coding standards in `rules/` covering naming conventions, logging policy, execution policy, and schema changes.

## Install

```bash
claude plugin add accelerate-data/backend-skills
```

Codex installs plugins through registered marketplaces. Register the marketplace repo or
marketplace checkout that contains `backend-skills`; do not register this plugin source repo
directly as a marketplace root.

## Local development

```bash
claude --plugin-dir .      # Load without installing
claude plugin validate .   # Validate structure
python3 scripts/validate_plugin_manifests.py
python3 scripts/check_plugin_version_bump.py --base-ref origin/main
npm --prefix tests/evals run eval:coverage
npm --prefix tests/evals run eval:codex-compatibility
npm --prefix tests/evals run eval:tauri  # Requires OpenCode auth
codex plugin marketplace --help  # Confirm the local Codex CLI marketplace workflow
```

## Updating the plugin

1. Make your changes to skills, commands, or rules
2. Bump `version` in both `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json` to the same value
3. Validate: `python3 scripts/validate_plugin_manifests.py`
4. Check the shared version bump: `python3 scripts/check_plugin_version_bump.py --base-ref origin/main`
5. Run deterministic eval checks: `npm --prefix tests/evals run eval:coverage` and `npm --prefix tests/evals run eval:codex-compatibility`
6. Run the Tauri skill eval when OpenCode auth is available: `npm --prefix tests/evals run eval:tauri`
7. Validate in Claude: `claude plugin validate .`
8. Test locally in Claude: `claude --plugin-dir .`
9. Confirm the local Codex CLI marketplace workflow: `codex plugin marketplace --help`
10. Commit and push — the marketplaces pick up the latest default branch automatically
11. After merge, verify from the marketplace repo that references this plugin source
