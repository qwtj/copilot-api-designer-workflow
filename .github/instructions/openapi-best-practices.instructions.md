OpenAPI Best Practices (concise)

- Use OpenAPI 3.1.0 and JSON Schema 2020-12 for full JSON Schema expressiveness.
- Naming: use plural resource paths (`/pets`), concise `operationId`s (`pets_list`), and PascalCase for schema names (`Pet`, `PetList`).
- Reuse: centralize shared pieces under `components` and prefer `$ref` links to avoid duplication.
- Descriptions: include clear `summary` and longer `description` where needed; example-driven descriptions are better.
- Examples: provide at least one rich `example` per response, and small request examples for complex endpoints.
- Errors: standardize into a single `components.schemas/Error` and reference it across responses.
- Security: define `components.securitySchemes` and apply `security` selectively at operation level when needed.
- Pagination/Filtering: provide a reusable paginated envelope schema and consistent query-parameter patterns.
- Backwards compatibility: avoid breaking changes; when necessary, bump `info.version` and/or introduce versioned paths.
- Codegen: avoid `oneOf`/`anyOf` ambiguity where codegens struggle; document intended shapes clearly.
