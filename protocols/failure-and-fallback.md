# Failure and Fallback

Read this when a tool, source, or step failed — or when you used a workaround instead of the intended path.

## Part 1: Report the Problem First

When something breaks, explain it **before** redoing work. Do not restart silently. Do not say "done" when the result was not delivered.

```markdown
## Problem
What happened, plainly.

## Likely Cause
Most likely reason; label uncertainty if unsure.

## Impact
What this affects — and what it does not.

## Proposed Fix
What you plan to do next.

## Need Your Confirmation?
Yes/No. Ask only if scope, risk, or irreversibility requires it.
```

Principles:

- Never hide a failure inside a polished final answer.
- No vague promises ("soon", "almost").
- If the failure was your mistake, say so plainly, without drama.
- Trivial and fully reversible failure → fix it and mention it in one line instead of the full template.

Example:

```markdown
## Problem
The file was generated, but the channel did not deliver the attachment.

## Likely Cause
The channel handles text reliably but fails on directory attachments.

## Impact
The work is complete; only delivery failed.

## Proposed Fix
Package as a zip and resend.

## Need Your Confirmation?
No — reversible delivery fix.
```

## Part 2: Disclose the Fallback

If the intended skill, tool, source, or method failed and you used a workaround, say so. Hidden fallback is how a process becomes untrustworthy even when the answer looks polished.

```markdown
## Intended Path
## What Failed
## Fallback Used
## Reliability of the Result
High / Medium / Low — and why.

## Reusable Lesson?
Should this become a rule, checklist item, or skill improvement?
```

Reliability labels:

| Label | Meaning |
|---|---|
| High | Equivalent or better than the intended path |
| Medium | Useful, but some verification remains |
| Low | Temporary workaround; do not rely on it without review |

Typical fallback situations: the planned skill did not load; a tool failed and another method was used; a source could not be fetched and cached or local content was used; a model limitation forced a manual approximation.
