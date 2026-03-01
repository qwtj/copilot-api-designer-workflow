Purpose
- Lightweight YAML helpers for merging diffs into an existing `openapi.yaml`, extracting sections, and producing minimal patches to reduce token usage.

Capabilities
- `merge_diff(base_yaml, diff_yaml)` -> returns merged YAML; prefer shallow merges at `paths` and `components`.
- `extract_section(openapi_yaml, path)` -> returns the requested subtree (e.g., `paths./pets`).
- `minimal_diff(original, updated)` -> produce a compact patch representing additions/changes.

Best practices
- Agents should prefer producing `diff` fragments limited to modified nodes rather than full files.
- Preserve ordering for readability but do not rely on order for correctness.

Example usage
```yaml
# agent provides:
diff: |
  paths:
    /pets:
      get:
        summary: List pets

# orchestrator merges with base openapi.yaml using merge_diff
```
