# Source Discovery (per audit)

The audit is only as trustworthy as the three files it runs on. This is how to find them reliably
and confirm anything ambiguous before reading. Never guess a file or a tab — a wrong source
produces a confidently wrong audit.

## 1. Find the review thread in `dpr-approvals`

1. Locate the Slack channel `dpr-approvals` (search channels if you don't have its ID).
2. The user names the PR (e.g. "audit the Luxo Living PR"). Search the channel for the matching
   review thread. Threads are titled like "**Luxo Living PR for review**", so match on the brand
   name plus wording like "PR", "for review", or "approval".
3. If several threads match (e.g. multiple rounds for the same brand), list the candidates with
   their date/author and ask which to audit with `AskUserQuestion`. Prefer the most recent unless
   the user says otherwise.

## 2. Resolve the press-release Google Doc

1. In the chosen thread (the root message and replies), find the **Google Doc link**
   (`docs.google.com/document/...`). Extract the document ID from the URL.
2. Read the document via Google Drive. This is the press release under audit.
3. If the thread has no Doc link, or has several, ask the user which link is the press release.
4. Note the brand and any campaign name from the doc title/thread — you'll use it to find the
   evidence folder next.
5. Note the **accompanying assets** on the thread/doc — the **pitch** and the **imagery** — you'll
   check for these in the completeness track (`completeness-checklist.md` §A). Their absence is a
   finding, so record what is and isn't attached.

## 3. Classify the piece (data-led / expert-led / UGC)

This decides whether §4–5 (the data file + methodology hunt) even apply.

1. **Data-led** — the story is built on a dataset, ranking, index, or survey the campaign produced.
   These need a raw data file **and** a methodology document; proceed to §4.
2. **Expert-led** — the story is built on an expert's commentary or quotes. It may cite a stat, but
   it is not built on a dataset the campaign produced.
3. **UGC** — the story is built on user-generated content.
4. For expert-led and UGC pieces, **do not** go hunting for a raw data file + methodology; skip to
   the completeness track. If such a piece cites a **single self-sourced stat**, that stat just
   needs a credible source noted — it does not require a full methodology document.
5. If the type is genuinely ambiguous (e.g. an expert-led piece leaning heavily on a ranking),
   confirm with `AskUserQuestion` rather than assuming, because it changes what evidence you require.

## 4. Locate the brand's evidence in Google Drive (data-led only)

For a **data-led** piece, the **raw data file** and **methodology document** live in a brand-scoped
Drive folder, not in the Slack thread. Find them:

1. Search Drive for the brand's folder (try the brand name and campaign name). List its contents.
   If a shared brand config exists in `StudioHawk PR Automation / Brand Configs / <brand>.config.json`
   and records a campaign/Drive folder, use it as a shortcut — but still confirm the specific files.
2. **Raw data file** — a spreadsheet (`.xlsx`, `.csv`, or Google Sheet) holding the raw and ranked
   tables behind the story. Filenames often include the brand, campaign, "data", "ranking", or
   "index".
3. **Methodology document** — a Word doc, PDF, or Google Doc explaining how the data was collected,
   scored, weighted, and ranked. Filenames often include "methodology", "method", "scoring",
   "criteria", or "how we".
4. If you find zero or multiple plausible candidates for either file, list what you found and ask
   the user to pick, with `AskUserQuestion`. Do not proceed on a guess.

## 5. Confirm the right data tab (data-led only)

Spreadsheets frequently carry old, working, or duplicate tabs. Before treating the data as truth:

1. List the tabs/sheets in the data file.
2. Identify the **final ranked table** that the press release is actually built on. If it's not
   obvious (multiple ranked tabs, "old"/"v1"/"working" tabs, unclear which is final), ask the user
   which tab is authoritative rather than assuming.
3. Record the exact tab name and the columns that map to the figures the PR cites (rank, score,
   each weighted factor, totals), so every recalculation in the audit is traceable to a cell.

## 6. Ready to audit

For a data-led piece, once you have confirmed the **press release**, the **data file + correct
tab**, and the **methodology document**, proceed to `audit-checklist.md`. For expert-led/UGC pieces,
the press release (plus whatever assets are attached) is enough — go straight to the completeness
track. Either way, run `completeness-checklist.md` on every piece, and state the files and the piece
type at the top of the report so the reviewer can verify the inputs at a glance.
