# RTL Generation Template

Use this template when generating RTL for the AI-assisted Verilog lab workflow (see `docs/INSTRUCTION.md`).

## CONTEXT

The workflow provides a context file built from (in order):

- **Required:** `docs/ARCHITECTURE.md` or `ARCHITECTURE.md` (architecture and interfaces)
- **Optional:** `docs/PLAN.md` (Implementation Plan)
- **Optional (if present):** `docs/INTERFACE_SPEC.md`, `docs/NAMING_CONVENTIONS.md`, `docs/TESTPLAN.md` 

Use the context file given in the prompt as the single source of truth.

## TASK

Generate synthesizable Verilog RTL for the requested module: **`{{module_name}}`**.

### MODULE REQUIREMENTS

- Follow interfaces and block descriptions from the architecture document
- Include synchronous reset and proper clock domains
- Comment each FSM state and key combinational logic
- Use naming consistent with the architecture; if `NAMING_CONVENTIONS.md` is in context, follow it
- Keep module hierarchy consistent with the architecture

### DELIVERABLES

1. RTL file: **`rtl/{{module_name}}.v`**
2. Optional: short Markdown comment header at the top of the file describing the module

### VALIDATION

- Code must compile with Icarus Verilog (`iverilog`)
- Design should be verifiable against test vectors if `TESTPLAN.md` is in context
- Prefer Verilator-clean style where practical

### MANDATORY JSON OUTPUT

At the **end** of your response, output exactly one JSON block (replace placeholders with real values):

```json
{
  "rtl_files": ["rtl/{{module_name}}.v"],
  "simulation_passed": true,
  "coverage_percentage": 100,
  "plan_item_completed": true,
  "version": "issue_number_YYYYMMDD"
}
```

- `simulation_passed`: set to `true` when RTL is ready for simulation; `false` if not yet run
- `coverage_percentage`: 0–100
- `version`: e.g. `"42_20250311"` (issue number and date)
