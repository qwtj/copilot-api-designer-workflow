---
name: initial-spec-from-requirements
description: Deterministically convert a structured requirements YAML fragment into an initial OpenAPI 3.1 diff patch.
---

Purpose
- Deterministically convert a structured `requirements` YAML fragment into an initial OpenAPI 3.1 `diff` patch.

Input (required)
- `requirements` YAML block including: `title`, `version`, `resources[]` (name, summary, operations[]), `security` summary, and `examples`.

Output (format)
- A single fenced YAML block labelled `diff:` containing minimal top-level keys to be merged into `openapi.yaml` (`openapi`, `info`, `servers`, `paths`, `components`).
- Keep expansions small and reentrant; do not output full large examples unless explicitly requested.

Deterministic rules
- Use `operationId` in the form `{resource}_{operation}`.
- Reuse component names as `#/components/schemas/{Resource}{Entity}`.
- Prefer `200`/`201`/`204` HTTP codes consistent with REST semantics.

Example output snippet
```yaml
diff: |
  openapi: 3.1.0
  info:
    title: Pets API
    version: 1.0.0
  paths:
    /pets:
      get:
        operationId: pets_list
        summary: List pets
```
