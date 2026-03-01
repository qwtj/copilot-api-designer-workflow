---
name: standardize-errors
description: Produce a standard error response schema and map common HTTP error codes to that schema.
tools: ["read","search"]
agent: "openapi-refinement"
---

Purpose
- Produce a standard error response schema and map common HTTP error codes to that schema.

Input
- Existing error fragments (if any), desired fields (code, message, details, traceId), and localization considerations.

Output
- `diff` fenced YAML adding `components.schemas/Error` and updating common responses (400,401,403,404,500) to reference it.

Rules
- Use RFC-friendly fields: `type`, `title`, `status`, `detail`, `instance` as appropriate. Add `traceId` for observability.
