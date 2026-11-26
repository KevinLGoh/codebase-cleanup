# Codebase Cleanup Review

A Claude skill that reviews a codebase the way a careful senior engineer would: it finds code that adds no value, explains why, and plans how to remove it safely.

**Aggressive at finding unnecessary code, conservative about deleting it, evidence-driven when recommending changes.**

## What it finds

| # | Category | Examples |
|---|---|---|
| 1 | Dead code and dependencies | Unused functions, exports, routes, endpoints, imports and packages |
| 2 | Duplicate logic | Copied formatters, validators, fetch wrappers and business rules |
| 3 | Unused UI components | Components never rendered, unused props, styles and assets |
| 4 | Complexity and overengineering | Wrappers that only forward, one-implementation interfaces, needless layers |
| 5 | Legacy code | Finished feature flags, old shims and polyfills, deprecated APIs |
| 6 | Redundant queries and API calls | N+1 queries, repeated fetches, sequential independent awaits |
| 7 | Abandoned files | Unreachable files, `_old` and `.bak` files, configs for removed tools |
| 8 | Structural issues | Circular dependencies, boundary-crossing imports, dumping-ground utils |

For every finding, the report explains **why it's unnecessary** (with evidence), **the impact of removing it**, **the risks to check first**, and **where it fits in a phased cleanup plan**. Findings are tagged with [Refactoring.Guru code smells](https://refactoring.guru/refactoring/smells) where they fit.

## How it stays safe

- **Report only by default.** It writes a `CLEANUP_REVIEW.md` report and changes no code until you approve specific findings.
- **No deletion on missing references alone.** It maps entry points and checks dynamic imports, reflection, framework conventions, config and external consumers before calling anything unused.
- **Separate confidence and risk ratings.** A finding can be certain but still risky to fix. High-risk changes can never be marked "do now".
- **Asks before running your code.** Tests, builds and analysers that load project config only run with your permission. Tools that modify files never run during a review.
- **Small, verified changes.** In apply mode, each change is its own commit, checked against a test baseline and reverted if it causes a new failure.
- **Your work is preserved.** It never overwrites uncommitted changes, and your edits to the report always win.

## Install

### Claude Code (plugin)

This repository is private, so you need read access to it, and git on your machine must be able to authenticate to GitHub.

```bash
claude plugin marketplace add KevinLGoh/codebase-cleanup
claude plugin install codebase-cleanup-review@kevinlgoh
```

Or inside a session: `/plugin marketplace add KevinLGoh/codebase-cleanup`, then `/plugin install codebase-cleanup-review@kevinlgoh`.

### Claude Code (standalone skill)

Copy the skill folder into your personal skills directory:

```bash
git clone https://github.com/KevinLGoh/codebase-cleanup.git
cp -r codebase-cleanup/skills/codebase-cleanup-review ~/.claude/skills/
```

### Claude.ai

Download `codebase-cleanup-review.zip` from the [latest release](https://github.com/KevinLGoh/codebase-cleanup/releases), then upload it in **Settings > Capabilities > Skills**. The release also includes the same skill as a `.skill` file.

## Usage

Ask in plain language ("find dead code in src/api", "what can we safely delete?"), or run the command with arguments:

| Command | What it does |
|---|---|
| `/codebase-cleanup-review` | Audit the whole repository |
| `... audit src/billing` | Audit one directory |
| `... dead-code --changed` | Dead code in files changed against the default branch |
| `... duplicates`, `simplify`, `queries`, `architecture` | Focus on one area |
| `... apply-approved F-003 F-007` | Apply specific approved findings |
| `... apply-approved phase:1` | Apply one phase of the cleanup plan |
| `... audit --report chat` | Summarise in chat without writing a report file |

As a plugin, the command is `/codebase-cleanup-review:codebase-cleanup-review`.

### Optional configuration

Add a `.cleanup-review.yml` to your repository root to set exclusions:

```yaml
report_path: CLEANUP_REVIEW.md
ignore_paths: ["legacy/payments-v1/**", "scripts/one-off/**"]
intentional:
  - path: src/core/ports/
    reason: Hexagonal architecture ports, kept on purpose
known_false_positives:
  - symbol: registerWebhookHandlers
    reason: Loaded by plugin registry at runtime
finding_budget: 40
```

## Recommended first run

Run an `audit` on a repository you know well, then check the top 20 findings by hand. Note which are genuine, actionable or false positives before trusting it with `apply-approved`.

## Repository layout

```text
.claude-plugin/
  plugin.json                  plugin manifest
  marketplace.json             lets this repository act as its own marketplace
skills/codebase-cleanup-review/
  SKILL.md                     rules and workflow
  references/
    analysis-tools.md          tools per language
    code-smells.md             smell catalogue and suggested fixes
    report-template.md         report structure
```

## Credits

- Martin Fowler, [*Refactoring: Improving the Design of Existing Code*](https://martinfowler.com/books/refactoring.html) (2nd edition)
- [Refactoring.Guru code smells catalogue](https://refactoring.guru/refactoring/smells)

## Licence

[MIT](LICENSE)
