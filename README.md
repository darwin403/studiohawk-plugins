# StudioHawk Plugins

A Claude plugin marketplace for StudioHawk's digital PR and SEO workflows.

## Plugins

### studiohawk-weekly-pr-updates

Drafts weekly digital PR client updates. For a given brand, it pulls coverage from the
"[NEW] Client Link Tracker & Media Requests" Google Sheet, completed and outstanding work from
the brand's Monday.com board, and context from Slack and Gmail — then saves a **Gmail draft** for
a team member to review and send. It never sends automatically. The first run for a brand runs a
discovery phase and saves a reusable brand config to a shared Google Drive folder.

Requires connecting: Slack, monday.com, Google Drive, Gmail (each teammate connects their own
accounts once).

## Install

In Claude Code or the Cowork desktop app, add this marketplace, then install the plugin:

```
/plugin marketplace add darwin403/studiohawk-plugins
/plugin install studiohawk-weekly-pr-updates@studiohawk-plugins
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
└── studiohawk-weekly-pr-updates/ # the plugin
    ├── .claude-plugin/plugin.json
    ├── .mcp.json                 # connector declarations
    ├── skills/                   # weekly-pr-update, schedule-weekly-pr-updates
    └── README.md
```
