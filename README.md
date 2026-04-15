# Backend Skills

Backend coding standards for Rust, Tauri, and Node sidecar architecture.

## Skills

| Skill | Description |
|-------|-------------|
| `tauri` | Tauri desktop app framework with Rust backend and Node sidecar |

## Rules

Always-on coding standards in `rules/` covering naming conventions, logging policy, execution policy, and schema changes.

## Install

```bash
claude plugin add accelerate-data/backend-skills
```

## Local development

```bash
claude --plugin-dir .      # Load without installing
claude plugin validate .   # Validate structure
```

## Updating the plugin

1. Make your changes to skills, commands, or rules
2. Bump `version` in `.claude-plugin/plugin.json`
3. Validate: `claude plugin validate .`
4. Test locally: `claude --plugin-dir .`
5. Commit and push — the marketplace picks up the latest default branch automatically (no version field in marketplace entries)
