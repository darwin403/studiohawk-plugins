# Brand Config Schema

Each brand has one JSON config file stored in the shared Google Drive folder
`StudioHawk PR Automation / Brand Configs`, named `<brand-slug>.config.json`. This is the single
source of truth the weekly-update skill reads on every run. Keep it current.

## Schema

```json
{
  "brand_slug": "acme-foods",
  "brand_name": "Acme Foods",
  "owner": {
    "name": "Jane Marketer",
    "email": "jane@studiohawk.com.au"
  },
  "client_recipients": [
    { "name": "Sam Client", "email": "sam@acmefoods.com", "status": "verified" }
  ],
  "slack": {
    "channels": [
      { "name": "client-acme-foods", "id": "C0123ABCD", "private": false }
    ]
  },
  "monday": {
    "board_id": "1234567890",
    "board_name": "Master Campaign Management - Acme Foods",
    "active_groups": ["Current Campaigns"],
    "status_column": "status",
    "done_values": ["Done", "Complete"],
    "blocked_values": ["Stuck", "Blocked"],
    "waiting_on_client_values": ["Waiting on client", "Client review"]
  },
  "coverage_sheet": {
    "name": "[NEW] Client Link Tracker & Media Requests",
    "file_id": "1AbC...xyz",
    "link": "https://docs.google.com/spreadsheets/d/1AbC...xyz",
    "brand_tab": "Acme Foods",
    "filter_column": null,
    "filter_value": null,
    "columns": {
      "outlet": "Publication",
      "headline": "Anchor Text",
      "url": "Live Link",
      "link_type": "Link Type",
      "domain_authority": "DA",
      "date": "Date Live"
    }
  },
  "gmail": {
    "label": "Clients/Acme Foods",
    "contacts": ["sam@acmefoods.com"]
  },
  "campaign_docs": [
    { "name": "Master Campaign Management - Acme Foods", "link": "https://..." }
  ],
  "reporting": {
    "timezone": "Australia/Sydney",
    "window_days": 7
  },
  "notes": "Client prefers Friday send; only report follow + no-follow links, skip syndications.",
  "last_updated": "2026-07-08",
  "last_run": null
}
```

## Field notes

- `brand_slug` — lowercase, hyphenated; must match the file name.
- `client_recipients[].status` — `"verified"` or `"unverified"`. If any intended recipient is
  `"unverified"`, the skill drafts to the `owner` instead and flags it.
- `monday.done_values` / `blocked_values` / `waiting_on_client_values` — the actual status label
  strings on that board, used to classify items into completed vs outstanding vs client-action.
- `coverage_sheet.brand_tab` OR (`filter_column` + `filter_value`) — use whichever isolates this
  brand's rows. Leave the unused one `null`.
- `coverage_sheet.columns` — maps friendly field names to the actual column headers in the sheet.
- `notes` — free-text, brand-specific quirks worth honouring in the draft.
- `last_updated` / `last_run` — ISO dates; update `last_run` after each successful draft.

Keep the file valid JSON. When editing, read it, modify, and write the whole file back.
