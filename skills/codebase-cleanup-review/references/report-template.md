# Report template

Structure for the report written in step 6. Each finding uses the fields listed in SKILL.md.

```markdown
# Cleanup Review: <repository>

Run: <date> · Mode: <mode> · Scope: <scope> · Commit: <sha>

## Summary

- Findings: <n>, with counts by status, category, priority, confidence, risk and verification
- Files affected: <n> · Estimated effort: <range>
- Baseline: <passed>/<total> tests, <n> already failing (or "not run")
- Estimated savings (not measured): ~<n> lines, <n> dependencies, <n> files

## Coverage

Analyses run, with tool, command class and status. Gaps and checks that could not run.

## Top priorities

## Cleanup plan

## Findings

### F-014 · Unnecessary service wrapper

`src/services/filings.ts:42-58` · Status: Open · Attempt: Not attempted

| Field | Detail |
|---|---|
| Category | 4. Complexity and overengineering |
| Smells | Middle Man |
| What it is, and why it's unnecessary | <description and evidence> |
| Impact of removing | <benefit> |
| Risks before changing | <specific checks> |
| Confidence and change risk | High, Medium |
| Priority | Do now, verification required |
| Recommendation | <action, steps and alternatives considered> |
| Effort and verification | S, Not run |
| Fingerprint | `src/services/filings.ts#FilingsService.getFiling` · `4/forwarding-wrapper` · `a3f9c2` |

## Appendix: lower-priority findings

| ID | Category | Location | Summary | Confidence | Risk | Priority |
|---|---|---|---|---|---|---|

## History

| ID | Change | Date | By | Note |
|---|---|---|---|---|
```
