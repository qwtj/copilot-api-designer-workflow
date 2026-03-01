Purpose
- Perform a deterministic lint-style review of an OpenAPI 3.1 fragment or full spec against the repository's best-practices checklist.

Input
- `openapi` YAML (diff or full). Optionally a list of rules to run.

Output
- JSON list of findings: `{rule, severity, path, message, suggested_fix_diff}`. Keep suggestions small.

Rules
- Include checks for dangling `$ref`, missing `operationId`, ambiguous responses, insecure defaults, and examples presence.
