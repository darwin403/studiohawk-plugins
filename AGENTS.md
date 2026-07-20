# AGENTS.md

Guidance for AI agents working on this repo. This repo is a **Claude Code plugin marketplace**
that distributes a single plugin. Most of the traps here are about the marketplace/plugin
**structure**, not the code inside the skills.

## Repository structure (do not break this)

```
.claude-plugin/
└── marketplace.json             # marketplace manifest ONLY
studiohawk-dpr-toolkit/          # the plugin (marketplace source -> "./studiohawk-dpr-toolkit")
├── .claude-plugin/
│   └── plugin.json              # plugin manifest ONLY
├── .mcp.json
├── docs/
└── skills/
```

- Root `.claude-plugin/` holds **only** `marketplace.json`.
- The plugin lives in its **own subfolder** with its **own** `.claude-plugin/plugin.json`.
- `marketplace.json` `plugins[0].source` is `"./studiohawk-dpr-toolkit"`.

## The #1 trap: never flatten the plugin into the repo root

The desktop / claude.ai marketplace sync runs **strict schema validation**. It **fails** when the
plugin is the marketplace root — i.e. when `plugin.json` and `marketplace.json` share the same
root `.claude-plugin/` directory (`source: "."` or `"./"`).

Symptom: **"Marketplace sync failed. Check the repository URL and try again."** (The URL is fine —
the message is misleading; it's a manifest/structure rejection.)

**`claude plugin validate .` does NOT catch this.** The CLI validator is lenient and passes on the
broken flat layout, so passing validation is *not* proof the desktop app will accept it. The only
reliable check is adding the marketplace in the desktop app itself (Customize → Plugins → Add
marketplace → Add from a repository).

Rule: **keep the plugin in a subfolder** so the marketplace root and plugin root are different
directories. Do not "simplify" by moving the plugin to the root, even for a single-plugin repo.

## Other manifest rules learned the hard way

- **Pure ASCII in manifests.** No smart quotes, em-dashes (—), or other non-ASCII in
  `marketplace.json` / `plugin.json` descriptions. Non-ASCII has broken desktop sync before. Use
  `-` and straight quotes.
- **No `$schema` key** in `marketplace.json` (a dead 404 URL) and put `version`/`description`
  under a `metadata` object at the marketplace root. Strict validation rejects unrecognized root
  keys.
- Relative-path plugin sources **must start with `./`** (e.g. `"./studiohawk-dpr-toolkit"`, not
  `"."` or `"studiohawk-dpr-toolkit"`).
- Plugin name and marketplace name being **identical is fine** — that was verified working and is
  not the cause of sync failures.

## The #2 trap: a skill silently missing from the available-skills list

If a skill isn't detected (it just never appears), the cause is almost always its
`SKILL.md` **YAML frontmatter `description`**. The plugin directory's frontmatter parser chokes on
`&`, angle brackets `< >`, square brackets `[ ]`, or **any non-ASCII character** — em-dashes (`—`),
en-dashes (`–`), and smart/curly quotes (`“ ” ‘ ’`) — and **silently skips the whole skill** with no
error. The other skills in the same plugin still load, so it looks like a per-skill glitch.

This has recurred multiple times (an em-dash regressed `press-release-audit` even after the bracket
rule was documented). Before committing any SKILL.md, check the frontmatter block:

```
grep -nP '[&<>\[\]]|[^\x00-\x7F]' <skill>/SKILL.md   # inspect the frontmatter matches
```

Fix by rewording with plain ASCII (plain hyphen `-`, comma, or restructured phrasing). These
characters are fine in the SKILL.md **body** and in `references/` — only the frontmatter
`description` is parsed strictly. See `studiohawk-dpr-toolkit/docs/ADDING-WORKFLOWS.md` for the full
rule.

## Deploying changes

The desktop app syncs from **GitHub**, not the local working tree. Any manifest/structure change
must be **committed and pushed** before it takes effect, and users re-sync via Customize → Plugins
→ Update (or remove + re-add the marketplace if a previous failed sync cached a bad state).

## Verifying a structure change

1. `claude plugin validate .` (necessary, not sufficient — see trap above).
2. Confirm layout: `marketplace.json` alone at root; `plugin.json` in the subfolder's
   `.claude-plugin/`; `source` points at the subfolder.
3. Commit + push, then add/update the marketplace in the desktop app to confirm sync succeeds.
