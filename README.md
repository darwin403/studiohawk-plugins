# StudioHawk Plugins

A Claude plugin marketplace for StudioHawk's digital PR and SEO workflows.

## Plugins

### studiohawk-dpr

StudioHawk's digital PR (DPR) workflow automations, bundled as a growing suite of skills. Install
once, connect the shared connectors (Slack, monday.com, Google Drive, Gmail), and every teammate
gets each DPR workflow. New automations are added over time as additional skills in this same
plugin.

Available skills today:

- **weekly-pr-update** — drafts a weekly digital PR client update for a brand. Pulls coverage from
  the "[NEW] Client Link Tracker & Media Requests" Google Sheet, completed and outstanding work
  from the brand's Monday.com board, and context from Slack and Gmail — then saves a **Gmail
  draft** for a team member to review and send. It never sends automatically. The first run for a
  brand runs a discovery phase and saves a reusable brand config to a shared Google Drive folder.
- **schedule-weekly-pr-updates** — sets up the recurring Monday 9:00 AM AEST run that auto-drafts
  weekly updates for every brand with a saved config.

Requires connecting: Slack, monday.com, Google Drive, Gmail (each teammate connects their own
accounts once).

## Install

In Claude Code or the Cowork desktop app, add this marketplace, then install the plugin:

```
/plugin marketplace add darwin403/studiohawk-plugins
/plugin install studiohawk-dpr@studiohawk-plugins
```

After installing, connect the four services when prompted. Then try:

```
Draft the weekly PR update for <brand>
```

To automate it:

```
Schedule my weekly PR updates
```

## Updating

To pull the latest version after changes are pushed to this repo:

```
/plugin marketplace update studiohawk-plugins
```

## Repository layout

```
studiohawk-plugins/
├── .claude-plugin/
│   └── marketplace.json          # marketplace manifest (lists the plugins)
└── studiohawk-dpr/               # the DPR workflow suite plugin
    ├── .claude-plugin/plugin.json
    ├── .mcp.json                 # connector declarations
    ├── docs/ADDING-WORKFLOWS.md  # how to add a new DPR workflow skill
    ├── skills/                   # weekly-pr-update, schedule-weekly-pr-updates
    └── README.md
```
