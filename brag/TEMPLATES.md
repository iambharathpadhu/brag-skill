# Templates

## Raw entry (one per win, in `themes/<theme>.md`, newest at top)

```markdown
### <Win title> — YYYY-MM-DD
- **What:** what you did, one or two lines
- **Impact:** outcome, who benefited, a metric (real numbers only)
- **Scope:** Solo | Led | Cross-team — and who was involved
- **Skills:** [skill, skill, skill]
- **Evidence:** PR #123, ticket ID, doc or demo link
```

Four things matter: what you did, the impact, who you did it with, and proof. Add the number
now. In December you will not remember it.

## Theme file header

```markdown
---
theme: <theme-name>
---
# <Theme name>
One line on what this theme covers.

<entries, newest first>
```

## config.md

```markdown
# Brag config
sources: [github, tracker, paste]
github: { handle: <your-handle>, repos: [owner/repo] }
tracker: <Linear | Jira | GitHub Issues | other>
default_window: since last sweep
rubric: <paste your company's levels or review criteria, or "none">
```

## Appraisal summary (`appraisals/<timeframe>.md`)

```markdown
# <Timeframe> — appraisal summary
## Headline wins
1-3 items. Each: outcome first, then what you did, with a number if one exists.
## By theme
One short paragraph per theme, linking the raw entries.
## Skills shown
What the wins prove, mapped to the rubric if there is one.
## Gaps
Wins with no metric yet. Fill these before submitting.
```
