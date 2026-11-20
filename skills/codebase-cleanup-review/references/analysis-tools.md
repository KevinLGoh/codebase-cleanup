# Analysis tools

Tools for step 2 of the workflow, by stack.

Check each tool's command class (rule R3 in SKILL.md) before running it. knip builds its graph from entry files, so a missing entry point makes whole chains of used code look unused: check its entry configuration and framework plugins first.

| Stack | Unused code | Unused dependencies | Duplication | Complexity | Cycles |
|---|---|---|---|---|---|
| JS / TS | knip | knip, depcheck | jscpd | lizard, ESLint | dependency-cruiser, madge |
| Python | vulture | deptry | jscpd, pylint | radon, lizard | import-linter, pydeps |
| Go | staticcheck (U1000), deadcode | go mod tidy -diff | jscpd | gocyclo, lizard | not possible (compiler forbids) |
| Rust | cargo check, clippy | cargo-machete, cargo-udeps | jscpd | lizard | manual review |
| Java / Kotlin | PMD, detekt | build tool reports | PMD CPD | PMD, lizard | jdeps |
| PHP | phpstan | composer-unused | jscpd | lizard | manual review |
| Ruby | debride | manual review | flay | rubocop | manual review |
| Any | rg, git log | manifest review | jscpd | lizard | manual review |
