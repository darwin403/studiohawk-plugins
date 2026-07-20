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

## Install

Do this once. Everything happens in the **Claude desktop app** — no typing of commands.

### Step 1 — Add your four connectors

1. In the left sidebar, open **Customize → Connectors**.
2. Browse the connector list and add each of these, signing in with your StudioHawk account:
   - **Slack**
   - **Gmail**
   - **Google Drive**
   - **monday.com**

Do all four now, so nothing interrupts you later. Each one shows **Connected** when it's done.

### Step 2 — Add the toolkit plugin

1. In the left sidebar, open **Customize → Plugins**.
2. In the **Personal plugins** section, click the **"+"** → **Add marketplace** → **Add from a
   repository**.
3. Paste this and let it sync:

   ```
   https://github.com/darwin403/studiohawk-dpr-toolkit
   ```

4. Click **Browse plugins**, find **studiohawk-dpr-toolkit**, and click **Install**.

**That's it — installation is done.** You now have both skills available in your chat. Head to
**Usage** below to start using them.

---

## Usage

Everything you do runs in a **Cowork chat**. On the home screen, in the message box, select
**Cowork** (the toggle next to **Chat**), then start your message with the skill's slash command:

- **Weekly client update** — `/weekly-client-update`
- **Press release audit** — `/press-release-audit`

Starting with the slash command makes sure Claude runs the right skill. Everything below is typed
straight into that Cowork chat.

### Weekly client update

**Start it** — begin with the slash command and add the brand:

```
/weekly-client-update draft this week's update for <brand>
```

That's all you do — it finds the brand's Slack channel, monday.com board, coverage sheet, and
client contacts on its own, pulls this week's info, and hands you a finished draft. The first time
you name a brand it figures out the details under the hood — you don't set anything up.

**What you get**

- A ready-to-review **Gmail draft** with this week's:
  - **Coverage secured** — placements that went live, with links.
  - **Work completed** and **what's next**.
  - **Action items for you** — anything the client needs to approve or provide.
  - **Reference documents** — a tidy list of the press releases, campaigns, and docs mentioned,
    hyperlinked so the client can click straight through.
- A short note back in chat showing where the info came from, so you can double-check quickly.

**Good to know**

- **It never sends.** The draft sits in your Gmail Drafts until *you* send it.
- You can **ask for any change** — "make it shorter", "drop the intro", "add a line about the
  podcast". Just say it.
- If it can't confirm a client can open a linked document, it **flags it for you** to check before
  sending — so no broken "request access" links go out.
- If there's no coverage this week, it says so honestly instead of inventing anything.

### Press release audit

**Start it** — begin with the slash command and name the press release:

```
/press-release-audit check the <brand> press release
```

Claude finds the review thread in the `dpr-approvals` Slack channel, opens the linked Google Doc,
and pulls the brand's raw data file and methodology document from Google Drive.

**What you get** — a checklist **in chat only** covering:

- Claims that don't match the data
- Overstated or exaggerated wording
- Wrong statistics
- Claims the methodology doesn't actually support
- The limitations of the methodology itself

**Good to know**

- It **only reads** — it never edits the doc or posts to Slack.
- It uses the real data file and methodology as the source of truth, so it won't guess.

---

## Managing the plugin

**Update** — open **Customize → Plugins** in the left sidebar, find the **studiohawk-dpr-toolkit**
marketplace, and click **Update** to sync the latest version. Your saved brand setups are kept —
you don't need to redo anything.

**Remove** — in **Customize → Plugins**, click **Uninstall** on the **studiohawk-dpr-toolkit**
plugin to turn it off, or remove its marketplace to delete the source completely.

---

## Need a hand?

- **A service isn't connected?** Open **Customize → Connectors** and make sure all four (Slack,
  Gmail, Google Drive, monday.com) show **Connected**.
- **Something looks off in a draft?** Just tell Claude what to change — it's built for that.
- **Stuck?** Ask in the team's internal channel, or ping whoever set up the toolkit.
