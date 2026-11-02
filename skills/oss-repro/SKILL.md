---
name: oss-repro
description: Use when an open-source bug report needs a minimal reproduction, when someone says "repro", "nasıl reproduce", "minimal example", or before filing/confirming a public-repo bug. Turns vague reports into a copy-paste repro (steps, commands, expected vs actual, environment). On first load read references/repro-checklist.md; worked example in examples/demo-run.md.
---

# OSS Repro

Turn a fuzzy bug report into a **minimal, runnable reproduction** a maintainer can execute in under five minutes.

## Steps

1. **Extract the claim** — one sentence: what breaks, for whom, since when.
2. **Strip noise** — drop unrelated stack, opinions, and "it used to work" without a version. Keep versions, OS, commands, and the smallest input that triggers the failure.
3. **Write the repro pack** (user's language for prose; English for commands/paths):
   - Environment: OS, runtime, package versions (`node -v` / `python --version` / lockfile hash if known)
   - Prep commands (clone, checkout SHA, install)
   - Exact steps numbered
   - Expected vs actual (paste raw output; never paraphrase errors)
   - Minimal fixture (smallest file/snippet; no full project dump)
4. **Advisor pass** — max 3 bullets: is this still too big? missing a version? conflating two bugs? Fix the pack before delivering.
5. **Deliver** — markdown block ready to paste into a GitHub issue. If the user asked you to open the issue, draft only (L0); do not post unless they explicitly said to send without preview.

## Hard rules

- Prefer a failing command over a long narrative.
- One bug per repro. Split if two failures appear.
- Never invent stack traces or exit codes. Mark unknowns as `unknown — please fill`.
- Public repos only for OpenLane; no private/customer dumps.

See `references/repro-checklist.md` and `examples/demo-run.md`.
