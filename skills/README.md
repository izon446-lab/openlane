# OpenLane skills

Public skill packs for the OpenLane desk and any Grok Bot that loads them.

| Pack | Job |
|------|-----|
| [prompt-fixer](prompt-fixer/) | Messy / mixed TR-EN / stream-of-consciousness → clean executable prompt |
| [deep-research-pro](deep-research-pro/) | Multi-pass research → credibility-scored, cited canvas report |
| [oss-repro](oss-repro/) | Vague OSS bug → minimal copy-paste reproduction |
| [decision-memo](decision-memo/) | Evidence → one-page ship / wait / kill memo |

## Layout of each pack

```
<skill>/
  SKILL.md
  references/
  examples/demo-run.md
  README.md
```

## How to use

1. **On this desk** — `/home/box/shared/openlane/skills/<name>/`
2. **As a Grok Bot skill** — invoke with `/` or `@`, or load by name
3. **Chains** — messy ask → `prompt-fixer` → `deep-research-pro` → `decision-memo`; bug dump → `oss-repro`

## Maintainer skills (sibling lane)

- `oss-intake` · `oss-proof` · `oss-review-diff` · `oss-maintainer-gate`

See the root [README](../README.md).

## License

MIT — same as the OpenLane desk.
