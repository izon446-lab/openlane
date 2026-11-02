---
name: decision-memo
description: Use when the user needs a decision-ready one-pager — "karar notu", "decision memo", "ne yapalım", ship/wait/kill, or after deep research when they must pick an option. Compresses evidence into options, tradeoffs, recommendation, and kill-criteria. On first load read references/memo-template.md; worked example in examples/demo-run.md.
---

# Decision Memo

Compress research or a messy debate into a **one-page decision memo** a human can act on.

## Steps

1. **Name the decision** — one sentence: what must be chosen by when.
2. **Options** — 2–4 mutually exclusive options (include "do nothing"). No strawmen.
3. **Tradeoffs table** — rows = criteria the decision actually cares about; columns = options. Prefer numbers/dates over adjectives.
4. **Recommendation** — one option + why (3–5 lines). State the biggest risk if wrong.
5. **Kill / revisit criteria** — what evidence would flip the call; review date.
6. **Advisor pass** — check for hidden fifth option, missing criterion, or recommendation that ignores the table. Fix before deliver.
7. **Deliver** — prefer a short canvas or markdown memo. If prior work used `deep-research-pro`, cite its Source Notes; do not invent new URLs.

## Hard rules

- Never hide uncertainty; label estimates.
- Do not implement the decision unless the user explicitly asks after the memo.
- Language matches the user (Turkish OK); keep option labels stable in English if they are code/product names.

Template: `references/memo-template.md`. Example: `examples/demo-run.md`.
