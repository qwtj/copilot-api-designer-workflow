Purpose
- Add or refine `securitySchemes` and per-operation `security` requirements for the API.

Input
- Current `components.securitySchemes` fragment (if any), desired auth types (e.g., OAuth2, bearer, API Key), and high-level rules (scopes, required flows).

Output
- `diff` fenced YAML that adds `components.securitySchemes` and updates `security` at root or operation level. Include recommended scope lists and example tokens.

Rules
- Use `bearer` for JWT-like tokens, `http` with `bearer` scheme and `bearerFormat: JWT`.
- For OAuth2 provide `flows` and minimum scopes, and show example `security` usage for an endpoint.
