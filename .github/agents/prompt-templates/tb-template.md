# Testbench Generation Template

Use this template when generating testbenches for the AI-assisted Verilog lab workflow (see `docs/INSTRUCTION.md`).

## CONTEXT

The workflow provides a context file built from:

- **Required:** `docs/ARCHITECTURE.md` or `docs/ARCHITECTURE.md`
- **Optional:** `docs/PLAN.md`, `docs/INTERFACE_SPEC.md`, `docs/TESTPLAN.md` if present

Use the context file given in the prompt.

## TASK

Generate a Verilog testbench for module: **`{{module_name}}`**.

### TESTBENCH REQUIREMENTS

- Cover inputs and corner cases; use `TESTPLAN.md` test vectors if in context
- Include clock(s), reset, and stimulus generation
- Add assertions or checks for interface and timing constraints where appropriate
- Comment each major test step
- Dump waveforms (e.g. `$dumpfile` / `$dumpvars` for `.vcd`) for debugging

### DELIVERABLES

1. Testbench file: **`tb/{{module_name}}_tb.v`**
2. Optional: short description of test strategy in comments or a small Markdown note

### VALIDATION

- Testbench must compile with Icarus Verilog
- It should run with `vvp` and complete without errors
- VCD (or equivalent) should be produced for debugging

### MANDATORY JSON OUTPUT

At the **end** of your response, output exactly one JSON block:

```json
{
  "tb_files": ["tb/{{module_name}}_tb.v"],
  "simulation_passed": true,
  "coverage_percentage": 100,
  "plan_item_completed": true,
  "version": "issue_number_YYYYMMDD"
}
```

- `simulation_passed`: `true` if the testbench has been run successfully (or is ready to run)
- `coverage_percentage`: 0–100
- `version`: e.g. `"42_20250311"`
