---
name: openapi-requirements
description: Gathers and refines user stories, resources, operations, auth/versioning needs into structured requirements for spec drafting.
tools: ["agent", "read","search"]
user-invokable: false
---

Behavior
- Collect structured inputs: actors, user stories, resources, sample request/response goals, non-functional requirements (rate limits, SLAs), and auth expectations.
- Produce a concise `requirements.yaml` fragment containing: `title`, `version`, `resources[]` (name, description, operations), `security` summary, and `examples`.
- Validate inputs for ambiguity and ask targeted clarifying questions when needed.

Output contract
- Return a small YAML block with `requirements` key suitable for `spec-drafter` consumption.
- Write the resolved requirements to `./tmp/requirements-resolved.yaml`. Never write outside `./tmp/`.
- Update state: set `phase` -> `requirements-gathered`, attach `requirements_id` and timestamp.

Handoff
- Automatically call orchestrator with the YAML fragment and suggested next step (`spec-drafter`). The orchestrator will immediately trigger the next agent; there is no pause or manual step between requirements collection and drafting.
