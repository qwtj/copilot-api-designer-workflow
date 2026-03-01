OpenAPI Handoff - Patient & MedicalRecord API

Files:
- OpenAPI spec: ./tmp/openapi.yaml

Summary:
- Purpose: Minimal PHI-sensitive API to manage `Patient` and `MedicalRecord` resources.
- Security: OAuth2 (authorizationCode + clientCredentials) and `bearerAuth` (JWT). Scopes used: "patient:read", "patient:write", "record:read", "record:write", "consent:manage".
- Consent: Access to detailed PHI (`MedicalRecord.details`, `Patient.birthDate`) requires explicit patient consent; endpoints note consent-required behavior.
- Data minimization: List endpoints return minimal patient fields by default.

Implementation notes:
- The spec enforces UUID patterns for identifiers and includes an `Error` schema used by `Unauthorized`/`Forbidden` responses.
- Some non-blocking documentation suggestions remain: add `description` for path parameters and a few schema properties; consider moving repeated parameters into `components.parameters` for reuse.
- Deletion endpoints are modeled as soft-delete semantics; 204 responses intentionally have no body.

Next steps (optional):
- Run `openapi-cli validate ./tmp/openapi.yaml` or `swagger-cli validate` to verify locally.
- Consider adding examples for error responses and consolidating OAuth2 scope docs in `info.description`.
