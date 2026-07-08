---
name: weekly-pr-update
description: >
  StudioHawk digital PR client updates, end to end. Use when a user says things like "set up
  StudioHawk PR updates", "get started with weekly PR updates", "draft the weekly update for a
  brand", "weekly client update", "PR update for a client", "run the Monday client updates", or
  "put together this week's coverage report", or when a scheduled task runs. The first time a
  brand is set up it runs discovery, shows a sample email, offers a no-send test draft, and offers
  to set up a recurring weekly schedule. After that it drafts the update on demand. Pulls coverage
  from the Client Link Tracker and Media Requests Google Sheet, completed and outstanding work
  from the brand's Monday.com board, and context from Slack and Gmail, then creates a Gmail DRAFT
  that a team member reviews and sends. Never sends automatically.
metadata:
  version: "0.2.1"
  author: "StudioHawk"
---

# StudioHawk Weekly PR Update

One skill that takes a team member from first-time brand setup to a ready-to-send draft, and
optionally onto autopilot. Everything it produces is a Gmail **draft** — nothing is ever sent
automatically.

## Say the outcomes upfront

The first time you help a person (or whenever they ask "what does this do"), tell them plainly
what this skill will do, so there are no surprises:

1. **Set up a brand** — find its Slack channel, Monday board, coverage sheet rows, and client contacts once.
2. **Show a sample email** — so they see exactly what a client update will look like.
3. **Optional test draft** — a real Gmail draft to check the flow (no email is sent).
4. **Optional weekly schedule** — drafts appear automatically each week, still never sent.

Then reassure: "Nothing is ever emailed automatically — every update is a draft you review and send."

## Golden rules

1. **Never send.** Only ever create a Gmail *draft*. A human reviews and sends it.
2. **Use action buttons.** For every decision, ask with the AskUserQuestion tool (clear, short
   options, one question at a time) rather than a wall of text. Always allow a free-text option
   so the person can describe something specific.
3. **One brand at a time.** Each interactive run targets one brand. Scheduled runs loop brands.
4. **Cite sources, never fabricate.** Link the Slack messages, Monday items, and sheet rows used.
   If a source is empty for the window, say "nothing this week" rather than inventing content.
5. **Let the person steer.** After showing a draft, they can ask for any change ("shorter",
   "drop the intro", "add a line about X"). Apply it to that draft — no saved preferences needed.

## Routing — decide the mode first

- **Unattended / scheduled run** (no human present) -> go to *Unattended run*. Ask nothing.
- **A brand was named** -> load its config from Google Drive
  `StudioHawk PR Automation / Brand Configs / <brand-slug>.config.json`.
  - Config exists -> go to *Draft an update*.
  - No config yet -> run the *Setup wizard* (first time for this brand).
- **Nothing specific asked** -> use AskUserQuestion to show a menu: "Draft an update now", "Set up
  a new brand", "Set up or change the weekly schedule".

## Setup wizard (first time for a brand)

Read `references/onboarding-flow.md` and follow it stage by stage. In short: welcome and state the
outcomes -> choose the brand -> discover its sources and save a brand config -> build and
**render a sample email in chat** -> offer a no-send test draft -> offer to create a weekly
schedule -> recap what was set up and how to run it again.

## Draft an update (on-demand)

1. **Brand config** — load `StudioHawk PR Automation / Brand Configs / <brand-slug>.config.json`.
   If missing, run the setup wizard first.
2. **Reporting window** — the previous 7 days ending today unless the user says otherwise. Record
   exact start/end dates and scope every source query to them.
3. **Gather data** — coverage from the `[NEW] Client Link Tracker & Media Requests` sheet;
   completed and outstanding work from the brand's Monday.com board; context from Slack and Gmail.
   See `references/report-template.md` for what maps into each section.
4. **Compose** — follow the default structure in `references/report-template.md`. Keep it warm,
   concise, and client-appropriate. If a `my-writing-style` skill is available, apply it for voice.
5. **Create the Gmail draft (never send)** — addressed to the client recipient(s) in the config,
   subject `<Brand> — Weekly PR Update (w/e <week-ending date>)`. If the config marks the client
   address "unverified", draft to the internal owner instead and flag it.
6. **Report back** — brand, window, a short summary (coverage count, tasks completed, client
   action items), the draft subject, and links to the key sources used. Remind them they can ask
   for any tweak before sending.

## Set up or change the schedule

Do **not** build scheduling logic in this skill. When the user opts in, hand off to Cowork's
built-in scheduling skill (the `/schedule` skill). First confirm timing with action buttons
(default **Mondays 9:00 AM AEST**), then create a recurring task with:

- **Cron (local time):** `0 9 * * 1` (Monday 9:00 AM; the machine's timezone should be
  Australia/Sydney for AEST). Adjust if the user picked a different day/time.
- **Scope:** all brands with a saved config in `StudioHawk PR Automation / Brand Configs`.
- **Prompt for the task:** "Run the StudioHawk weekly-pr-update skill unattended for every brand
  with a saved config. Draft each update as a Gmail DRAFT and never send. Report the brands
  processed, the coverage/tasks/action-item counts, and the draft subject lines."

Confirm afterward: the day/time/timezone, which brands are covered, and that output appears as
Gmail drafts awaiting review. Remind them nothing is sent automatically.

## Unattended run (scheduled)

When triggered by a scheduled task, ask **no** questions. For each brand with a saved config,
run *Draft an update* and create a Gmail draft. Produce one short run report: brands processed,
per-brand counts, draft subjects, and anything skipped (e.g. a brand with no config yet).

## Data sources

| Source | Used for |
| --- | --- |
| Google Sheet `[NEW] Client Link Tracker & Media Requests` | Coverage secured in the window |
| Monday.com board (brand-specific) | Work completed, in-progress, and client-blocked items |
| Slack (brand channel) | Confirmations, context, colour |
| Gmail (brand label/threads) | Open client asks, approvals, recipient contacts |

## Reference files

- `references/onboarding-flow.md` — the first-time setup wizard, stage by stage, with action-button options.
- `references/discovery-playbook.md` — first-run process to identify a brand's sources and build its config.
- `references/brand-config-schema.md` — exact JSON schema for a saved brand config.
- `references/report-template.md` — the default client-update structure and source-to-section mapping.
