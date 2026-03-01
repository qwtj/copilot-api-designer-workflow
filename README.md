# API Writer — OpenAPI Design Orchestrator

This repository contains tooling and agent rules for an automated OpenAPI design workflow driven from the `.github` folder.

**Purpose**
- **What:** Coordinate multi-phase OpenAPI design via agents and an orchestrator.
- **Why:** Automate requirement gathering, spec drafting, validation, and refinement to produce a finalized OpenAPI artifact.

**Repository Layout**
- **.github:** Agent rules, orchestrator instructions, and validation/checklists used by the workflow.
- **examples/**: Example projects and handoffs (e.g., `examples/patient_api`).
- **tmp/**: Transient artifacts and outputs produced by agents during runs.

**Key Concepts**
- **Orchestrator:** Central coordinator that reads design state and launches the appropriate agent for the current phase.
- **Agents:** Specialized workers (requirements, drafting, validation, refinement) that produce or modify OpenAPI artifacts.
- **Phases:** A fixed phase-transition table drives which agent runs next and when the workflow completes.

**Workflow (high level)**
- The orchestrator reads a state file in `.github` and selects an agent to run.
- Agents update state, write artifacts into `./tmp`, and may produce diffs or full OpenAPI YAML.
- The final approved phase results in a handoff artifact (e.g., `tmp/handoff.md`).

**Files of Interest**
- `.github/copilot-instructions.md` — Orchestrator & agent rules and expectations.
- `.github/agents/` — Agent definitions and behaviors invoked by the orchestrator.
- `.github/instructions/` — Best-practice and validation checklists used by the validation/refinement agents.

**How to work with this repo**
- Read the orchestrator rules in the `.github` folder before making changes to agents.
- Agents should write all newly created artifacts under `./tmp` to keep outputs separate from source.
- On validation failures, agents should attempt automatic fixes and update state; manual intervention is required only when issues persist.

**Notes & Next Steps**
- Use `examples/` as a reference for expected outputs and final handoffs.
- When adding or changing agents, update the orchestrator rules and the corresponding instruction/checklist files in `.github`.

**Contact**
- Repository maintainers: check repository settings for owner/contact information.
