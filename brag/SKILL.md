---
name: brag
description: Keep a brag doc for appraisals — sweep your recent work (GitHub PRs, tickets from Linear/Jira/GitHub Issues/anything, or a list you paste) and file themed win entries into a folder of markdown, then generate an appraisal summary for any date range. Use when the user runs /brag, wants to log their wins, or asks for an appraisal / review summary from their logged work.
---

# Brag doc

A brag doc is a running log of what you shipped, so review time is a lookup, not a memory test.
At appraisal time people remember last month, not the year. This skill keeps the log current and
builds the summary on demand.

## The two layers

```
<brag folder>/
├── README.md        how this folder works (written on first run)
├── config.md        where wins come from, your handles, the default window
├── index.md         browse surface: themes + flagship wins
├── log.md           append-only record of every sweep
├── themes/          RAW LAYER — wins filed by theme, written weekly, rich but unpolished
├── standalone.md    wins that fit no theme yet
└── appraisals/      DERIVED LAYER — summaries generated on demand, never hand-edited
```

Raw entries are the source of truth. Appraisal summaries are generated from them for whatever
date range and rubric you name. The raw layer never changes shape when the rubric does.

## Step 0 — First run: set up the folder

If the brag folder does not exist or has no `config.md`:

1. Ask where it should live. Any folder of markdown works: an Obsidian vault subfolder, a notes
   directory, a private repo. Create the layout above.
2. Ask where wins come from. Offer these, any combination:
   - **GitHub** — merged PRs by the user, through the local `gh` CLI (their own auth).
   - **A task tracker** — Linear, Jira, GitHub Issues, Asana, Notion, anything with a connector
     or MCP in this session. Completed items assigned to the user.
   - **Paste or describe** — a list of wins, kudos from chat, a local `git log`, release notes.
   - Anything else the user names. Do not assume Linear or GitHub.
3. Write the answers into `config.md`: sources, GitHub handle and repos, tracker name, default
   window, optional appraisal rubric. Read `config.md` on every later run instead of asking again.

Never store a token, password or API key anywhere in the folder.

## Step 1 — Pick the window

- Default: **since the last sweep**. Read the newest date in `log.md`, sweep from the next day to today.
- If the user named a range ("last month", "Q2", "since April"), use that.
- First run with no log: ask how far back to start. Default to 30 days.

## Step 2 — Sweep each configured source

**GitHub** (if configured):

```
gh pr list --repo <owner/repo> --author <handle> --state merged \
  --search "merged:>=<START>" --json number,title,mergedAt,url,additions,deletions,labels
```

For PRs that look flagship (large diffs, new features, refactors), read the body to ground the
impact line: `gh pr view <n> --repo <owner/repo> --json title,body`.

**Task tracker** (if configured): find the user, list items assigned to them and completed
inside the window. Capture the identifier, title, completion date and project. If the connector
is not authorised in this session, skip it, say so in the report, and carry on.

**Pasted / described**: take what the user gives you as the evidence. Ask one question if a win
has no outcome attached.

A missing source never fails the run. Report the gap and continue with the rest.

## Step 3 — Draft and file entries

- Map each win to an existing theme file. Read the theme list from `index.md`. Create a theme only
  when several wins cluster outside every existing one.
- Roll closely related PRs or tickets into one entry. One entry per outcome, not per PR.
- Use the entry schema in [TEMPLATES.md](TEMPLATES.md). Insert **newest-at-top** within a theme.
- **Never invent metrics.** State impact qualitatively from what the PR or ticket says. Where a real
  number would help and you do not have it, leave `> 📌 Add metric:` so the user fills it in while
  they still remember it.
- Evidence cites PR numbers and ticket IDs. Link related themes with `[[theme-name]]`.

## Step 4 — Update index and log

- `index.md`: theme counts, and the flagship table if a new headline win landed.
- `log.md`: append `## [YYYY-MM-DD] sweep | <n> wins across <themes>`.

## Step 5 — Report

Say how many wins were filed, which themes grew, any flagship additions, any gaps (a source
skipped, metrics still to fill). Do not commit or push anything. The user reviews the files first.

## Appraisal mode

When the user asks for an appraisal or review summary for a range:

1. Read `config.md` for a rubric. If none, group by **scope × impact × skills**.
2. Read every raw entry inside the range. Do not summarise from memory.
3. Write `appraisals/<timeframe>.md` using the template in [TEMPLATES.md](TEMPLATES.md): headline
   wins first, then themes, then skills shown, then gaps (wins with no metric).
4. Every claim in the summary must trace to a raw entry. If it does not, cut it.

## Privacy

The brag folder holds real work. Keep it in a private location. This skill runs on the user's own
machine with their own auth and sends nothing anywhere.
