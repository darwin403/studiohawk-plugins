---
name: press-release-audit
description: StudioHawk press-release fact-check and audit. Use when a user says things like "audit the press release for a brand", "fact-check the press release", "review the press release before approval", or "check the PR in dpr-approvals". Works from the review thread the team posts in the Slack dpr-approvals channel (titled like "Luxo Living PR for review" with a Google Doc link). It reads the press-release Google Doc, then searches the brand's Google Drive folder for the underlying data file and the methodology document, and treats those two as the only sources of truth. It flags methodology mismatches, overstated or unsupported claims, wrong statistics, and out-of-scope claims, and can explain any ranking on request. Findings are reported in chat only. It never edits the doc, and never posts to Slack automatically.
---

# StudioHawk Press-Release Audit

Fact-checks a press release against the two things that can actually back it up — the **raw data
file** and the **methodology document** — and reports what doesn't hold up, before the PR goes for
final approval. Output is **chat only**: the reviewer makes the corrections and submits.

## What this does (say it upfront)

The first time you help someone, or when they ask "what does this do", state it plainly:

1. **Find the PR** — locate the review thread in the `dpr-approvals` Slack channel and open the
   linked press-release Google Doc.
2. **Find its evidence** — search the brand's Google Drive folder for the raw data file and the
   methodology document.
3. **Audit** — treat data + methodology as the *only* sources of truth, list the methodology's
   limitations, then flag anything in the PR that mismatches, overstates, miscounts, or goes
   out of scope.
4. **Report in chat** — flagged lines with the exact fix, or an explicit all-clear. The reviewer
   applies changes and submits for approval.

## Golden rules

1. **Two sources of truth only.** The data file and the methodology document. Do **not** use
   outside knowledge, training data, or assumptions. If a claim can't be verified from those two
   files, say so explicitly — never guess to fill a gap.
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
Follow `references/source-discovery.md` §1–2.

### 2. Locate the evidence in Google Drive
Search the brand's Drive folder for the **raw data file** (Excel/CSV/Google Sheet) and the
**methodology document** (Word/PDF/Doc). Confirm the right file, and the right **tab**, when there
is any doubt — old, duplicate, or working tabs are common. Follow `references/source-discovery.md`
§3–4.

### 3. Run the audit
Read all three (PR, data, methodology) and work through `references/audit-checklist.md`: list the
methodology limitations first, then flag issues across the four categories with a quote, the
source, and a suggested correction. Report the result in chat.

### 4. Explain a ranking (on request)
If a ranking looks off, or the user asks "why is X above Y", follow `references/ranking-analysis.md`
to show the working from the methodology's factors and weightings — using only the data file.

### 5. Wrap up
End with a short recap: which two source files were used, the limitations applied, and the count of
issues found (or a clean bill). Remind the reviewer to tag **Dani, Kiran, or Georgia** on anything
uncertain, and — once corrections are made — to post in the approvals channel and tag **Georgia**,
noting a fact-check against the methodology was completed. You do not post this yourself.

## Data sources

| Source | Used for |
| --- | --- |
| Slack `dpr-approvals` channel | The review thread + the press-release Google Doc link |
| Press-release Google Doc | The claims being audited |
| Raw data file (brand Drive folder) | Ground-truth figures, rankings, tables — source of truth |
| Methodology document (brand Drive folder) | Scope, what was measured/excluded, scoring & weightings — source of truth |

## Reference files

- `references/source-discovery.md` — find the review thread, resolve the PR doc, and locate the
  brand's data file + methodology in Google Drive (with confirmation on ambiguity).
- `references/audit-checklist.md` — the audit discipline: limitations-first, the four flag
  categories, per-issue format, and the chat report layout.
- `references/ranking-analysis.md` — how to explain why one item is ranked above another, showing
  the working from methodology factors and weightings.
