# Changelog

## 2.0.0 — 2026-06-10

Deep restructure for cross-tool portability and weaker-model compatibility.

### Trigger policy changed: broad → medium

- v1 triggered on any "non-trivial AI collaboration" including routine multi-step execution. v2 triggers on: explicit invocation, reliability-behavior requests, or high-stakes work (publish / release / submit / handoff / irreversible / bulk).
- Routine coding, editing, and ordinary multi-step execution no longer trigger.
- Trigger decision rewritten as a first-match decision table in SKILL.md so weaker models can apply it deterministically.

### Structure: 11 protocols → 5, examples merged

- `invocation-router.md` → absorbed into the SKILL.md trigger table.
- `clarification-first.md` → `clarify-before-acting.md` (now a decision table).
- `goal-recalibration.md` + `iteration-feedback.md` → `stay-on-goal.md`.
- `evidence-discipline.md` + `decision-comparison.md` + `adaptive-explanation.md` + `edge-notes.md` → `evidence-and-options.md`.
- `problem-transparency.md` + `fallback-disclosure.md` → `failure-and-fallback.md`.
- `deliverable-audit.md` → `deliver-and-audit.md`.
- `examples.md` → merged into `references/prompt-patterns.md` (prompt + expected behavior pairs).
- Each protocol file now has a disjoint "read when" condition listed in SKILL.md.

### SKILL.md is now self-sufficient

- A tool or model that reads only SKILL.md gets correct basic behavior: trigger table, intensity levels, 12 core rules, all response shapes. Protocol files add depth, not required context.

### Other

- `agents/openai.yaml`: `allow_implicit_invocation` false → true, consistent with the medium-trigger description.
- evals: 12 → 13 cases; added routine-coding negative (no trigger) and bulk-deletion positive (confirm scope first).
- pressure scenarios: rebalanced for medium trigger; added weak-alias-plus-intent and routine-multi-step cases.
- frontmatter: added `license: Apache-2.0` and `metadata.version`.
- READMEs rewritten to match; structure tree corrected (README_CN.md and LICENSE were missing from the v1 tree).

## 1.0.0 — 2026-05-31

Initial public release: 11 protocols, 4 references, pressure scenarios, evals, bilingual READMEs.
