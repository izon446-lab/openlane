# Deep Research Pro — Source Standards Reference

Support file for `deep-research-pro`. Credibility scoring rubric and citation mechanics.

## 1. Credibility tiers (high → low)

| Tier | Source type | Typical score |
|---|---|---|
| 1 | Official/regulatory sources, filings, audited statistics, standards bodies | 5/5 |
| 2 | Peer-reviewed academic work, major statistical agencies (OECD, TÜİK, Eurostat) | 5/5 |
| 3 | Established press with editorial standards (Reuters, AP, FT, major nationals) | 4/5 |
| 4 | Recognized industry analyst reports (Gartner, McKinsey, Statista) | 4/5 |
| 5 | Practitioner/vendor blogs with concrete production data | 3/5 |
| 6 | General vendor marketing blogs, SEO content farms | 2/5 |
| 7 | Forums, social media, anonymous claims | 1/5 — use only as sentiment, never as evidence |

Adjustments:
- **-1**: vendor reporting ROI on its own product; undated content; heavy uncited aggregation.
- **+0.5**: primary data with published methodology; official docs of the product/system itself.
- A Tier-5 source with firsthand production numbers can outrank a Tier-4 summary of it —
  score the actual content, not just the brand.

## 2. Scoring rules for the Source Notes table

- Score is `n/5`, never prose ("High", "Trusted" are forbidden).
- Score the source as used in THIS report, not in general.
- If a claim rests on a single ≤3/5 source, the Findings text must say so
  ("vendor-reported", "single-source estimate").

## 3. Citation mechanics

- Web citation format, one parenthesis per sentence, at the end:
  `The claim was denied by both newsrooms. ([News Journal](https://exact.url), [Daily Report](https://exact.url2))`
- The Source cell in the Source Notes table IS the Markdown link: `[Source name](exact URL)`.
- Copy URLs character for character from tool results. Never construct, shorten, or
  normalize a URL. If no usable URL exists, name the source in plain text without a link.
- Internal/private sources: use the reference format the tool returned (e.g.
  `search-result://…`, `doclib://…`). Never fabricate a public URL for an internal source.
- Never cite: local file paths, workspace files, user uploads, canvas files.
- Dates: use the source's own date from the tool result; if none is available, write `-`.
  Never guess a date.

## 4. Conflicts and caveats block (after the source table)

Structure:
1. Name the conflict in one line (which numbers/sources disagree).
2. Explain the methodological cause if identifiable (different definitions, periods, samples).
3. State which figure the report relies on and why.
4. Any access limitations (paywalls, blocked pages, unavailable internal corpora).
