# Project Workflow (not GitHub Actions)

This repository uses a **custom, agent-driven workflow** built entirely from files under `.github/`.

- The term “workflow” refers to the chain of prompts, agent definitions, and state management.
- The orchestrator triggers each phase automatically; there are no manual handoffs or scriptable pauses.
- Do _not_ confuse this with GitHub Actions workflows. There is **no** `.github/workflows` logic here.

All modifications to the workflow should occur by editing the agent or prompt files in `.github/`. The orchestrator reads `openapi-design-state.json` to persist progress and knows to transition immediately to the next phase.
