---
name: manage-state
description: Provides a consistent interface for agents to read and update the shared design state in `.github
---
Purpose
- Provide concise, deterministic read/write/update patterns for `.github/openapi-design-state.json` so agents can persist progress.

API (pseudo)
- `read_state()` -> returns JSON state.
- `update_state(patch)` -> merges `patch` into state and appends an entry to `history` with `{ts, actor, change}`.
- `set_phase(phase, details)` -> convenience to set `phase` and write `lastUpdated`.

Example JSON patch
```json
{
  "phase": "initial-spec-drafted",
  "current_agent": "openapi-spec-drafter",
  "status": "drafted paths for pets",
  "lastUpdate": "2026-02-28T12:00:00Z"
}
```

Notes
- Keep writes idempotent and small. Always include `actor` and timestamp in history entries.
