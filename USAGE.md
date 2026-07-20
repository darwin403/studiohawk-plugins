# StudioHawk DPR Toolkit — Team Guide

A plain-English guide to using the StudioHawk digital PR skills inside Claude. No technical
knowledge needed. You talk to Claude in normal English — the examples below are things you can
literally type.

**The golden rule:** these skills only ever prepare **drafts** for you to review. Nothing is
emailed, posted, or changed on its own. You always have the final click.

---

## What you can do with it

The toolkit adds two skills to Claude:

| Skill | What it does for you |
| --- | --- |
| **Weekly client update** | Writes the weekly PR update email for a brand and saves it as a **Gmail draft** for you to review and send. |
| **Press release audit** | Fact-checks a press release before it goes out and tells you (in chat) what to fix. |

---

## 1. Install it (once)

You only do this the first time.

**Step 1 — Add the toolkit and install it.** Type these two lines to Claude, one at a time:

```
/plugin marketplace add darwin403/studiohawk-dpr-toolkit
/plugin install studiohawk-dpr-toolkit@studiohawk-dpr-toolkit
```

**Step 2 — Connect your accounts.** When prompted, connect these four services with your own
StudioHawk logins (you only do this once):

- **Slack**
- **monday.com**
- **Google Drive**
- **Gmail**

That's it — you're ready.

---

## 2. Weekly client update

### Start it

The very first time you do a brand, set it up:

```
Set up StudioHawk PR updates
```

Claude walks you through it with clickable buttons — pick the brand, and it finds the brand's
Slack channel, monday.com board, coverage sheet, and client contacts for you. You'll see a
**sample email** so you know exactly what it looks like, and it can save a weekly schedule if you
want one.

After a brand is set up, just ask for a draft anytime:

```
Draft the weekly client update for <brand>
```

### What you get

- A ready-to-review **Gmail draft** with this week's:
  - **Coverage secured** — placements that went live, with links.
  - **Work completed** and **what's next**.
  - **Action items for you** — anything the client needs to approve or provide.
  - **Reference documents** — a tidy list of the press releases, campaigns, and docs mentioned,
    hyperlinked so the client can click straight through.
- A short note back in chat showing where the info came from, so you can double-check quickly.

### Good to know

- **It never sends.** The draft sits in your Gmail Drafts until *you* send it.
- You can **ask for any change** — "make it shorter", "drop the intro", "add a line about the
  podcast". Just say it.
- If it can't confirm a client can open a linked document, it **flags it for you** to check before
  sending — so no broken "request access" links go out.
- If there's no coverage this week, it says so honestly instead of inventing anything.

---

## 3. Press release audit

### Start it

Name the press release you want checked:

```
Audit the <brand> press release
```

Claude finds the review thread in the `dpr-approvals` Slack channel, opens the linked Google Doc,
and pulls the brand's raw data file and methodology document from Google Drive.

### What you get

A checklist **in chat only** covering:

- Claims that don't match the data
- Overstated or exaggerated wording
- Wrong statistics
- Claims the methodology doesn't actually support
- The limitations of the methodology itself

### Good to know

- It **only reads** — it never edits the doc or posts to Slack.
- It uses the real data file and methodology as the source of truth, so it won't guess.

---

## 4. Updating the plugin

When the team ships improvements, pull the latest version by typing:

```
/plugin marketplace update studiohawk-dpr-toolkit
```

Your saved brand setups are kept — you don't need to redo anything.

---

## 5. Removing the plugin

If you ever need to remove it:

```
/plugin uninstall studiohawk-dpr-toolkit@studiohawk-dpr-toolkit
```

To also remove the toolkit source completely:

```
/plugin marketplace remove studiohawk-dpr-toolkit
```

---

## Need a hand?

- **A service isn't connected?** Claude will tell you which one and prompt you to connect it.
- **Something looks off in a draft?** Just tell Claude what to change — it's built for that.
- **Stuck?** Ask in the team's internal channel, or ping whoever set up the toolkit.
