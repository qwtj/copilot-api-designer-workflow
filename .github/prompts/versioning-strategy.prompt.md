Purpose
- Recommend a versioning strategy and update `info.version` and server URL patterns to align with semantic versioning or date-based versioning.

Input
- Current `info.version` (if any), expectations for breaking vs non-breaking changes, and client compatibility constraints.

Output
- Short markdown recommendation and a `diff` YAML snippet that updates `info.version` and example server URL(s).

Rules
- Prefer semantic versioning in `info.version`. If versioned endpoints are required, recommend `/{version}` path prefix or hostname strategy and include example redirects.
