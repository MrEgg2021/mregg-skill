# mregg-skill

A portable reliability protocol for AI collaboration.

It is not a personality skin, prompt trick, or model-specific wrapper. It is a reusable operating protocol for work that matters: clarify before acting, reason from evidence, expose problems, compare options, disclose fallbacks, and deliver outputs that can be checked.

The public project name is **MrEgg.skill**. The machine-readable folder and skill id is **`mregg-skill`**, for compatibility with skill systems that require lowercase letters, numbers, and hyphens.

## What It Does

Use `mregg-skill` when the cost of a wrong, vague, overconfident, or hidden-failure AI response is higher than the cost of a slightly more structured process.

It makes an AI assistant:

- ask before guessing when ambiguity matters — and proceed under labeled assumptions when it does not;
- recalibrate when a long task drifts from the original goal;
- revise from feedback without discarding valid work;
- separate evidence, reasoning, assumptions, and uncertainty;
- give objective critique instead of flattering the user;
- compare options and recommend one, with trade-offs;
- disclose failures before retrying, and fallbacks with a reliability rating;
- audit a deliverable before claiming completion.

The goal is not to make every answer longer. The goal is to make important answers trustworthy.

## When It Triggers

**Medium-trigger policy** — the skill activates in exactly three situations:

1. **Explicit invocation** — `mregg-skill`, `MrEgg.skill`, "use the MrEgg method", "use the reliability protocol", 按旦旦的方法.
2. **Reliability-behavior requests** — "do not guess", "do not flatter me", "separate evidence from assumptions", "compare options and recommend one", "disclose fallbacks", "audit before saying done", and similar.
3. **High-stakes work** — publishing, releasing, submitting, handing off, bulk or irreversible changes.

It deliberately does **not** trigger for greetings, quick factual answers, routine coding or editing, or ordinary multi-step execution. Reliability is not ceremony; routine work should stay fast.

Weak aliases (`MrEgg`, `Dandan`, `旦旦`, `蛋蛋`, `是旦不是蛋`) never trigger by themselves — only together with a reliability request.

## Intensity Levels

The skill always uses the lightest sufficient level:

| Level | Name | Output |
|---:|---|---|
| 0 | Off | Normal reply, no markers |
| 1 | Light | Conclusion → Assumptions → Output → Quick check |
| 2 | Structured | Only the sections that help |
| 3 | Audit | Full structure with risks, fallback, and final audit |

When active, the visible footprint defaults to one marker line — `Reliability mode: light` / `structured` / `audit` — not a heavy template.

Useful prompts:

```text
Use mregg-skill in light mode. Keep it concise.
Use mregg-skill in structured mode for the analysis, then light mode for execution.
Use full audit mode. Include assumptions, evidence, risks, uncertainty, fallback, and a final audit.
```

More invocation patterns, each with its expected behavior: [references/prompt-patterns.md](references/prompt-patterns.md).

## Project Structure

```text
mregg-skill/
├── SKILL.md                          # Canonical entry point — self-sufficient
├── README.md
├── README_CN.md
├── CHANGELOG.md
├── LICENSE
├── agents/
│   └── openai.yaml                   # Optional metadata for OpenAI-style tools
├── evals/
│   └── evals.json                    # Machine-readable test cases
├── protocols/                        # Depth, loaded on demand
│   ├── clarify-before-acting.md      # Ask vs assume: a decision table
│   ├── stay-on-goal.md               # Goal recalibration + revising from feedback
│   ├── evidence-and-options.md       # Evidence discipline, option comparison, explanation, edge notes
│   ├── failure-and-fallback.md       # Problem transparency + fallback disclosure
│   └── deliver-and-audit.md          # Completion checklist
├── references/
│   ├── compatibility.md              # Per-tool install and usage notes
│   ├── output-checklist.md           # Pre-flight for complex outputs
│   ├── privacy-boundaries.md         # Public/private boundary
│   └── prompt-patterns.md            # Invocation prompts + expected behavior
└── tests/
    └── pressure-scenarios.md         # Human-readable regression scenarios
```

## Design Principles

- **SKILL.md is self-sufficient.** A tool — or a weaker model — that reads only SKILL.md gets correct basic behavior: the trigger table, intensity levels, core rules, and all response shapes. Protocol files add depth, not required context.
- **Decision tables over prose.** Trigger and clarify decisions are "first matching row wins" tables, so less capable models can apply them deterministically.
- **Reliable process, light output.** Triggering never implies a heavy template. The level matches the risk.
- **Meta-skill, not a replacement.** Domain skills (coding, writing, patents, document parsing) do the work; `mregg-skill` adds the reliability layer:

```text
Use the PDF extraction skill to read the file, then use mregg-skill to audit the extracted findings and uncertainty.
```

## Installation

The bundle is plain Markdown/JSON — no scripts, network access, or dependencies.

- **Claude Code**: copy the folder to `~/.claude/skills/mregg-skill/`. Re-copy after each update; installed copies do not auto-sync.
- **Claude.ai / Desktop**: zip the folder itself (the archive must expand into `mregg-skill/`) and upload via Skills.
- **OpenAI-style agents**: `agents/openai.yaml` is read by tools that understand it; others use SKILL.md directly.
- **Any other tool**: if it supports Agent Skills, point it at the folder; if not, paste SKILL.md as a system/custom instruction — it works standalone.

Details per tool: [references/compatibility.md](references/compatibility.md).

## Testing and Maintenance

- [tests/pressure-scenarios.md](tests/pressure-scenarios.md) — 23 human-readable regression scenarios, including negative cases (routine work must not trigger; explicit brevity always wins).
- [evals/evals.json](evals/evals.json) — 13 machine-readable cases.

When the skill misbehaves, add a test case before changing the protocol. Watch for both failure directions: over-triggering on routine work, and under-triggering on high-stakes or explicitly requested reliability work.

## Important Boundaries

- It does not make the AI automatically correct; it makes assumptions, evidence, failures, and recommendations visible enough for a human to judge.
- It is not a substitute for domain expertise, source verification, testing, or code execution.
- It must never override an explicit request for brevity on low-risk tasks.
- It must never expose private identity, account data, secrets, local paths, or confidential project facts.

## License

Apache License 2.0 — see [LICENSE](LICENSE).

## Core Philosophy

> Process reliability creates result reliability.

`mregg-skill` does not promise the AI is always right. It forces the collaboration process to become visible enough for a human to judge.
