Purpose
- Make a targeted enhancement to a single `paths` entry: descriptions, parameters, responses, examples, and links to components.

Input
- A small `paths` fragment and `goal` (e.g., "improve pagination", "add examples", "clarify errors").

Output
- A `diff` fenced YAML block with only the modified nodes. Include a 1-2 sentence rationale.

Rules
- Preserve existing operationIds. Use `$ref` for schema reuse. Keep changes minimal and reviewable.
