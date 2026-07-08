# StudioHawk Plugins

A Claude plugin marketplace for StudioHawk's digital PR and SEO workflows.

## Plugins

### studiohawk-dpr

StudioHawk's digital PR (DPR) workflow automations, bundled as a growing suite of skills. Install
once, connect the shared connectors (Slack, monday.com, Google Drive, Gmail), and every teammate
gets each DPR workflow. New automations are added over time as additional skills in this same
plugin.

Available skills today:

- **weekly-pr-update** — one guided skill that takes a team member from first-time setup to a
  ready-to-send draft: it sets up the brand (discovery), shows a sample email, offers a no-send
  test draft, and offers to set up a weekly schedule via Cowork's built-in `/schedule`. Pulls
  coverage from the "[NEW] Client Link Tracker & Media Requests" Google Sheet, completed and
  outstanding work from the brand's Monday.com board, and context from Slack and Gmail — then
  saves a **Gmail draft** for review. It never sends automatically.

Requires connecting: Slack, monday.com, Google Drive, Gmail (each teammate connects their own
accounts once).

## Install

In Claude Code or the Cowork desktop app, add this marketplace, then install the plugin:

```
/plugin marketplace add darwin403/studiohawk-plugins
/plugin install studiohawk-dpr@studiohawk-plugins
```

After installing, connect the four services when prompted. Then get started:

```
Set up StudioHawk PR updates
```

This runs a guided onboarding (brand setup, sample email, saved format, optional test draft, and
an optional weekly schedule). Afterward, draft anytime with:

```
Draft the weekly PR update for <brand>
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
    ├── skills/                   # weekly-pr-update (setup -> draft -> schedule)
    └── README.md
```
