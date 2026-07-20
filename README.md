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
[studiohawk-dpr-toolkit/docs/ADDING-WORKFLOWS.md](studiohawk-dpr-toolkit/docs/ADDING-WORKFLOWS.md) for how to add one.

## Connectors

Declared in `.mcp.json`: **Slack**, **monday.com**, **Google Drive**, **Gmail**. Each teammate
adds all four upfront in the desktop app under **Customize → Connectors** (their own accounts, once):

- **Slack** — to read client channels
- **monday.com** — to read each brand's Master Campaign Management board
- **Google Drive** — to read the coverage sheet and store brand configs
- **Gmail** — to create the draft updates

Shared config location (created automatically on first use):
`Google Drive / StudioHawk PR Automation / Brand Configs / <brand>.config.json`.

## Install

Everything is done in the **Claude desktop app** — no CLI. See [USAGE.md](USAGE.md) for the full,
illustrated team walkthrough.

1. **Add connectors** — open **Customize → Connectors** in the sidebar and add **Slack**,
   **Gmail**, **Google Drive**, and **monday.com**, signing in with your StudioHawk accounts.
2. **Add the plugin** — open **Customize → Plugins**, and in **Personal plugins** click
   **"+" → Add marketplace → Add from a repository**, then paste the repo URL:

   ```
   https://github.com/darwin403/studiohawk-dpr-toolkit
   ```

   Then click **Browse plugins** and **Install** `studiohawk-dpr-toolkit`.

That's it — the toolkit is installed and ready to use.

## Using the skills

You now have two skills in your chat, each with its own slash command. Start a **Cowork chat**
(select **Cowork** in the message box), begin with the slash command, and ask in plain English —
brand setup and discovery are handled under the hood.

- **Weekly client update** — `/weekly-client-update`

  ```
  /weekly-client-update draft this week's update for <brand>
  ```

- **Press release audit** — `/press-release-audit`

  ```
  /press-release-audit check the <brand> press release
  ```

See [USAGE.md](USAGE.md) for the full, plain-English walkthrough of each skill.

## Updating

Open **Customize → Plugins** in the desktop app, find the **studiohawk-dpr-toolkit** marketplace,
and click **Update** to pull the latest version.

## Removing

Open **Customize → Plugins**, then **Uninstall** the **studiohawk-dpr-toolkit** plugin — or remove
its marketplace entirely to delete the source.

## Repository layout

This repo is the marketplace at its root; the plugin it lists lives in a same-named subfolder
(the marketplace manifest points its `source` at `./studiohawk-dpr-toolkit`). The marketplace and
plugin manifests are kept in separate `.claude-plugin/` directories — required for the desktop app
to sync the marketplace.

```
.claude-plugin/
└── marketplace.json             # marketplace manifest (lists the plugin below)
studiohawk-dpr-toolkit/          # the plugin (source: ./studiohawk-dpr-toolkit)
├── .claude-plugin/
│   └── plugin.json              # plugin manifest
├── .mcp.json                    # connector declarations (Slack, monday.com, Drive, Gmail)
├── docs/ADDING-WORKFLOWS.md     # how to add a new DPR workflow skill
└── skills/                      # weekly-client-update, press-release-audit
README.md
USAGE.md                         # plain-English team guide
```
