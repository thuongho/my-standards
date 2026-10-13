# CLAUDE.md

## Version bump on every plugin change

Any change under `skills/` (add, edit, rename, delete) must bump `version` in `.claude-plugin/plugin.json` in the same commit.

**Why:** Claude Code caches installed plugins by version. An unchanged version means `/plugin` update keeps the stale copy and the change never shows up.

**How to apply:** patch bump (`1.0.2` → `1.0.3`) for edits, minor bump for a new skill. Never commit a `skills/` change without it.
