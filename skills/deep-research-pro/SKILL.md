---
name: deep-research-pro
description: Load this skill for thorough, Perplexity-level deep research. Triggers on requests for thorough investigation, source-backed briefs, market or technical landscape analysis, evidence-based comparisons, fact-checking, "araştır", "deep research", "rapor hazırla", or when the user wants a polished research report with citations. Handles advisor-critiqued research planning, iterative multi-angle search, source credibility scoring, conflicting evidence resolution, and structured report output. On first load, read references/workflow.md, references/source-standards.md and references/report-templates.md. For a full worked example, read examples/demo-run.md.
---

# Deep Research Pro

Perplexity-level, source-backed deep research engine. Break the user's question into
answerable sub-questions, run an iterative multi-pass search, score source credibility,
surface conflicting evidence, and produce a decision-ready report on a canvas.

## Stage 0 — Advisor Pass (run before anything else)

Adopt the persona of a skeptical senior analyst and critique the request BEFORE researching:

- **Framing**: Is the question the user actually needs answered, or just the one they typed?
- **Decision gap**: Which decision does this research support? If unknown, assume and flag.
- **Scope bias**: Too broad to answer, or too narrow to be useful?
- **Metric ambiguity**: Implicit assumptions like "better" — better by which metric?
- **Failure modes**: Stale data, paywalled sources, speculative topic — identify upfront.

List each advisor comment as a bullet, write the corrective action next to it
(add/remove a sub-question, define the metric, change source type), and update the plan
accordingly. Summarize the advisor verdict to the user in 2-3 lines before searching.
If the user pushes back on an advisor comment, the user wins.

## Stage 1 — Decompose

- Rewrite the research goal as a single-sentence "Research Question" in your own words.
- Split it into 3-6 independently searchable sub-questions.
- Assign each sub-question its expected source type (official statistics, academic paper,
  industry report, news, filings, documentation, primary data).
- Clarify scope: geography, time horizon, industry, audience, and the decision it supports.
  Ask via `ask_user_question` ONLY if a gap materially changes the result; otherwise assume
  and flag the assumption in the report.
- If the user's message is messy or scattered, load the `prompt-fixer` skill first and let
  it produce the corrected brief.

## Stage 2 — Research Plan

For broad or high-stakes requests, write a 4-6 line plan before executing: main search
angles, source types, whether internal/company sources are needed, which angles are secondary.

## Stage 3 — Iterative Search Loop

Multi-pass, Perplexity-style. Never stop at one search round:

1. **Discovery pass** — broad queries to map the topic (2-4 queries, run in parallel).
2. **Targeted pass** — one specific query per sub-question; hunt primary sources.
3. **Deep-dive pass** — open strong results with `open_url` and read the source. Never cite
   a claim that depends on details beyond the snippet without opening the source.
4. **Gap pass** — new queries for unanswered sub-questions and conflicting claims. Continue
   until every sub-question is answered or a genuine blocker remains.
5. **Freshness check** — for fast-moving topics (prices, regulation, products, current
   events) use `recency_days` and record source dates.

Routing: public info → web search; recent news → news search; internal/private/company
info → connected integrations (Notion, Slack, Drive, Gmail, Outlook, SharePoint); user
files → read the files first. Choose corpora deliberately per query; when in doubt, leave
corpora unset to search everything connected.

## Stage 4 — Evidence Discipline

Track while working: source title, URL/internal reference, date, source type, key claims,
credibility note. Full scoring rubric in `references/source-standards.md`.

- Cross-check important claims across at least 2 independent sources.
- Never hide conflicts: show both numbers and explain which survey definition or
  methodology causes the divergence.
- Keep verified facts, estimates, opinions, and your own inference clearly separated.

## Stage 5 — Synthesis & Report

Load the `canvas` skill and deliver the report as a canvas (default `text/markdown`;
slides/dashboard/table if requested). Report language: the language of the user's request,
used consistently including all headings and the source table.

Required structure: Research Question, Executive Summary (3-7 ranked takeaways),
Methodology, Findings (organized by theme, every claim cited), Source Notes (mandatory —
Source / Credibility (n/5) / Last updated columns; Markdown links in the Source cell;
"-" when the date is unknown), Open Questions, Recommendations / Next Steps.
Templates in `references/report-templates.md`; a full worked example in `examples/demo-run.md`.

## Hard Rules

- One citation parenthesis per sentence, at the end: ([Source](url)).
- Never cite a source you did not inspect when the claim depends on details beyond its snippet.
- Never turn local file paths, workspace files, or user files into Markdown links or cite them.
- Never invent, guess, or normalize URLs. Use exact URLs from inspected sources only.
- After creating the canvas, send only a brief chat summary — never paste the full report.
