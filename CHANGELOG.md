# Changelog

## 1.1.0 (2026-11-27)

- Added Codex support, with a Codex plugin manifest, a Codex marketplace and an `agents/openai.yaml` file for the skill
- Moved the icon to `assets/icon.png` so both tools can use it
- Made the skill's wording work in both Claude Code and Codex
- Rewrote the README for public release

## 1.0.0 (2026-11-21)

First public release.

- Eight review categories with deterministic precedence
- Reachability analysis with a false-positive checklist
- Separate confidence, change risk and verification ratings, with priority safety caps
- Command classification (read-only, executes code, modifies files)
- Report with stable finding IDs, statuses and attempt outcomes; user edits preserved
- Apply mode with per-commit and per-phase verification
- Reference files for analysis tools, code smells and the report template
