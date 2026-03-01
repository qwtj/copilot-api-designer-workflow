Orchestrator & Agent rules (glue)

- The orchestrator MUST read `.github/openapi-design-state.json` before deciding the next action.
- Agents must output YAML changes as either a small `diff` (preferred) or a `full` `openapi.yaml` block. Always label blocks clearly.
- Use the `manage-state` skill to persist phase transitions and `yaml-manipulation` for merges.
- Keep prompts reentrant: agents should be able to re-run against the same inputs and produce stable, minimal diffs.
- For any validation failure, produce `findings` JSON and suggested `diff` fixes; do not auto-apply without orchestrator approval.
- Use `runSubagent`: after `final-approved`, orchestrator prepares a `handoff.md` summary for implementers.
