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

If one skill isn't detected (it just never appears, while its siblings load fine), the cause is
its `SKILL.md` **YAML frontmatter**. The skill is silently rejected with no error. Two distinct
causes, in order of how often they've bitten this repo:

1. **`description` over 1024 characters (most common here).** The Agent Skills spec caps
   `description` at **1024 chars**; a longer one makes the whole skill invalid and it is dropped.
   `claude plugin validate` does **not** catch this — it only validates `marketplace.json`, not
   each `SKILL.md`. This is what actually broke `press-release-audit` (its description had grown to
   1164 chars). Keep descriptions comfortably under 1024 — the working skills here sit around 820.
2. **Parser-hostile characters in `description`.** Avoid `&`, angle brackets `< >`, square
   brackets `[ ]`, and non-ASCII (em-dashes `—`, en-dashes `–`, smart quotes `“ ” ‘ ’`). Use plain
   ASCII. (These are fine in the SKILL.md **body** and in `references/` — only the frontmatter is
   strict.)

Before committing any SKILL.md, check both at once:

```
# 1) length of each skill's description (must be <= 1024)
for f in studiohawk-dpr-toolkit/skills/*/SKILL.md; do \
  python3 -c "import re,yaml,sys;t=open('$f').read();d=yaml.safe_load(re.match(r'^---\n(.*?)\n---',t,re.S).group(1));print(len(d['description']),'$f')"; done
# 2) hazardous chars in frontmatter
grep -nP '[&<>\[\]]|[^\x00-\x7F]' studiohawk-dpr-toolkit/skills/*/SKILL.md
```

Fix by trimming/rewording the `description` in plain ASCII. See
`studiohawk-dpr-toolkit/docs/ADDING-WORKFLOWS.md` for the full rule.

## Deploying changes

The desktop app syncs from **GitHub**, not the local working tree. Any manifest/structure change
must be **committed and pushed** before it takes effect, and users re-sync via Customize → Plugins
→ Update (or remove + re-add the marketplace if a previous failed sync cached a bad state).

## Verifying a structure change

1. `claude plugin validate .` (necessary, not sufficient — see trap above).
2. Confirm layout: `marketplace.json` alone at root; `plugin.json` in the subfolder's
   `.claude-plugin/`; `source` points at the subfolder.
3. Commit + push, then add/update the marketplace in the desktop app to confirm sync succeeds.
