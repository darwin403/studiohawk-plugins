---
name: weekly-pr-update
description: >
  Draft a weekly digital PR client update for a StudioHawk brand or client. Use when the user
  says things like "draft the weekly update for a brand", "weekly client update", "PR update
  for a client", "run the Monday client updates", or "put together this week's coverage report",
  or when a scheduled weekly-update task runs. Pulls coverage from the Client Link Tracker and
  Media Requests Google Sheet, completed work and outstanding items from the brand's Monday.com
  board, plus context from the brand's Slack channel and Gmail threads, then creates a Gmail
  DRAFT (never sends) for a team member to review and approve.
metadata:
  version: "0.1.0"
  author: "StudioHawk"
---

# Weekly PR Client Update

Draft a weekly digital PR progress update for a single StudioHawk brand and leave it as a
Gmail **draft** for human approval. Never send email automatically.

## Golden rules

1. **Never send.** Only ever create a Gmail *draft*. A human reviews and sends it.
2. **One brand at a time.** Each run targets one brand/client. If asked to run "all clients",
   loop: run the full process for each brand sequentially.
3. **Config first.** Every brand has a saved config file in the shared Drive folder
   `StudioHawk PR Automation / Brand Configs`. If it exists, load it. If it does NOT exist,
   run the Discovery phase first (see below), then save a config before drafting.
4. **Cite sources.** In the draft's internal notes, keep links back to the Slack messages,
   Monday items, and sheet rows used, so the reviewer can verify quickly.
5. **When unsure, ask.** If the brand can't be identified confidently, or discovery finds
   multiple candidate channels/boards, ask the user to confirm rather than guessing.

## Inputs

Determine the target brand from the user's request (e.g. "draft the weekly update for Acme").
If no brand is given and this is a scheduled run, read the brand list from
`StudioHawk PR Automation / Brand Configs` and process each saved brand.

Establish the reporting window: the previous 7 days ending today, unless the user specifies
otherwise. Record the exact start/end dates and use them in every source query.

## Step 1 — Load or create the brand config

Search Google Drive for the folder `StudioHawk PR Automation / Brand Configs` and a file named
`<brand-slug>.config.json`. (Create the folder the first time it is needed.)

- **Config found** → read it and continue to Step 2.
- **Config not found** → run the **Discovery phase**. Read
  `references/discovery-playbook.md` and follow it end to end. It produces a config that must be
  saved to Drive using the schema in `references/brand-config-schema.md` before continuing.

The config tells you exactly which Slack channel(s), Monday board, Drive sheets/tabs, Gmail
label/contacts, and client recipient(s) belong to this brand — so later runs are fast and
consistent.

## Step 2 — Gather this week's data

Pull from each source using the identifiers in the config. Scope every query to the reporting
window. Read `references/report-template.md` for exactly what maps into each section.

**Coverage achieved** — from the Google Sheet `[NEW] Client Link Tracker & Media Requests`:
read the brand's tab/rows, filter to links/placements secured within the window (published date
or "live" status in the window). Capture: publication/outlet, headline/anchor, URL, link type
(follow/no-follow/brand mention), domain authority if present, and date.

**Tasks completed** — from the brand's Monday.com board: items moved to Done/Complete within the
window, plus notable updates. Also scan the brand's Slack channel for confirmations of pitches
sent, assets delivered, or work signed off.

**Outstanding action items / client requests** — from Monday: items that are in-progress,
blocked, waiting-on-client, or due soon. From Gmail (brand label/thread) and Slack: any open
questions, approvals needed, or requests the client made that are not yet resolved. Clearly
separate "we're working on it" from "we need something from the client".

**Context/colour** — skim the brand's Slack channel and recent Gmail thread for anything that
should be acknowledged (wins to celebrate, issues to flag). Do not include anything sensitive
or internal-only in the client-facing draft.

If a source returns nothing for the window, note "nothing this week" internally rather than
inventing content. Never fabricate coverage, metrics, or dates.

## Step 3 — Draft the update

Compose the client-facing update following `references/report-template.md`. Keep it warm,
concise, and client-appropriate — this is going to an external client. Structure:

1. Short intro line with the reporting week.
2. **Coverage achieved this week** — the wins, with outlet + link.
3. **Work completed** — what the team delivered.
4. **In progress / next steps** — what's underway.
5. **Action items for you** — anything the client needs to review, approve, or provide. Omit
   this section if there are genuinely no client actions.

If a `my-writing-style` skill is available, apply it so the draft matches the team's voice.

## Step 4 — Create the Gmail draft (never send)

Create a Gmail **draft** (do not send) addressed to the client recipient(s) from the config,
with the account owner's usual signature. Subject line format:
`<Brand> — Weekly PR Update (<week ending date>)`.

Leave the recipient as configured, but if the config marks the client email as "unverified",
create the draft addressed to the managing team member instead and note that the client
address needs confirming. When in doubt, draft to the internal owner, not the client.

## Step 5 — Report back to the user

Tell the user: the brand, the reporting window, a 3-4 line summary of what's in the draft
(coverage count, tasks completed count, number of client action items), and confirm the Gmail
draft was created (with its subject). Remind them it is a draft awaiting their review and send.
Provide links to the key sources used.

## Reference files

- `references/discovery-playbook.md` — first-run process to identify a brand's sources and build its config.
- `references/brand-config-schema.md` — exact JSON schema for a saved brand config.
- `references/report-template.md` — the client-update structure and what data maps into each section.
