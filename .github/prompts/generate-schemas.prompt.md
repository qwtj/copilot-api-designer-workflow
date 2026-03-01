Purpose
- Generate reusable `components.schemas` entries from resource descriptions or example payloads.

Input
- Resource name, representative example JSON (optional), fields with types (optional), constraints (min/max, pattern), and usage notes.

Output
- `diff` fenced YAML block containing `components.schemas` entries using JSON Schema draft 2020-12 compatible with OpenAPI 3.1.
- Include `examples` and `nullable`/`nullable`-equivalent annotations where needed.

Rules
- Name schemas using PascalCase: `{Resource}{Entity}`.
- Prefer composition (`allOf`, `oneOf`) for shared pieces; create small shared schemas when repeated.
