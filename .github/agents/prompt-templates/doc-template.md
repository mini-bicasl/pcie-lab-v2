# Documentation Template

Use this template when generating module documentation for the AI-assisted Verilog lab workflow (see `docs/INSTRUCTION.md`).

## CONTEXT

The workflow provides a context file built from:

- **Required:** `docs/ARCHITECTURE.md` or `docs/ARCHITECTURE.md`
- **Optional:** `docs/PLAN.md`, `docs/INTERFACE_SPEC.md`, `docs/NAMING_CONVENTIONS.md` if present

Use the context file and any referenced RTL/testbench paths.

## TASK

Write Markdown documentation for module: **`{{module_name}}`**.

### DOCUMENTATION REQUIREMENTS

- Short overview and role of the module in the architecture
- Module interface: ports, widths, directions, and purpose
- State machine or control flow (ASCII or Mermaid diagram if useful)
- Timing or protocol notes if applicable
- References to RTL (`rtl/{{module_name}}.v`) and testbench (`tb/{{module_name}}_tb.v`)
- Brief rationale for main design choices and constraints
- Code-comment summaries only where they add clarity

### DELIVERABLES

1. Documentation file: **`docs/{{module_name}}.md`**
2. Use headings, tables, and diagrams so it renders well on GitHub

### MANDATORY JSON OUTPUT

At the **end** of your response, output exactly one JSON block:

```json
{
  "doc_files": ["docs/{{module_name}}.md"],
  "plan_item_completed": true,
  "version": "issue_number_YYYYMMDD"
}
```

- `plan_item_completed`: `true` when the documentation satisfies the Implementation Plan item for this module
- `version`: e.g. `"42_20250311"`
