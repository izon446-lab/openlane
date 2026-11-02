# Deep Research Pro — Detailed Workflow Reference

Support file for `deep-research-pro`. Read when you need execution depth beyond the SKILL.md summary.

## 1. Advisor Pass — detailed checklist

Run this as a written critique before any search. Output format:

```
ADVISOR PASS
- Framing: [is the typed question the real question? if not, state the real one]
- Decision: [what decision does this support? assumed if unknown → FLAG]
- Scope: [too broad / too narrow / acceptable — with the corrective action]
- Metrics: [ambiguous terms found ("better", "top", "cheaper") and the metric chosen]
- Failure modes: [stale data risk, paywall risk, speculative topic, thin sources]
VERDICT: [1-2 lines: what the plan will do differently because of this critique]
```

Common corrective actions:
| Advisor finding | Corrective action |
|---|---|
| Question is a proxy for a decision | Add a sub-question about the decision criteria |
| No metric defined | Pick a defensible metric and state it in Methodology |
| Scope too broad | Pick 1-2 representative segments, mark the rest as Open Questions |
| Scope too narrow | Add the adjacent driver/competitor/regulation sub-question |
| Fast-moving topic | Set `recency_days` in every search and prefer sources < 12 months old |
| Internal context likely exists | Search connected corpora, not just the web |

## 2. Sub-question quality bar

A good sub-question is:
- **Answerable** by an inspectable source, not by opinion alone.
- **Sized** to one fact-cluster (not "the market", but "market size and growth rate, 2024-2026").
- **Assignable** to an expected source type before searching.
- **Conflict-aware**: if two source types will disagree (vendor blogs vs. regulator data),
  split it into "what vendors claim" and "what independent data shows".

Bad: "Is AI popular?" → Good: "What share of knowledge workers use AI daily, by latest survey?"

## 3. Search pass mechanics

- **Discovery pass**: 2-4 broad queries, parallel. Goal: vocabulary, key players, competing framings.
  Do NOT cite from this pass except for orientation.
- **Targeted pass**: one query per sub-question. Include entity names, years, units
  ("survey", "statistics", "regulation", "benchmark") in the query.
- **Deep-dive pass**: open the top 1-3 results per sub-question. Extract exact figures, dates,
  methodology notes. If a page fails to open, say so and fall back to the next source — never
  cite the unopened one.
- **Gap pass**: for each still-unanswered sub-question, write 2 alternative query formulations
  (synonyms, English + user's language, site-specific terms). Stop only when: (a) answered,
  (b) repeated searches return nothing new, or (c) sources are paywalled/blocked — then mark
  it in Open Questions, not as a failure to hide.
- Budget attention: high-stakes claims get the deep-dive treatment; orientation claims can
  survive on discovery-pass snippets if the source is authoritative and the claim is uncontroversial.

## 4. Cross-checking protocol

- Tier-1 claims (numbers, legal thresholds, prices, dates): 2 independent sources minimum,
  and the two must not share an origin (a blog citing a report does not count as independent
  from the report).
- Divergence handling: report both figures, attribute each to its source and definition,
  and state which one you relied on and why. Example pattern: "Pew reports 21% (share of work
  done with AI), Gallup 50% (used at least a few times a year) — the definitions differ,
  so both are correct."
- Freshness tie-break: when sources conflict and recency differs, prefer the more recent
  primary source and note the superseded figure.

## 5. Common failure modes and fixes

| Failure mode | Symptom | Fix |
|---|---|---|
| Snippet-citation | Citing details that were not in the snippet | Open the source or drop the claim |
| Source laundering | Citing a blog that cites the real source | Cite the original; name the blog only as discovery |
| Single-source number | One vendor's ROI claim presented as fact | Label as vendor-reported, score credibility ≤3/5 |
| Scope drift | Report answers a broader question than asked | Re-read the Research Question before synthesis |
| Language mismatch | Report language drifts to source language | Fix output language at synthesis; sources stay as-is |
| Canvas afterthought | Report pasted in chat, canvas skipped | Canvas is mandatory; chat gets only the summary |
