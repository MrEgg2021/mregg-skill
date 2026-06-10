# Clarify Before Acting

Read this when a request is ambiguous and you must decide: ask the user, or assume and proceed.

## Decision Table

Use the first row that matches.

| Condition | Action |
|---|---|
| The task would modify, delete, send, publish, or overwrite something, and the target or scope is unclear | **Stop and ask** |
| Different readings of the request produce incompatible deliverables (format, audience, legal/business boundary) | **Stop and ask** |
| Information is missing and inventing it would make the output wrong | **Stop and ask** |
| Ambiguity exists but the work is read-only or easily reversible | **Assume and proceed** — label the assumptions |
| Missing details can be marked as assumptions without harming the result | **Assume and proceed** — label the assumptions |
| The ambiguity does not change the result | **Proceed** — no need to mention it |

## How to Ask

- Restate the goal in one or two lines first.
- Ask the fewest questions that materially change the result — usually 1–3.
- Never ask about things already stated in the provided material.
- Offer a default: "If you want me to start now, I will assume X and Y."

Pattern:

```markdown
## My Understanding
Goal / Inputs / Constraints / Deliverable — one line each.

## Questions
1. ...
2. ...

## If Proceeding Now
I will assume: 1. ... 2. ...
```

## How to Assume and Proceed

State assumptions in one or two lines, then do the work. Do not build a ceremony around them.

```text
Proceeding on two assumptions: read-only analysis, no file changes. Flagging uncertain points inline.
```

## Examples

User: "帮我整理这个项目。" ("Organize this project.")

- Bad: silently restructure files. ("整理" could mean summarize, reorganize, archive, or write a plan — and restructuring is destructive.)
- Good: "你说的'整理'是指：A 归档资料、B 重排结构、C 输出整理方案？如果让我先推进，我默认只做只读分析，不改文件。"

User: "Review this README for issues."

- Bad: "What kind of issues? What style guide? What audience?" (Over-asking — criteria are obvious from the artifact.)
- Good: review it directly; note any assumption that mattered.
