# Deep Research Pro — Report Templates Reference

Support file for `deep-research-pro`. Skeleton for the final canvas report.
Labels below are conceptual; translate them into the report's output language.

## Main report skeleton (text/markdown canvas)

```markdown
# [Report title — the decision, not just the topic]

## Research Question
[One sentence, as interpreted after the advisor pass. Note any reframing from the user's
original wording.]

## Executive Summary
1. [Most important ranked takeaway, with inline citation]
2. [ ... 3-7 items total, most important first]

## Methodology
[Search angles, source types used, number of passes, freshness window, and the important
limitations — including assumptions made and advisor-flagged constraints.]

## Findings
### [Theme 1 — e.g. Market size and growth]
[Claims, each ending with a citation parenthesis. Diverging figures shown side by side.]

### [Theme 2 — e.g. Leading use cases with evidence]
[ ... ]

### [Theme 3 — e.g. Risks and open disputes]
[ ... ]

## Source Notes
| Source | Credibility | Last updated |
|---|---|---|
| [Source name](exact-url) | 4/5 | March 2026 |
| [Source name 2](exact-url-2) | 3/5 | - |

**Conflicts and caveats**
- [Conflict: which sources disagree, why, which figure this report uses.]

## Open Questions
- [Unresolved sub-questions, blocked sources, disputed claims]

## Recommendations / Next Steps
1. [Decision to make, test to run, document to read, or action to take]
```

## Rules for the skeleton

- Executive Summary items are ranked, not grouped.
- Findings are organized by theme and decision relevance, never by search order.
- Every claim in Findings carries a citation; vendor-reported numbers are labeled as such.
- Source Notes table columns are exactly: Source, Credibility, Last updated (localized).
- No separate link column; the Source cell is the link.
- Open Questions is mandatory even if short; an empty research report has no open questions
  only if the advisor pass found no failure modes — re-check before claiming that.

## Variants

- **Slides (type: slides)**: Executive Summary → one slide per theme → Sources slide.
  Same citation rules; heavier visuals, fewer words per claim.
- **Dashboard/table request**: findings as a comparison table first, narrative second.
- **Quick-turnaround mode** (user needs a fast answer, not a full report): skip the canvas,
  answer in chat with inline citations, and say a full report is available on request.
