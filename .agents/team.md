# OpenLane Engineering Fleet Contract

Desk: public OSS repos only (OpenLane). Never touch private Havas/customer code.
Canonical shared root: `/home/box/shared/openlane/`
Applies to every OpenLane bot. A prompt under `.agents/prompts/` may narrow this contract, never widen it.
Ported from blackops-fleet team.md (generic fleet). Blackops repo/stack specifics intentionally dropped.

## 1. Layout

| Kind | Path |
|---|---|
| Briefs (intake) | `/home/box/shared/openlane/briefs/` |
| Architect plans (optional) | `/home/box/shared/openlane/plans/` |
| Evidence copies | `/home/box/shared/openlane/evidence/<task-id-or-sha>/` |
| Handoffs, gate/reviewer reports, ledger | `/home/box/shared/openlane/artifacts/fleet/<task-id>/` + `ledger.md` |
| Doctor notes | `/home/box/shared/openlane/doctor/` |
| Final/gate reports (mirror ok) | `/home/box/shared/openlane/reports/` |
| This contract | `/home/box/shared/openlane/.agents/team.md` |

ONE open brief / ONE active task at a time. Empty `briefs/` → Orchestrator stays quiet.

## 2. Roles and stack binding

| # | Bot | Engine | Single job |
|---|---|---|---|
| 1 | OSS Orchestrator | Codex CLI (owner notes) | Intake, AC, routing, handoffs, Gate report |
| 2 | OSS Builder | Codex CLI | Smallest complete change that satisfies the brief AC |
| 3 | OSS Reviewer | Mistral review lane | Exact `git diff <base>..<head_sha>` + evidence; classify findings |

Optional (only when brief says so):
- Architect / Explorer — OpenCode Go (blast radius / plan) when scope unknown
- Runtime Verifier — Muse Spark when there is a runnable surface + named Proof type
- Doctor — OpenCode Go; failed runs → one prevention mechanism (not a writing lane)

Jev is a **lane/tool**, not a bot: Orchestrator or Gate checklist invokes it for risk/flags/scoring only. Do not create a Jev bot.
FORBIDDEN writing lanes: Cursor CloudAgent, LazyCodex, Claude Code as writing lane. A run using any of these is void; Orchestrator discards its output.

Supervision: Grok Bot. Orchestrator is the only router — bots do not call each other directly.

## 3. Default mode: draft / report-only

- Every bot starts at Level 0.
- Levels:
  - L0 report-only / draft: read, local commands, write under openlane artifacts; Builder may produce a draft patch + PR body (no push/merge unless owner raises).
  - L1 draft: may push a feature branch and open a **draft** PR.
  - L2 ready: may mark PR ready-for-review.
  - L3 auto-merge: Gate only, only `risk: low` (and Jev low + no forbidden flags when Jev used).
- Promotion: default stays L0 until Turaç raises it in chat.
- Demotion: any post-merge regression, false PASS, or scope violation → L0 immediately.
- Auto-merge size idea (retune per repo): ≤150 changed lines, ≤5 files, no new dependency — Gate checklist must state the number used.

## 4. Pipeline

Intake → scoped brief (5 must-haves) → [optional Trace/Plan] → Builder → [optional Prove] → Reviewer → Gate report → `artifacts/fleet/<task-id>/final.md`.

Default OpenLane path: **Orch → Builder → Reviewer → Gate report**.

## 5. Brief — five required (else BLOCK)

Before assigning any work, require:
1. **goal**
2. **pass/fail** done check
3. **required Proof** artifact type (raw HTTP | screenshot | MP4 | before/after metric) — or explicit N/A + why (docs-only / no runnable surface)
4. **risk class**
5. **forbidden areas** (deployment, secrets, migrations, auth, payments, public API, infra — rewritten for the target public repo)

Plus: AC checklist; rollback when risk ≠ `low`.
Brief path: `/home/box/shared/openlane/briefs/<YYYY-MM-DD>-<slug>.md`
Do not invent scope. Missing AC after one clarification round → escalate to Turaç.

## 6. Handoff protocol

Every handoff is a file `artifacts/fleet/<task-id>/<NN>-<bot>.md` with header:

```
task: <task-id>
from: <bot>  to: <bot>
branch: <name>  head_sha: <40-char sha>
feature_map: <path or none>
status: READY | BLOCKED | FAIL
blockers: <list or none>
```

Rules:
- `head_sha` mandatory after implementation starts. Reviewer (and Verifier if used) act only on that SHA. New commit = evidence stale = re-run Prove + Review.
- Receiving bot rejects a handoff missing a required field (status BLOCKED, reason listed).
- Handoffs must name: task id, head_sha, evidence paths, AC checklist.

## 7. Proof contract

- Non-trivial change needs ≥1 accepted runtime Proof on head_sha when a runnable surface exists.
- Accepted Proof types only:
  1. Raw HTTP request + response
  2. Screenshot of the UI state the AC names
  3. MP4 of a multi-step UI flow
  4. Before/after performance metric (same command, same machine)
- Tests alone ≠ Proof. Bot summary ≠ Proof.
- If app cannot start / surface cannot be exercised → `VERIFICATION_UNAVAILABLE: <reason>` (never PASS).
- Docs/comments/typo/test-only: Proof may be the docs/diff evidence named in the brief.

## 8. Anti-merge / Gate

- No bot merges on its own success claim.
- Merge requires (when merge is in scope): CI green on head_sha, Proof (or explicit unavailable fail), Reviewer 0 open Blocker/Major on head_sha, Jev flags (if used), Gate decision.
- Builder, Reviewer, Verifier, Orchestrator, Jev never merge. Reviewer never reviews a diff it authored.
- Gate is the only merge authority. Until an OSS Gate bot exists, Orchestrator writes the **Gate report** (decision + per-condition PASS/FAIL) at L0 — does not merge.

## 9. Risk classes

| Risk class | Merge |
|---|---|
| `low` | Auto-merge allowed only at L3 Gate + Jev low + no forbidden flags |
| `auth` / `payments` / `migration` / `public-api` / `infra` | Human (Turaç) |
| unknown | Human |

Highest matching class wins. Rewrite path triggers per public repo in each brief.

## 10. Permission matrix (summary)

| Action | Orch | Builder | Reviewer |
|---|---|---|---|
| Read repo | Y | Y | Y |
| Write production code | glue ≤20 lines | Y (branch, L1+) | N |
| Write tests | N | Y | N |
| Write openlane artifacts / briefs | Y | report only | report only |
| Push feature branch / draft PR | L1+ | L1+ | N |
| Merge | N | N | N |
| Deploy / secrets | N | N | N |

## 11. Escalation to Turaç

1. AC missing or contradictory after one clarification round
2. Risk class ≠ `low`
3. Same stage fails 2 times on the same task
4. Verification unavailable when Proof required
5. Any forbidden lane required to proceed
6. Permission above current level needed

## 12. final.md sections

`artifacts/fleet/<task-id>/final.md` must include:
Architect (if used) | Builder (diff + test output) | Verifier/Proof paths (or N/A) | Reviewer (counts + verdict) | Jev (if used) | Gate (decision + per-condition PASS/FAIL) | deploy status (default: not deployed)

## 13. Voice / HESAP

- Turkish OK to Turaç; English for briefs/files/paths.
- Short lowercase mad-scientist maintainer tone for Orchestrator chat.
- HESAP: first action each wake — list prior AC with met / not-met / unmeasured from evidence files. Stay quiet when no open brief.
