# Prompt Patterns

Copy-paste prompts for invoking `mregg-skill`, with the behavior each one should produce.

## Invoke

```text
Use mregg-skill.
Use the reliability protocol.
Use MrEgg.skill. I need an auditable process, not only a conclusion.
按旦旦的方法分析。
别脑补，先反问。
```

Expected: a short `Reliability mode:` marker, then the lightest sufficient structure.

## Control Intensity

```text
Use mregg-skill in light mode. Keep it concise.
Use mregg-skill in structured mode for the analysis, then light mode for execution.
Use full audit mode. Include assumptions, evidence, risks, uncertainty, fallback, and a final audit.
```

Expected: the requested level — light stays compact (Conclusion → Assumptions → Output → Quick check); audit ends with a concrete audit result.

## Clarify First

```text
I have not fully defined this requirement. Do not build yet; ask the critical questions first.
Restate your understanding, then ask only the questions that materially change the result.
If you can safely proceed, state your assumptions and continue. If not, stop and ask.
```

Expected: restated goal, the few questions that matter, and a default path ("if proceeding now, I assume…"). No interrogation when the work is reversible.

## Objective Critique

```text
Do not flatter me. Objectively judge what is weak in this idea and why.
If my premise is wrong, say why and what evidence would change your view.
```

Expected: a clear verdict that follows the evidence, weak points named, no motivational filler.

## Evidence Separation

```text
Separate evidence, reasoning, assumptions, and uncertainty. Do not present inference as fact.
Give me sources, observations, or file references for factual claims.
```

Expected: the four categories kept visibly distinct; specific citations; a verification path for uncertain points.

## Option Comparison

```text
Give me three options. For each: pros, cons, downstream effects, risks, best-fit scenario. Then recommend one.
```

Expected: a comparison table plus a recommendation — or an exact statement of what must be verified before choosing. No bare "it depends".

## Failure and Fallback

```text
If you discover a problem, do not silently redo the work. Explain the problem, impact, and proposed fix first.
If the intended tool, source, or skill fails and you use a workaround, disclose it and rate the reliability of the result.
```

Expected: Problem / Likely Cause / Impact / Proposed Fix before any retry; fallbacks disclosed with a High / Medium / Low label.

## Goal Recalibration

```text
Pause and check whether we are still solving the original goal. If we have drifted, explain what changed and recommend the next step.
```

Expected: original goal vs current direction, drift named, a concrete continue/adjust/ask recommendation.

## Revise From Feedback

```text
Revise this using my feedback. Keep the parts that still work, remove the parts that do not, and give me a complete replacement.
```

Expected: keep/change/remove/add applied exactly; valid prior work preserved; output is standalone, not a fragment.

## Explain a Concept

```text
Explain this with a familiar analogy, then say where the analogy becomes inaccurate.
```

Expected: plain explanation, bounded analogy, explicit statement of where the analogy breaks.

## Edge Note

```text
At the end, add one short edge note with an overlooked boundary or useful adjacent detail — only if it genuinely helps.
```

Expected: at most one short, useful note; nothing if it would be decorative.

## Audit a Deliverable

```text
Audit this deliverable before calling it done. Check missing requirements, weak evidence, hidden assumptions, privacy leakage, and undisclosed fallbacks.
```

Expected: the deliver-and-audit checklist applied, concrete issues listed, completion claimed only if the audit passes.

## Combine With Domain Skills

```text
Use the PDF extraction skill to read the file, then use mregg-skill to audit the extracted findings and uncertainty.
```

Expected: the domain skill does the work; mregg-skill adds the reliability layer on top.
