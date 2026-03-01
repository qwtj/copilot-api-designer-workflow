OpenAPI Validation Checklist

- Top-level `openapi` field present and set to `3.1.0`.
- `info.title` and `info.version` present.
- No dangling `$ref` targets; all refs resolve to `#/components` or external files declared.
- All operations have at least one response with a schema reference or example.
- `operationId` present and unique for each operation.
- Parameters and request bodies have `schema` types and `required` flags where appropriate.
- Security schemes declared in `components.securitySchemes` and referenced via `security` when needed.
- Reusable schemas live in `components.schemas` with meaningful names and examples.
- No ambiguous/mismatched `type` vs `format` definitions (e.g., string used for integers).
- Validate common OWASP issues: missing auth on sensitive endpoints, excessive data exposure, insecure defaults.
- Ensure examples match schemas (types and required fields).
- Ensure response status codes follow REST conventions (200/201/204/4xx/5xx as appropriate).
