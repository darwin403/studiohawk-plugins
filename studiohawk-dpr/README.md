# StudioHawk DPR

A Cowork plugin bundling StudioHawk's digital PR (DPR) workflow automations as a growing set of
skills. Install once, connect the shared connectors (Slack, monday.com, Google Drive, Gmail), and
each teammate gets every DPR workflow. New automations are added over time as additional skills in
this same plugin.

## Skills

### `weekly-pr-update`  (available)

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
tweak on the spot (shorter, reorder, add a note). When run **unattended** by a schedule, it loops
every configured brand and creates drafts with no prompts.

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

- Get started: "Set up StudioHawk PR updates" → runs the guided setup.
- Draft one brand now: "Draft the weekly PR update for <brand>."
- Add another brand: "Set up a new brand."
- Tweak a draft: just ask (e.g. "make it shorter", "drop the intro line").
- Automate it: during setup (or "set up the weekly schedule") it hands off to Cowork's
  `/schedule` to create Monday 9:00 AM AEST drafts for every brand with a saved config.

## Notes

- Nothing is ever sent automatically — output is always a Gmail draft awaiting approval.
- If a client email address hasn't been verified, the draft is addressed to the managing team
  member instead, and flagged.
- The plugin never fabricates coverage, metrics, or dates; empty sources are reported as such.
