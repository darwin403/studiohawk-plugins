# Weekly Client Update — Report Template

This is the structure and tone for the client-facing draft. The audience is an **external
client**, so keep it warm, clear, and free of internal jargon or sensitive internal chatter.

## Source → section mapping

| Section | Primary source | What to include |
| --- | --- | --- |
| Coverage achieved | `[NEW] Client Link Tracker & Media Requests` sheet (brand rows), corroborated by Slack | Placements that went live in the window: outlet, headline/anchor, link, link type, DA if available |
| Work completed | Monday board items marked Done in the window; Slack sign-offs | Pitches sent, assets delivered, campaigns launched, milestones hit |
| Outstanding | Monday items in active groups (not done), Monday blocked/stuck items, open media requests in the sheet, unresolved Gmail/Slack threads | Everything still open on our (or the joint) side: active work, what's next, blocked items, and pitches/requests awaiting a response — a single consolidated view across all sources |
| Action items for you | Monday "waiting on client" items; open asks in Gmail/Slack | Only things the client must review, approve, or provide |
| Reference documents | Config `reference_docs` (client_shareable) + docs discovered in Drive for the window + placement URLs | A consolidated, deduped list of every client-facing document referenced above, for easy client reference |

## Draft format

```
Subject: <Brand> — Weekly PR Update (w/e <Fri date>)

Hi <Client first name>,

Here's your digital PR update for the week ending <date>.

Coverage secured this week
- <Outlet> — "<Headline / anchor>" (<link type>, DA <n>): <URL>
- <Outlet> — ...
(If none: "No new placements went live this week, but here's what's in motion below.")

Work completed
- <Item> — <one-line outcome>
- <Item> — ...

Outstanding
- <Item> — <status / expected timing>
- <Blocked item> — <what it's waiting on>
- <Media request / pitch> — <outlet, awaiting response>
(Consolidate everything still open across sources; omit the whole section if nothing is outstanding.)

Action items for you
- <What we need> — <why / by when>
(Omit this whole section if there are no client actions this week.)

Reference documents
- <Press release title> — <URL>
- <Campaign / landing page> — <URL>
- <Client-facing doc> — <URL>
(Omit this whole section if there are no client-shareable reference documents this week.)

Thanks,
<Owner name>
<Signature>
```

## Style guidance

- Lead with wins. If coverage was secured, make it the star.
- Quantify where honest data exists (number of placements, DA, pitches sent). Never invent
  numbers, dates, or outlets.
- One line per item; link every placement.
- "Outstanding" is the single home for everything still open on our side — pull it from every
  source (Monday active + blocked, media requests, unresolved Gmail/Slack), deduped by item.
- Keep "Action items for you" short and specific — this is what drives the client to respond. An
  item belongs in one section only: if the client must act, it goes here, not in "Outstanding".
- If a `my-writing-style` skill is available, match the team's voice.
- Reporting window and dates come from the config timezone (default Australia/Sydney).

## Linking references (inline + reference documents section)

When an item names a specific artifact — a press release, campaign, landing page, published asset,
or a client-facing doc — hyperlink that mention to its source, and also collect it into the
**Reference documents** list at the end. The same links appear in both places (inline for context,
end list for easy scanning). Rules:

1. **Build the candidate set** from three sources, deduped by URL:
   - the brand config's `reference_docs` where `client_shareable` is `true`;
   - documents discovered in Google Drive for the reporting window (Drive connector `search_files` /
     `read_file_content`) that are clearly client-facing;
   - placement URLs already in the Coverage section.
2. **Client-appropriateness gate — never leak internal material.** Only include documents a client
   should see: published press releases, live campaign/landing pages, published assets, and docs
   already shared with the client. **Never** put internal sources in the email — Monday boards,
   internal Slack, internal strategy/planning docs, or any `reference_docs` entry with
   `client_shareable: false`. Those belong only in the internal notes block below.
3. **Access — flag, don't drop.** If a document is client-appropriate but you can't confirm the
   client can actually open it (unknown sharing, not a public URL), still include the link, but list
   it in the internal notes block flagged "verify sharing before sending" so the reviewer checks
   access first. Prefer a public/canonical URL over a Drive link when one exists.
4. **Never invent a link.** If no trustworthy source exists for an item, leave it as plain text.
5. **Deduplicate.** A placement already linked inline in Coverage doesn't need re-listing, but do
   include it in the Reference documents section so that list is complete on its own.

## Internal notes block (not part of the client email)

When reporting back to the user in chat, include a short internal note with source links: the
Slack messages, Monday item URLs, and sheet rows used, plus anything skipped or uncertain, so the
reviewer can verify fast before sending. Also list, separately:

- **Reference links needing a sharing check** — any client-appropriate document included in the
  email whose client access you couldn't confirm (per Linking rule 3). The reviewer confirms the
  client can open each before sending.
- **Internal docs held back** — client-relevant material deliberately kept out of the email
  (internal Monday/Slack/strategy docs, `client_shareable: false` entries), so the reviewer knows
  it was considered and excluded on purpose.
