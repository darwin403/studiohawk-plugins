# Adding a new DPR workflow

`studiohawk-dpr` is designed to grow. Each digital PR workflow lives as its own **skill** inside
this one plugin, so teammates get every new workflow automatically the next time the marketplace
updates. This guide explains how to add one.

## 1. Create the skill folder

Add a new folder under `skills/` named in kebab-case after the workflow, with a `SKILL.md` inside:

```
studiohawk-dpr/
└── skills/
    └── <your-workflow-name>/
        ├── SKILL.md
        └── references/            # optional, for progressive disclosure
```

Keep the folder name short and action-oriented (e.g. `outreach-tracking`, `coverage-report`,
`media-list-builder`).

## 2. Write SKILL.md

`SKILL.md` needs YAML frontmatter with a `name` and a `description`, followed by the instructions:

```markdown
---
name: your-workflow-name
description: >-
  Third-person description that tells Claude WHEN to use this skill. Include the natural phrases a
  teammate would actually say, e.g. "build a media list for <brand>", "track outreach for
  <brand>". Mention the sources it reads (Slack, Monday.com, Google Drive, Gmail) and the output
  it produces.
---

# Your workflow name

Step-by-step instructions Claude follows when the skill runs...
```

Guidelines for the description:

- Write it in the **third person** ("Draft…", "Build…", "Track…") — it is how the model decides to
  trigger the skill, not a slash command label.
- Lead with trigger phrases teammates will actually type.
- Name the connectors and the concrete deliverable.
- **Keep the frontmatter `description` parser-safe:** no `&`, no angle brackets `< >`, and no
  square brackets `[ ]`. The plugin directory's frontmatter parser chokes on these and silently
  skips the whole skill (it just won't appear in the available skills list). Use plain words
  instead — write "for a brand" rather than `<brand>`, and spell out sheet/board names without
  brackets. These characters are fine in the SKILL.md **body** and in `references/`, just not in
  the frontmatter description. (This has bitten two skills already.)

Guidelines for the body:

- Reuse the existing patterns: load a brand config first, gather data, draft, then produce output.
- **Never send anything automatically** — every client-facing output is a draft awaiting approval.
- Never fabricate coverage, metrics, or dates; report empty sources as empty.
- Cite the source (sheet row, Monday item, Slack message, Gmail thread) for anything you assert.

## 3. Reuse the shared brand config

Brand configs already live in Google Drive at
`StudioHawk PR Automation / Brand Configs / <brand-slug>.config.json` (see
`skills/weekly-pr-update/references/brand-config-schema.md`). New workflows should read the same
config so a brand only has to be discovered once. If your workflow needs extra per-brand fields,
add them to that schema rather than creating a second config file.

## 4. Keep references small

Put long lookup material (playbooks, schemas, templates) in a `references/` subfolder and point to
it from `SKILL.md`. This keeps the always-loaded skill body short and lets Claude pull detail in
only when needed.

## 5. Update docs and ship

- Add the new skill to the plugin `README.md` "Skills" list and to the marketplace `README.md`.
- Bump the `version` in `.claude-plugin/plugin.json` and in the marketplace entry if you want a
  clean update signal.
- Commit and push. Teammates pick it up with `/plugin marketplace update studiohawk-plugins`.

## Connectors

If a new workflow needs a service that isn't already declared, add it to `.mcp.json` (an `http`
entry with its MCP `url`). Teammates will be prompted to connect the new service the next time they
run a skill that needs it. Don't remove or rename the existing four connectors — Slack, monday.com,
Google Drive, and Gmail are shared by every workflow.
