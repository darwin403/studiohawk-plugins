# Audit Checklist

Run this once you have the press release, the confirmed data file + tab, and the methodology
document (see `source-discovery.md`). The data file and methodology are the **only** sources of
truth. Do not use outside knowledge, training data, or assumptions. If a claim can't be verified
from those two files, say so explicitly — never guess.

## Step 1 — List the methodology's limitations first

Before flagging anything, read the methodology and write down, plainly:

- **Scope** — what was measured, and over what period/region/population.
- **Exclusions** — what was deliberately left out.
- **Data sources & platforms** — where the numbers came from, and any search terms used.
- **Scoring & weighting** — how each factor is scored and weighted into the final ranking.

Every claim in the press release is judged against this scope. Anything that reaches beyond it gets
flagged in Step 2.

## Step 2 — Flag issues in four categories

Review the press release against the data and methodology and flag:

1. **Methodology accuracy** — Does the PR correctly describe how the data was collected, scored,
   and ranked? Flag any search term, data source, platform, weighting, or step in the PR that does
   not match the methodology document.
2. **Overstated or unsupported claims** — Anything that goes beyond what the data shows or beyond
   the methodology's stated scope: exaggeration, assumed intent, inferred causation, or claims the
   dataset can't directly support.
3. **Incorrect statistics or figures** — Every number, percentage, ranking, and statistic must
   match the data exactly. **Recalculate** from the data file; don't trust the PR's arithmetic.
4. **Out-of-scope claims** — Subjective claims ("best", "worst", "most stressful", "safest") that
   the methodology doesn't actually measure.

## Step 3 — Format for each flagged issue

For every issue, give three things:

- **PR says:** the exact quoted line from the press release.
- **Source says:** what the data file (cite the tab/cell) or methodology (cite the section) actually
  states.
- **Suggested fix:** a corrected version of the line where one is possible, or "cannot be supported
  from the data — remove or reword" when it can't.

## Step 4 — Report in chat

Structure the chat report as:

```
Files audited
- Press release: <doc title / link>
- Data: <file name> — tab "<tab>"
- Methodology: <file name>

Methodology limitations applied
- Scope: ...
- Excluded: ...
- Sources/platforms: ...
- Weightings: ...

Issues found (<n>)
1. [Methodology accuracy] PR says: "..." | Source says: ... | Suggested fix: ...
2. [Incorrect statistic]  PR says: "..." | Source says: ... (recalculated: ...) | Suggested fix: ...
...

(If none: "No issues found. Checked against the limitations listed above — every claim is
supported by the data and stays within the methodology's scope.")
```

Then close with the wrap-up from `SKILL.md` §5: tag Dani/Kiran/Georgia on anything uncertain, and
after corrections, post in the approvals channel and tag Georgia noting the fact-check was done.
You do not post anything yourself — the reviewer does.

## Discipline reminders

- Recalculate; don't assume the PR's numbers are right.
- If the data file contradicts the methodology (e.g. a weighting differs), flag the conflict rather
  than silently trusting one — the reviewer decides.
- Empty or missing evidence is a finding, not a blank to fill: say "not present in the data".
