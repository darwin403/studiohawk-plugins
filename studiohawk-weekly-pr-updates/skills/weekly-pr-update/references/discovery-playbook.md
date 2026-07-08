# Discovery Playbook (first run for a brand)

Run this the first time a brand is processed, or whenever its config is missing. The goal is to
locate every source that belongs to the brand and save a reusable config so future runs are fast
and require no re-discovery. Confirm ambiguous matches with the user rather than guessing.

## 0. Establish the brand

Get the brand/client name from the user. Derive a `brand_slug` (lowercase, hyphenated, e.g.
"Acme Foods" -> `acme-foods`). This slug names the config file.

## 1. Slack channel(s)

Search Slack for the brand's client channel. Try the brand name and common StudioHawk naming
patterns (e.g. `#client-<brand>`, `#<brand>`, `#<brand>-pr`, `#<brand>-digital-pr`). Use
`slack_search_channels` / `slack_search_public` to find candidates.

Record each channel's name and channel ID. If several plausible channels exist, list them and
ask the user which to include. Note whether any channel is private (the installer must be a
member for it to be searchable).

## 2. Monday.com board (Master Campaign Management)

The "Master Campaign Management" board is brand-specific. Search Monday for the brand's board by
name (try the brand name and "Master Campaign Management <brand>"). Use the Monday tools to list
boards and fetch the board schema.

Record: board ID, board name, and the column/status mapping that indicates completion (e.g. the
Status column value that means Done/Complete) and the values that indicate blocked or
waiting-on-client. Capture the group(s) used for active campaign work.

## 3. Google Drive — coverage sheet + campaign docs

Locate the shared coverage sheet `[NEW] Client Link Tracker & Media Requests` in Google Drive
(`search_files`). This is the primary coverage source and is usually shared across brands, so
identify the specific **tab** or the column/value that filters rows to this brand.

Record: the sheet's file ID and link, the brand's tab name (or the filter column + value used to
isolate this brand's rows), and the column positions for outlet, headline/anchor, URL, link
type, DA, and date.

Also search Drive for any brand-specific campaign folder or "Master Campaign Management" doc if
one exists, and record its link for reference.

## 4. Gmail — client thread & contacts

Search Gmail for recent threads with the client to identify: the client's contact name(s) and
email address(es), and any Gmail label the team uses for this brand. Record these.

Mark the client email as `"verified"` only if it clearly appears as the client contact in real
correspondence; otherwise mark `"unverified"` so drafts default to the internal owner.

## 5. Recipient & owner

Determine the managing team member (owner) for this brand and the intended client recipient(s)
for the weekly update. If unclear, ask the user. The owner is the safe fallback recipient for
drafts.

## 6. Save the config

Write the config to Google Drive at
`StudioHawk PR Automation / Brand Configs / <brand-slug>.config.json` using the schema in
`brand-config-schema.md`. Create the folder(s) if they do not exist. This shared location lets
every teammate reuse the same discovery, so the discovery phase only happens once per brand for
the whole team.

Confirm to the user what was discovered and saved, and flag anything that needs their
verification (e.g. an unverified client email, or a channel/board that had multiple candidates).

## Re-discovery

If a later run finds the saved identifiers no longer resolve (channel archived, board renamed,
sheet moved), re-run the relevant step, update the config in place, and note the change.
