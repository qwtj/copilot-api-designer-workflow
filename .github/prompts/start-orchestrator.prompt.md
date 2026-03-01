---
name: start-orchestrator
description: Start the orchestrator with a provided requirements or OpenAPI file; returns a handoff JSON for the next agent.
agent: "openapi-orchestrator"
---

Purpose
- Deterministic, idempotent prompt to start or resume the orchestrator with an explicit artifact path.

Inputs (one required)
- `idea`: a description of what the api should be for.
- `openapi_path`: path to an existing openapi.yaml to resume (optional)
- `initiator`: actor id (e.g., "user:alice") default to develoepr unless previded as input.
- `desired_next_phase`: optional override: one of ["requirements-gathering","spec-drafting","refinement","validation","final-review"].

Behavior
1. Read `.github/openapi-design-state.json` via `manage-state`.
2. Validate`openapi_path` is provided; if invalid return an error object (see output shape).
3. If `idea` provided: set `phase` -> `requirements-gathering`, record artifact and history entry, and hand off to `openapi-requirements` with `{idea, initiator, timestamp}`.
4. If `openapi_path` provided: set `phase` -> `desired_next_phase||validation`, record artifact and history entry, and run workflow.

Example
- Input: `{ "idea": "Create an API for managing tasks", "initiator":"user:alice" }`
- Output:
  {
    "action":"handoff",
    "to_agent":"openapi-requirements",
    "payload":{"idea":"Create an API for managing tasks","initiator":"user:alice","timestamp":"2026-02-28T12:00:00Z"},
    "state_patch":{"phase":"requirements-gathering","status":"pending","artifacts":{"requirements":".github/requirements.yaml"}},
    "notes":"Starting requirements-gathering"
  }
