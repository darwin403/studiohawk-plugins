# StudioHawk Weekly PR Updates

A Cowork plugin that drafts weekly digital PR client updates for StudioHawk. It pulls coverage,
completed work, and outstanding items from Slack, Monday.com, Google Drive, and Gmail, then saves
a **Gmail draft** for a team member to review and send. It never sends email automatically.

## What it does

Every week (or on demand), for a given brand/client, it:

1. Loads the brand's saved config — or, on the first run for a brand, runs a **discovery phase**
   that finds the brand's Slack channel, Monday board, coverage sheet rows, and Gmail contacts,
   then saves a reusable config to a shared Google Drive folder so the rest of the team benefits.
2. Gathers the week's data: coverage from the **"[NEW] Client Link Tracker & Media Requests"**
   Google Sheet, completed and outstanding tasks from the brand's **Monday.com** board, and
   context from **Slack** and **Gmail**.
3. Drafts a client-ready update (coverage achieved, work completed, in progress, action items).
4. Saves it as a **Gmail draft** for approval. A person reviews and hits send.

## Components

- **Skill: `weekly-pr-update`** — the core workflow (discovery + gather + draft + Gmail draft).
- **Skill: `schedule-weekly-pr-updates`** — sets up the recurring Monday 9:00 AM AEST run.
- **Connectors (`.mcp.json`)** — Slack, monday.com, Google Drive, Gmail.

## Setup

After installing the plugin, connect the four services when prompted (each teammate connects
their own accounts — this is a one-time per-person login):

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
