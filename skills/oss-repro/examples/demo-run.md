# Demo — vague report → repro pack

**Input:** "cli bazen patliyo health checkte ubuntu'da"

**Corrected claim:** `cli health` exits non-zero on Ubuntu 22.04 when the daemon is not running.

**Repro pack (excerpt):**

```md
## Repro
- OS: Ubuntu 22.04
- Binary: cli@1.4.2
- Steps:
  1. `cli stop` (ensure daemon down)
  2. `cli health`
- Expected: exit 0 or clear "daemon not running" message
- Actual: panic / exit 1 with (paste)
```
