# Setup wizard (first time for a brand)

Goal: take a team member from zero to a configured brand, a sample they can see, an optional test
draft, and an optional weekly schedule — using clear action buttons at every step. Nothing is
ever sent.

**How to ask:** use the AskUserQuestion tool for each decision. Keep options short and concrete
(2-4 per question), one question at a time, and always leave room for a free-text answer so the
person can describe something specific. Wait for their choice before moving on.

## Stage 1 — Welcome and outcomes

Greet the person and state, in a few lines, what this will set up (see "Say the outcomes upfront"
in SKILL.md) and the never-send promise. Then continue — no question needed.

## Stage 2 — Choose the brand

Ask which brand/client to set up. If they already named one, skip this.

- **Question:** "Which brand should we set up?"
- **Options:** any brand names you can detect from their Slack channels or Monday boards, plus a
  free-text option "Type the brand name".

## Stage 3 — Discover the brand's sources

Run discovery per `discovery-playbook.md`: find the brand's Slack channel, Monday board, its rows
in the `[NEW] Client Link Tracker & Media Requests` sheet, Gmail label/contacts, and the client
recipient(s). If anything is ambiguous (e.g. two possible channels), confirm with an action-button
question before saving. Save the brand config using `brand-config-schema.md`. Briefly tell the
person what you found so setup is observable.

## Stage 4 — Build and show a sample email

Gather this week's data for that brand and compose a full sample update using the default
structure in `report-template.md`. **Render the complete sample in chat** — subject line and body
— so the person sees exactly what a client update looks like. Label it clearly as a SAMPLE
(not saved, not sent). If a source is empty for the window, show the honest "nothing this week"
handling rather than inventing content. Let them know they can ask for any change now or on any
future draft (e.g. shorter, drop a section, add a line) — no setup required.

## Stage 5 — Optional test draft (no send)

- **Question:** "Want me to create a real test draft in Gmail now? No email is sent."
- **Options:** "Yes, create a test draft", "Skip for now".

If yes: create the Gmail draft for this brand. For a safe test, address it to the team member
(the internal owner), not the client, unless they say otherwise. Confirm it is sitting in their
Gmail Drafts and tell them the subject line.

## Stage 6 — Optional weekly schedule

- **Question:** "Set up an automatic weekly schedule? Drafts only — never sent."
- **Options:** "Yes — Mondays 9 AM AEST", "Pick a different day/time", "Not now".

If yes: hand off to Cowork's built-in scheduling skill (the `/schedule` skill) with the recurring
instruction described in SKILL.md ("Set up or change the schedule"). If they pick a different
day/time, adjust the cron accordingly before creating the task.

## Stage 7 — Recap

Summarize what is now set up: the brand configured, whether a test draft was created, and whether
a schedule was set. Then tell them how to use it going forward:

- Draft anytime: "draft the weekly update for <brand>".
- Add another brand: "set up a new brand".
- Adjust any draft on the fly by just asking (shorter, reorder, add a note, etc.).
