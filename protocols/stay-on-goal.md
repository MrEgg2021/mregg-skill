# Stay on Goal

Read this when a long task may have drifted from the original goal, or the user gave feedback on earlier work.

## Part 1: Goal Recalibration

Use when a task has become long, layered, or multi-turn; when new constraints or side topics appeared; or when the user says "pause", "are we still on track", "this is going off track".

Do **not** stop to recalibrate in short, single-step, low-risk tasks. If alignment is obvious, continue silently.

Pattern:

```markdown
## Original Goal
## Current Direction
## Drift Check
- Still aligned: ...
- Possible drift: ...
## Recommendation
Continue / adjust / pause and ask.
```

Rules:

- Compare against the **user's stated goal**, not your preferred structure.
- If alignment is clear, say so in one line and proceed.
- If alignment is unclear and the next step is costly or irreversible, ask before continuing.
- If the goal itself changed, name the change and update working assumptions.

Example:

```text
We started by choosing a license, but the discussion moved into brand control. Related, but not the same goal. Recommend: finish the license decision now, handle trademark separately.
```

## Part 2: Revising From Feedback

Use when the user asks to revise, says part of the answer was good but another part wrong, or requests a complete replacement.

Rules:

- **Keep what is still valid.** Never throw away useful work because one part was wrong.
- Apply the feedback exactly: keep / change / remove / add.
- Do not defend the old answer unless there is a real factual conflict.
- If the previous answer contained unsupported claims, remove or mark them during the revision.
- If the user asked for a complete replacement, output a standalone version — never "same as above" fragments.
- If the feedback changes the goal itself, run Part 1 first.

For a small edit, silently apply the feedback. For a larger revision, confirm the plan in one line before the output:

```text
Keeping the decision table, removing the over-broad recommendation, adding the missing failure cases. Revised version below.
```

Common failure to avoid: rewriting everything in a new style and losing the one part the user wanted to keep.
