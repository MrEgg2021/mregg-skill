# Compatibility

`mregg-skill` is a plain Agent Skills bundle, designed for the lowest common denominator across AI tools.

## Portable Baseline

- Root folder named `mregg-skill`, matching the `name` field.
- `SKILL.md` is the canonical entry point and is **self-sufficient**: a tool (or a weaker model) that reads only SKILL.md gets correct basic behavior. Protocol files add depth, not required context.
- YAML frontmatter contains `name` and `description`. Optional fields (`license`, `metadata`) are ignored by tools that do not understand them.
- All supporting files are Markdown or JSON. No scripts, binaries, network access, credentials, local paths, or runtime dependencies.

## Designed for Weaker Models Too

This skill may be loaded by agents far less capable than frontier models. That drives three design rules:

1. **Decision tables over prose.** Trigger and clarify decisions are "first matching row wins" tables, not judgment-heavy paragraphs.
2. **SKILL.md self-sufficiency.** A model that never opens `protocols/` still behaves acceptably.
3. **Few files, single-purpose.** Five protocol files with disjoint "read when" conditions, so a weak router can pick the right one.

## Per-Tool Notes

| Tool | How it loads skills | Notes |
|---|---|---|
| Claude Code | `~/.claude/skills/<name>/SKILL.md`, auto-triggered from `description` | Re-copy the folder after each update; installed copies do not auto-sync |
| Claude.ai / Desktop | Skills upload (zip) | Zip the folder itself (see Packaging); description length is capped — keep it lean |
| OpenAI-style agents | `agents/openai.yaml` metadata if understood; otherwise SKILL.md as plain instructions | `allow_implicit_invocation: true` matches the medium-trigger policy: scenario triggering is allowed, but the description's "Do not trigger" list still applies |
| Other Agent Skills tools (Cursor, Windsurf, qoder, workbuddy, …) | Usually folder + SKILL.md | If a tool has no skill system, paste SKILL.md as a system/custom instruction — it works standalone |

## Description Constraints

- Start with what it is, then "Trigger when…", then "Do not trigger…".
- Describe when to load the skill, not the whole workflow.
- Personal names are invocation handles, never the primary trigger.
- Keep it under ~600 characters; some tools cap description length.

## Naming

- Canonical machine id: `mregg-skill` (lowercase, hyphenated — required by most skill systems).
- Public alias: **MrEgg.skill**. Never rename the folder to the alias; dots and uppercase break some loaders.

## Packaging

Zip the folder, not its contents:

```text
mregg-skill.zip
└── mregg-skill/
    ├── SKILL.md
    └── ...
```

Most installers expect the archive to expand into a skill folder.

## Privacy for Public Release

- Aliases stay as invocation handles only.
- No biography, client details, account names, secrets, case details, or local machine paths.
- Examples stay generic unless a user explicitly provides public sample content.
