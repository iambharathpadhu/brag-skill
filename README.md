# brag — a Claude Code skill that keeps your brag doc for you

At appraisal time you remember last month, not the year. A **brag doc** is a running log of
your wins that you update weekly, so review time is a lookup.

This skill does the weekly sweep. It reads what you shipped, files each win as a short entry
(what, impact, scope, skills, evidence) under a theme, and later turns any date range into an
appraisal summary.

## Two layers

- **Raw layer** — wins filed weekly, rich but unpolished. This is the source of truth.
- **Derived layer** — appraisal summaries generated on demand from the raw entries, for any
  date range or rubric.

## Works with whatever you use

Wins can come from any mix of:

- **GitHub** merged PRs, through your own `gh` CLI
- **A task tracker** — Linear, Jira, GitHub Issues, Asana, Notion, anything Claude Code has a
  connector for
- **A list you paste** — kudos, release notes, a `git log`

It asks once where your wins come from and where to store the folder, then remembers. Any folder
of markdown works, including an Obsidian vault.

## Install

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/iambharathpadhu/brag-skill.git /tmp/brag-skill
cp -r /tmp/brag-skill/brag ~/.claude/skills/brag
```

Then in Claude Code:

```
/brag
```

First run sets up the folder. After that, run it weekly. Ask it for "an appraisal summary for
H1" any time.

## Files

| File | What it holds |
|---|---|
| `brag/SKILL.md` | The workflow: setup, sweep, file, report, appraisal mode |
| `brag/TEMPLATES.md` | The entry schema, config file and appraisal template |

## Honest limits

It never invents a metric. Where a number would help and it does not have one, it leaves a
marker for you. It reports what the PR or ticket says, so a vague ticket gives a vague entry.
Keep the brag folder private, since it holds real work. It stores no tokens and never commits.

---

Built by a frontend engineer who explains tech in Tamil —
[@barathbuilds on Instagram](https://www.instagram.com/barathbuilds) · [iambharathpadhu.vercel.app](https://iambharathpadhu.vercel.app)
