# Prompt Fixer — Interpretation Rules Reference

Support file for `prompt-fixer`. Common patterns in fast, scattered writing and how to
read them. Examples use Turkish because that is the primary language of this skill's user,
but the rules apply to any language.

## 1. Typo and phonetic-writing patterns (read-through, not correct-through)

Mental auto-correction is enough; never produce a spelling lecture:

| Written | Read as |
|---|---|
| "araştır", "arrastir", "arastir" | "araştır" (research) |
| "benm", "bnm" | "benim" (my) |
| "yapver", "yapiversen" | "yapıver" (go ahead and do it) |
| "bi", "bisi", "bşy" | "bir", "bir şey" (something) |
| "sonrasnda", "snrsnde" | "sonrasında" (afterwards) |
| "cikart", "ckrt" | "çıkar" (produce/extract) |
| "kime gidecek" vs "kim gidecek" | resolve from context (recipient vs. person) |
| Mixed: "bi brief lazım ama solid olsun" | goal in Turkish, quality bar in English — both stand |

## 2. Intent signals in thought-dumps

Scattered messages still carry structural signals:

- **The deliverable usually appears near the end**: "…investorlere gidecek" → output
  constraint (investor-facing deck/brief), even though it was the last fragment.
- **Question marks set the frame; imperative verbs set the task.** "büyük mü?" frames,
  "girsek mi?" decides, "özet çıkar" tasks.
- **Repeated nouns are the real subject.** If "pazar" appears three times, the report is
  about the market, not the drones mentioned once.
- **Audience hints**: "investorlere", "müşteriye", "ekibe", "hocaya" — each changes tone,
  format, and depth. Default: professional but plain.
- **Urgency hints**: "acil", "bugün", "hemen", "yarın sunum" — compress scope, prefer
  chat-answer or quick-turnaround mode over a full canvas report.
- **Casual tone ≠ low stakes.** "bakiver" can precede an investor decision; treat content
  seriously regardless of tone.

## 3. Context completion order

When the message references something unspecified, complete context in this order:
1. The current conversation (previous turns, previous canvases and artifacts).
2. Personal knowledge folders (only those whose descriptions plausibly match).
3. The filesystem (recent uploads, canvases).
4. If still unresolved → this is a candidate critical gap (Step 2), not an excuse to guess
   when the choice materially changes the result.

## 4. Assumption ledger

Keep implicit assumptions in a short ledger while working; surface the important ones in
one closing line:

- Language: match the user's message language unless told otherwise.
- Tone: professional-plain by default; playful only if the user's own tone clearly is.
- Length: "özet/brief" → 1-2 pages; "rapor" → full structure; "kısa" → chat answer.
- Format: default to canvas for reports/decks/tables; chat for quick answers and lists.
- Currency/locale: user's locale (Türkiye: TRY, dd.mm.yyyy, VAT rules) unless stated.

## 5. When to actually ask

Ask (max 2-3 questions, with options) ONLY when the answer materially changes the output:
- Which of several files/sources/documents the task refers to.
- Where the output is going (private note vs. client vs. investor vs. public post).
- Hard constraints: budget, deadline, legal/compliance boundaries, confidentiality.
- Two readings of the same sentence that lead to genuinely different deliverables.

Everything else → assume, mark, proceed.
