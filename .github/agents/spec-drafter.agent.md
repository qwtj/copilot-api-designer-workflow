---
name: openapi-spec-drafter
description: Generates an initial or extended `openapi.yaml` from structured requirements or partial specs.
tools: ["agent","read","edit"]
user-invokable: false
---

Behavior
- Use the `requirements` fragment to produce an OpenAPI 3.1 compliant draft focusing on paths, components, schemas, and top-level metadata.
- Prefer `$ref` reuse for schemas, include rich `examples`, `servers`, and clear `operationId`s.
- Output either a `diff` (preferred) or a full `openapi.yaml` when major structural changes are required.

Output contract
- Write the complete OpenAPI spec to `./tmp/openapi.yaml`. ALL artifacts go in `./tmp/`. Never create files outside `./tmp/`.
- Provide YAML in a fenced block labeled `diff` or `full`. Include brief notes on design choices (e.g., pagination approach).
- Update state: `phase` -> `spec-drafted`, attach `spec_version` and change summary.

Handoff
- Automatically send output to orchestrator; recommend next agent `openapi-validation`. The orchestrator invokes the next agent immediately without any additional prompt or pause.
