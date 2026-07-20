---
name: press-release-audit
description: StudioHawk press-release fact-check and audit. Use when a user says things like "audit the press release for a brand", "fact-check the press release", "review the press release before approval", or "check the PR in dpr-approvals". Works from the review thread the team posts in the Slack dpr-approvals channel (titled like "Luxo Living PR for review" with a Google Doc link). It reads the press-release Google Doc and classifies the piece as data-led, expert-led, or UGC. For data-led pieces it searches the brand's Google Drive folder for the underlying data file and methodology document and treats those two as the only sources of truth, flagging methodology mismatches, overstated or unsupported claims, wrong statistics, and out-of-scope claims (and can explain any ranking on request). For every piece it also runs a completeness and compliance check covering the accompanying pitch, imagery and imagery link, client quote, expert name/title/headshot, brand tie-in, first-mention client intro, logo in header, Archivo size-11 formatting, and legal soundness. Findings are reported in chat only. It never edits the doc, and never posts to Slack automatically.
---

# StudioHawk Press-Release Audit

Reviews a press release before it goes for final approval on two tracks: a **fact-check** of any
data claims against the two things that can actually back them up — the **raw data file** and the
**methodology document** — and a **completeness & compliance** check of the release package itself
(pitch, imagery, client quote, expert credits, brand tie-in, formatting, logo, legal soundness).
Output is **chat only**: the reviewer makes the corrections and submits.

## What this does (say it upfront)

The first time you help someone, or when they ask "what does this do", state it plainly:

1. **Find the PR** — locate the review thread in the `dpr-approvals` Slack channel, open the linked
   press-release Google Doc, and note the accompanying assets (pitch, imagery).
2. **Classify the piece** — is it **data-led** (built on a dataset/ranking), **expert-led** (built
   on expert commentary), or **UGC**? This decides whether the data + methodology fact-check applies.
3. **Fact-check (data-led)** — for data-led pieces, find the raw data file and methodology in the
   brand's Drive folder, treat those two as the *only* sources of truth, list the methodology's
   limitations, then flag anything that mismatches, overstates, miscounts, or goes out of scope.
   A single self-sourced stat in an expert-led/UGC piece does **not** require a full methodology.
4. **Completeness & compliance (every piece)** — run `references/completeness-checklist.md`: pitch,
   imagery + link, client quote, expert name/title/headshot, brand tie-in, first-mention intro,
   logo in header, Archivo size-11 formatting, and legal soundness.
5. **Report in chat** — flagged lines with the exact fix, or an explicit all-clear. The reviewer
   applies changes and submits for approval.

## Golden rules

1. **Two sources of truth only (for data claims).** When fact-checking a data-led piece, the data
   file and the methodology document are the only sources — do **not** use outside knowledge,
   training data, or assumptions, and if a claim can't be verified from those two files, say so
   explicitly rather than guessing. But **match the rigour to the piece**: only demand a raw data
   file + methodology when the campaign is genuinely **data-led**. An expert-led or UGC piece that
   just cites a single self-sourced stat should not be flagged for lacking a full methodology —
   note the stat needs a source, don't send the reviewer hunting for a dataset that was never built.
2. **Limitations before flags.** Always list what the methodology actually measured, excluded, and
   weighted *before* judging any claim. Every flag is measured against that scope.
3. **Never fabricate, always cite.** Quote the exact PR line, cite what the data/methodology says,
   and give the source (cell/tab, methodology section). Recalculate figures rather than trusting
   the PR's numbers.
4. **Read-only and chat-only.** Never edit the Google Doc, never post to Slack, never send
   anything. You only report findings in the conversation.
5. **Confirm ambiguous sources.** If you can't confidently identify the data file, the correct
   tab, or the methodology doc, ask with `AskUserQuestion` rather than picking one silently — the
   whole audit is only as trustworthy as the files it runs on.

## Flow

### 1. Locate the press release
The user names a PR (e.g. "audit the Luxo Living PR"). Find its review thread in the
`dpr-approvals` Slack channel and extract the press-release Google Doc link, then read the doc.
Note any accompanying assets on the thread/doc (pitch, imagery). Follow
`references/source-discovery.md` §1–2.

### 2. Classify the piece
Decide whether it's **data-led** (built on a dataset, ranking, or index), **expert-led** (built on
expert commentary/quotes), or **UGC**. This gates the next step: only data-led pieces need the raw
data file + methodology. If the type is genuinely ambiguous, confirm with `AskUserQuestion`.
Follow `references/source-discovery.md` §3.

### 3. Locate the evidence in Google Drive (data-led)
For a data-led piece, search the brand's Drive folder for the **raw data file** (Excel/CSV/Google
Sheet) and the **methodology document** (Word/PDF/Doc). Confirm the right file, and the right
**tab**, when there is any doubt — old, duplicate, or working tabs are common. Follow
`references/source-discovery.md` §4–5. Skip this for expert-led/UGC pieces; a single cited stat
just needs a source, not a full dataset.

### 4. Run the audit — two tracks
- **Fact-check (data-led):** read PR + data + methodology and work through
  `references/audit-checklist.md` — list the methodology limitations first, then flag issues across
  the four categories with a quote, the source, and a suggested correction.
- **Completeness & compliance (every piece):** work through
  `references/completeness-checklist.md` — pitch, imagery + link, client quote, expert
  name/title/headshot, brand tie-in, first-mention client intro, logo in header, Archivo size-11
  formatting, and legal soundness.

Report both in chat, in one combined report.

### 5. Explain a ranking (on request)
If a ranking looks off, or the user asks "why is X above Y", follow `references/ranking-analysis.md`
to show the working from the methodology's factors and weightings — using only the data file.

### 6. Wrap up
End with a short recap: which two source files were used, the limitations applied, and the count of
issues found (or a clean bill). Remind the reviewer to tag **Dani, Kiran, or Georgia** on anything
uncertain, and — once corrections are made — to post in the approvals channel and tag **Georgia**,
noting a fact-check against the methodology was completed. You do not post this yourself.

## Data sources

| Source | Used for |
| --- | --- |
| Slack `dpr-approvals` channel | The review thread + the press-release Google Doc link + accompanying assets (pitch, imagery) |
| Press-release Google Doc | The claims being audited + completeness/compliance of the release itself |
| Raw data file (brand Drive folder) | Data-led only: ground-truth figures, rankings, tables — source of truth |
| Methodology document (brand Drive folder) | Data-led only: scope, what was measured/excluded, scoring & weightings — source of truth |

## Reference files

- `references/source-discovery.md` — find the review thread, resolve the PR doc, classify the piece,
  and (for data-led) locate the brand's data file + methodology in Google Drive (with confirmation
  on ambiguity).
- `references/audit-checklist.md` — the fact-check discipline: limitations-first, the four flag
  categories, per-issue format, and the combined chat report layout.
- `references/completeness-checklist.md` — the completeness & compliance checks that run on every
  piece: pitch, imagery + link, client quote, expert credits, brand tie-in, first-mention intro,
  logo, Archivo size-11 formatting, and legal soundness.
- `references/ranking-analysis.md` — how to explain why one item is ranked above another, showing
  the working from methodology factors and weightings.
