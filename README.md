# OpenLane

**Open-source agent desk for small, verified PRs.**

Public repo: https://github.com/izon446-lab/openlane

One public-repo task at a time. Invent freely, verify strictly.

```
  issue / ask
       │
       ▼
┌─────────────┐   brief + AC    ┌─────────┐   patch + evidence   ┌──────────┐   Gate report
│ Orchestrator│ ──────────────► │ Builder │ ──────────────────► │ Reviewer │ ─────────────► decision
└─────────────┘                 └─────────┘                      └──────────┘
```

No CloudAgent. No LazyCodex. A green test suite alone is **not** Proof.

---

## Seats

| Seat | Job |
|------|-----|
| **Orchestrator** | Intake → one brief → handoffs → Gate report |
| **Builder** | Smallest change that meets AC; leave evidence |
| **Reviewer** | Exact `base..head` diff + evidence; Blocker / Major counts |

Optional when the brief says so: Architect (blast radius), Verifier (runtime Proof), Doctor (one prevention after repeated failure).

Jev is a scoring **lane**, not a seat.

---

## Desk layout

```
openlane/
  README.md
  .agents/
    team.md              # fleet contract (canonical)
    BRIEF-TEMPLATE.md
    HANDOFF-TEMPLATE.md
  briefs/                # one open brief at a time
  plans/                 # optional design traces
  evidence/              # Proof / review artifacts per task
  artifacts/fleet/       # handoffs, final.md, ledger
  reports/               # human-facing digests
  doctor/                # failure patterns
  skills/                # public skill packs (see skills/README.md)
```

Shared root on the box: `/home/box/shared/openlane/`

---

## Skills

### Maintainer lane (OSS PR pipeline)

| Skill | When |
|-------|------|
| `oss-intake` | Issue / ask → one Orchestrator brief |
| `oss-proof` | Start the real app, capture Proof |
| `oss-review-diff` | Adversarial exact-diff review |
| `oss-maintainer-gate` | CI + Proof + review → merge decision |

### Research & prompt lane (public packs)

| Skill | When |
|-------|------|
| [`prompt-fixer`](skills/prompt-fixer/) | Messy / mixed-language / stream-of-consciousness ask → clean structured prompt |
| [`deep-research-pro`](skills/deep-research-pro/) | Source-backed deep research → cited canvas report |
| [`oss-repro`](skills/oss-repro/) | Vague bug report → minimal copy-paste reproduction |
| [`decision-memo`](skills/decision-memo/) | Evidence → one-page ship/wait/kill decision |


---

## Brief — five required (else BLOCK)

1. **goal**
2. **pass/fail** done check
3. **Proof type** — raw HTTP \| screenshot \| MP4 \| before/after metric (or explicit N/A)
4. **risk class** — `low` \| `auth` \| `payments` \| `migration` \| `public-api` \| `infra`
5. **forbidden areas** — rewritten for that public repo

Plus AC checklist; rollback when risk ≠ `low`.

---

## Proof

Accepted runtime Proof on `head_sha` only:

1. Raw HTTP request + response  
2. Screenshot of the UI state the AC names  
3. MP4 of a multi-step UI flow  
4. Before/after metric (same command, same machine)

Tests alone ≠ Proof. Bot summary ≠ Proof.

---

## Merge bar (low risk)

All must PASS on the **same** `head_sha`:

1. risk `low` + no forbidden flags  
2. required CI green  
3. ≥1 accepted Proof artifact (or docs-only Proof named in the brief)  
4. Reviewer Blocker = 0 and Major = 0  
5. ≤150 lines / ≤5 files / no new dependency (retune per repo)  
6. no deploy without a human naming the SHA  

Default autonomy is **L0** (draft / report). Gate never merges until promoted.

---

## Contract

Full rules: [`.agents/team.md`](.agents/team.md)

Ported from the Blackops fleet pattern (generic parts only). Public repos only — never private Havas / customer code.

---

## License

MIT — invent freely, verify strictly.

---

*OpenLane OSS desk. Not affiliated with any company product.*
