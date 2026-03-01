Orchestrator & Agent rules (glue)

## Core Principle: FULLY AUTOMATIC — Never pause for human approval between phases.

### Orchestrator Responsibilities
1. Read `.github/openapi-design-state.json` to determine current phase.
2. Immediately launch the correct agent for that phase via `runSubagent` — NO waiting, NO asking user.
3. After each agent completes, update state and automatically launch the next agent.
4. Continue chaining agents until `final-approved` is reached, then produce `tmp/handoff.md`.

### Phase Transition Table (follow exactly, no deviations)
| Current Phase         | Agent to Launch          | Next Phase             |
|-----------------------|--------------------------|------------------------|
| `idea`                | `openapi-requirements`   | `requirements-gathered`|
| `requirements-gathered` | `openapi-spec-drafter` | `spec-drafted`         |
| `spec-drafted`        | `openapi-validation`     | `validation-complete`  |
| `validation-complete` | `openapi-refinement`     | `refined`              |
| `refined`             | `openapi-validation`     | `final-approved` (if no blocking issues) or `validation-complete` (if issues remain, max 2 retries) |
| `final-approved`      | _(none — write handoff)_ | done                   |

### Agent Rules
- Agents output YAML as a `diff` (preferred) or full `openapi.yaml` block — always clearly labelled.
- For validation findings: auto-apply all fixes immediately. Do NOT stop to ask for approval.
- Keep prompts reentrant: re-running an agent on the same inputs produces stable, minimal diffs.
- All new artifacts go in `./tmp`.
- After `final-approved`, orchestrator writes `tmp/handoff.md` summarising the spec for implementers.

### State Updates
- After each agent completes, write updated phase and status to `.github/openapi-design-state.json`.
- Append a history entry: `{ "phase": "...", "agent": "...", "timestamp": "..." }`.

ALL ARTIFACTS NEWLY CREATED BY AGENTS MUST BE IN `./tmp`