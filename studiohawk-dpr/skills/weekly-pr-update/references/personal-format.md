# Personal email format (per user)

Each team member has ONE saved format that applies to ALL their client updates across every
brand, so their drafts always read the way they want without re-specifying it each time. Brand
configs are shared across the team; the personal format is private to each user.

## Where it's stored

Google Drive: `StudioHawk PR Automation / User Preferences / <user-slug>.format.md`

- `<user-slug>` is derived from the team member's connected Gmail address
  (e.g. `jane.doe@studiohawk.com.au` -> `jane-doe`). This keeps each person's format separate even
  though everyone shares the same brand configs.
- Create the `User Preferences` folder the first time it is needed.

## What it contains

A short markdown spec the drafter reads before composing. Suggested fields:

- **Greeting** — e.g. "Hi <first name>," vs "Hello <first name>,".
- **Sections** — which sections to include and in what order (coverage, work completed, in
  progress, action items), and any to always omit.
- **Tone and length** — warm/formal/concise, and roughly how long.
- **Sign-off and signature** — closing line and signature block.
- **Phrases** — anything to always or never say.
- **Subject line pattern** — default `<Brand> — Weekly PR Update (w/e <date>)`.

Keep it human-readable; it is guidance for drafting, not code.

## How it's created and updated

- **Created** during onboarding, right after the person approves the sample email (Stage 5 of
  `onboarding-flow.md`).
- **Updated** anytime the person says "change my email format": load the current format, show a
  fresh sample using it, apply their changes with action buttons, and re-save.

## How it's applied

When drafting for any brand, load this file and follow it. If a `my-writing-style` skill is also
available, apply that for voice on top of these structural preferences. If no personal format
exists yet, fall back to the default structure in `report-template.md`.
