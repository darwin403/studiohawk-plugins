---
name: schedule-weekly-pr-updates
description: >
  Set up (or change) the recurring weekly schedule that auto-drafts StudioHawk digital PR client
  updates. Use when the user says "schedule my weekly PR updates", "automate the Monday client
  updates", "set up the weekly update task", "turn on weekly PR drafts", or wants to change the
  day/time the weekly updates run. Creates a recurring task that, each week, runs the
  weekly-pr-update skill for the user's brands and leaves Gmail drafts for approval.
metadata:
  version: "0.1.0"
  author: "StudioHawk"
---

# Schedule Weekly PR Updates

Create a recurring scheduled task so weekly client-update drafts are ready without anyone
remembering to run them. The task only ever produces Gmail **drafts** — a person still reviews
and sends.

## Defaults

- **When:** Every Monday at 9:00 AM, local time (StudioHawk default: AEST / Australia/Sydney).
  Cron runs in the machine's local timezone, so `0 9 * * 1` = Monday 9:00 AM for a user whose
  computer is set to Australian Eastern time.
- **Scope:** All brands that have a saved config in the shared Drive folder
  `StudioHawk PR Automation / Brand Configs`. If the user has none yet, tell them to run the
  weekly update once per brand first (that creates the config via discovery), or ask which
  specific brand(s) to schedule.

Confirm the day, time, and scope with the user before creating the task. Adjust the cron if they
want a different day/time.

## Create the task

Create a recurring scheduled task with:

- **Schedule (cron, local time):** `0 9 * * 1` (Monday 9:00 AM). Change to match the user's
  request if different.
- **Task id:** `weekly-pr-updates`
- **Prompt:** something equivalent to —

  > For each StudioHawk brand with a saved config in the Google Drive folder
  > "StudioHawk PR Automation / Brand Configs", use the weekly-pr-update skill to draft this
  > week's digital PR client update and save it as a Gmail DRAFT (never send). Report a summary
  > of each brand processed, the coverage/tasks/action-item counts, and the draft subject lines.
  > If any brand has no config yet, skip it and note that discovery is still needed.

If the scheduling tool needs a one-brand-per-task setup instead of a loop, offer to create one
task per brand (e.g. `weekly-pr-updates-<brand-slug>`), each scoped to that brand.

## After creating

Confirm to the user: the schedule (day/time/timezone), which brands are covered, and that output
will appear as Gmail drafts awaiting their review each week. Remind them nothing is ever sent
automatically. Tell them they can re-run this skill anytime to change the timing or scope.
