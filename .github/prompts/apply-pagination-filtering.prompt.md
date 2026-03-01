---
name: apply-pagination-filtering
description: Apply consistent pagination, filtering, and sorting patterns to list endpoints and add a paginated envelope.
tools: ["read","search"]
agent: "openapi-refinement"
---

Purpose
- Apply consistent pagination, filtering, and sorting patterns to list endpoints.

Input
- Target path (e.g., `/pets`), current operation fragment, and preferred pagination style (`offset`, `cursor`, or `page`).

Output
- `diff` fenced YAML that adds request `parameters` (query), response `schema` references (paged envelope), and examples.

Rules
- Use `limit`/`offset` for `offset` style; include `nextCursor` for `cursor` style.
- Provide a reusable `components/schemas/Paginated{Resource}` envelope.
