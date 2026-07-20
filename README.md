# StudioHawk DPR Toolkit

A Claude plugin bundling StudioHawk's digital PR (DPR) workflow automations as a growing set of
skills. Install once, connect the shared connectors (Slack, monday.com, Google Drive, Gmail), and
each teammate gets every DPR workflow. New automations are added over time as additional skills in
this same plugin.

> **New team member?** Start with the [Team Guide (USAGE.md)](USAGE.md) — a plain-English,
> non-technical walkthrough of installing and using the toolkit.

## Skills

### `weekly-client-update`  (available)

One skill that takes a team member from first-time setup all the way to a ready-to-send draft, and
optionally onto autopilot. Everything it produces is a **Gmail draft** — nothing is ever sent
automatically.

The **first time a brand is set up** it runs a guided flow with clickable action buttons:

1. States what it will set up, upfront.
2. **Sets up the brand** — a discovery phase finds the brand's Slack channel, Monday board,
   coverage sheet rows, and Gmail contacts, then saves a reusable config to a shared Google Drive
   folder so the rest of the team benefits.
3. **Shows a sample email** in chat so they see exactly what a client update will look like.
4. Offers a **no-send test draft** in Gmail to confirm the flow.
5. Offers to **set up a weekly schedule** via Cowork's built-in `/schedule` — drafts only.

After that it simply **drafts the update on demand** for the named brand; the user can ask for any
tweak on the spot (shorter, reorder, add a note). Referenced press releases, campaigns, and docs
are hyperlinked and gathered into a **Reference documents** list for the client. When run
**unattended** by a schedule, it loops every configured brand and creates drafts with no prompts.

### `press-release-audit`  (available)

Reviews a press release before it goes for final approval. Triggered on demand by naming a PR
(e.g. "audit the Luxo Living PR"), it finds the review thread in the `dpr-approvals` Slack channel,
opens the linked press-release Google Doc, and classifies the piece as **data-led**, **expert-led**,
or **UGC**. For a data-led piece it searches the brand's Google Drive folder for the **raw data
file** and the **methodology document**, treats those two as the only sources of truth, lists the
methodology's limitations, and flags methodology mismatches, overstated or unsupported claims, wrong
statistics, and out-of-scope claims — each with the exact quote, the source, and a suggested fix
(and it can explain why one item is ranked above another). A single self-sourced stat in an
expert-led/UGC piece does not trigger a demand for a full methodology. For **every** piece it also
runs a **completeness & compliance** check: accompanying pitch, imagery and imagery link, client
quote, expert name/title/headshot, brand tie-in, first-mention client intro, logo in header,
Archivo size-11 formatting, and legal soundness. Findings are reported in **chat only**: it never
edits the doc and never posts to Slack.

### More DPR workflows  (coming)

This plugin is designed to grow. Additional DPR automations will be added as new skills here (e.g.
outreach/pitch tracking, coverage reporting, media-list building). See
[docs/ADDING-WORKFLOWS.md](docs/ADDING-WORKFLOWS.md) for how to add one.

## Connectors

Declared in `.mcp.json`: **Slack**, **monday.com**, **Google Drive**, **Gmail**. Each teammate
connects their own accounts once when prompted:

- **Slack** — to read client channels
- **monday.com** — to read each brand's Master Campaign Management board
- **Google Drive** — to read the coverage sheet and store brand configs
- **Gmail** — to create the draft updates

Shared config location (created automatically on first use):
`Google Drive / StudioHawk PR Automation / Brand Configs / <brand>.config.json`.

## Install

In Claude Code or the Cowork desktop app, add this marketplace, then install the plugin:

```
/plugin marketplace add darwin403/studiohawk-dpr-toolkit
/plugin install studiohawk-dpr-toolkit@studiohawk-dpr-toolkit
```

After installing, connect the four services when prompted. Then get started:

```
Set up StudioHawk PR updates
```

This runs a guided onboarding (brand setup, sample email, saved format, optional test draft, and
an optional weekly schedule). Afterward, draft anytime with:

```
Draft the weekly client update for <brand>
```

See [USAGE.md](USAGE.md) for the full team walkthrough.

## Updating

To pull the latest version after changes are pushed to this repo:

```
/plugin marketplace update studiohawk-dpr-toolkit
```

## Removing

```
/plugin uninstall studiohawk-dpr-toolkit@studiohawk-dpr-toolkit
/plugin marketplace remove studiohawk-dpr-toolkit
```

## Repository layout

This repo is both the marketplace and the single plugin it lists — the plugin lives at the repo
root (the marketplace manifest points its `source` at `.`).

```
studiohawk-dpr-toolkit/
├── .claude-plugin/
│   ├── marketplace.json     # marketplace manifest (lists this plugin, source ".")
│   └── plugin.json          # plugin manifest
├── .mcp.json                # connector declarations (Slack, monday.com, Drive, Gmail)
├── docs/ADDING-WORKFLOWS.md # how to add a new DPR workflow skill
├── skills/                  # weekly-client-update, press-release-audit
├── README.md
└── USAGE.md                 # plain-English team guide
```
