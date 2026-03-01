---
name: start-orchestrator
description: Start the orchestrator with a provided requirements or OpenAPI file; returns a handoff JSON for the next agent.
tools: ["read", "agent"]
agent: "openapi-orchestrator"
---

Purpose
- Deterministic, idempotent prompt to start or resume the orchestrator with an explicit artifact path.

Inputs (one required)
- `requirements_path`: path to a YAML requirements file (e.g., .github/requirements.yaml)
- `openapi_path`: path to an existing openapi.yaml to resume (optional)
- `initiator`: actor id (e.g., "user:alice")
- `desired_next_phase`: optional override: one of ["requirements-gathering","spec-drafting","refinement","validation","final-review"].

Behavior
1. Read `.github/openapi-design-state.json` via `manage-state`.
2. Validate exactly one of `requirements_path` or `openapi_path` is provided; if invalid return an error object (see output shape).
3. If `requirements_path` provided: set `phase` -> `requirements-gathering`, record artifact and history entry, and hand off to `openapi-requirements` with `{requirements_path, initiator, timestamp}`.
4. If `openapi_path` provided: set `phase` -> `desired_next_phase||validation`, record artifact and history entry, and hand off to the appropriate agent (`openapi-validation` or `openapi-refinement`).
5. Persist only the state changes via `manage-state` (do not apply spec diffs here).

Output contract (always JSON)
- On success:
  {
    "action": "handoff",
    "to_agent": "<agent-name>",
    "payload": { ... },
    "state_patch": { ... },
    "notes": "short reason"
  }
- On input error:
  { "error": "exactly one of requirements_path or openapi_path required" }

Reentrancy
- Running this prompt multiple times with the same inputs must be idempotent (no duplicate history entries for identical requests).

Example
- Input: `{ "requirements_path": ".github/requirements.yaml", "initiator":"user:alice" }`
- Output:
  {
    "action":"handoff",
    "to_agent":"openapi-requirements",
    "payload":{"requirements_path":".github/requirements.yaml","initiator":"user:alice","timestamp":"2026-02-28T12:00:00Z"},
    "state_patch":{"phase":"requirements-gathering","status":"pending","artifacts":{"requirements":".github/requirements.yaml"}},
    "notes":"Starting requirements-gathering"
  }
