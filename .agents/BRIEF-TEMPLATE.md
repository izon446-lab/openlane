# BRIEF — <short title>

task: <slug-YYYY-MM-DD>
from: Orchestrator  to: Builder → Reviewer → Gate
repo: <owner/name>   # public only
base: origin/<branch> @ <40-char sha>
requested_by: Turac <ISO date Europe/Istanbul>
risk: low | auth | payments | migration | public-api | infra
forbidden: <deployment; secrets; … rewritten for this repo>
status: READY | BLOCKED
permission: L0 (default)

## Five required
1. **goal:** …
2. **pass/fail:** …
3. **Proof type:** raw HTTP | screenshot | MP4 | before/after metric | N/A (<why>)
4. **risk class:** …
5. **forbidden areas:** …

## AC
- [ ] AC1: …
- [ ] AC2: …

## Notes
- Lane: Builder = Codex CLI; Reviewer = Mistral. No CloudAgent / LazyCodex.
- Do not merge; Gate report decides.

## Rollback
…
