# RTL Generation Template

## CONTEXT
Provide all relevant files:
- Architecture: `ARCHITECTURE.md`
- Interface spec: `INTERFACE_SPEC.md`
- Naming conventions: `NAMING_CONVENTIONS.md`
- Test vectors: `TESTPLAN.md`

## TASK
Generate synthesizable Verilog RTL for the requested module: `{{module_name}}`.

### MODULE REQUIREMENTS
- Follow all interface specs from INTERFACE_SPEC.md
- Include synchronous reset and proper clock domains
- Comment each FSM state and combinational logic
- Follow naming conventions in NAMING_CONVENTIONS.md
- Use structured module hierarchy consistent with ARCHITECTURE.md

### DELIVERABLES
1. RTL file(s) (`*.v`) in `/rtl/`
2. Optional Markdown comment header explaining the module

### VALIDATION
- Must compile cleanly with Icarus Verilog
- Must pass all test vectors in TESTPLAN.md
- Lint clean with Verilator

### MANDATORY JSON OUTPUT
After generating RTL, return exactly this JSON (replace placeholders appropriately):
```json
{
  "rtl_files": ["rtl/{{module_name}}.v"],
  "simulation_passed": true,
  "coverage_percentage": 100,
  "plan_item_completed": true,
  "version": "{{issue_number}}_{{YYYYMMDD}}"
}
