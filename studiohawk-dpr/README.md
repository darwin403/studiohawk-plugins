# StudioHawk DPR

A Cowork plugin bundling StudioHawk's digital PR (DPR) workflow automations as a growing set of
skills. Install once, connect the shared connectors (Slack, monday.com, Google Drive, Gmail), and
each teammate gets every DPR workflow. New automations are added over time as additional skills in
this same plugin.

## Skills

### `weekly-pr-update`  (available)

Drafts a weekly digital PR client update for a brand. For a given brand it:

1. Loads the brand's saved config — or, on the first run for a brand, runs a **discovery phase**
   that finds the brand's Slack channel, Monday board, coverage sheet rows, and Gmail contacts,
   then saves a reusable config to a shared Google Drive folder so the rest of the team benefits.
2. Gathers the week's data: coverage from the **"[NEW] Client Link Tracker & Media Requests"**
   Google Sheet, completed and outstanding tasks from the brand's **Monday.com** board, and
   context from **Slack** and **Gmail**.
3. Drafts a client-ready update (coverage achieved, work completed, in progress, action items).
4. Saves it as a **Gmail draft** for approval — it never sends automatically.

### `schedule-weekly-pr-updates`  (available)

Sets up the recurring Monday 9:00 AM AEST run that auto-drafts weekly updates for every brand with
a saved config.

### More DPR workflows  (coming)

This plugin is designed to grow. Additional DPR automations will be added as new skills here (e.g.
outreach/pitch tracking, coverage reporting, media-list building). See
`docs/ADDING-WORKFLOWS.md` for how to add one.

## Connectors

Declared in `.mcp.json`: **Slack**, **monday.com**, **Google Drive**, **Gmail**. Each teammate
connects their own accounts once when prompted:

- **Slack** — to read client channels
- **monday.com** — to read each brand's Master Campaign Management board
- **Google Drive** — to read the coverage sheet and store brand configs
- **Gmail** — to create the draft updates

Shared config location (created automatically on first use):
`Google Drive / StudioHawk PR Automation / Brand Configs / <brand>.config.json`.

## Usage

- Draft one brand now: "Draft the weekly PR update for <brand>."
- First time for a brand: it runs discovery, confirms what it found, and saves the config.
- Automate it: "Schedule my weekly PR updates" → sets up Monday 9:00 AM AEST drafts for all
  brands that have a saved config.

## Notes

- Nothing is ever sent automatically — output is always a Gmail draft awaiting approval.
- If a client email address hasn't been verified, the draft is addressed to the managing team
  member instead, and flagged.
- The plugin never fabricates coverage, metrics, or dates; empty sources are reported as such.
