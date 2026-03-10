# Documentation Template

## CONTEXT
Provide references:
- Architecture: `ARCHITECTURE.md`
- Interface spec: `INTERFACE_SPEC.md`
- Naming conventions: `NAMING_CONVENTIONS.md`
- Testplan: `TESTPLAN.md`
- Related RTL and TB files

## TASK
Write detailed Markdown documentation for `{{module_name}}`.

### DOCUMENTATION REQUIREMENTS
- Architecture overview with block diagrams
- Module interfaces (ports, widths, directions)
- State machine diagrams (ASCII or Mermaid)
- Timing diagrams if applicable
- Link to relevant RTL and testbench files
- Explain rationale for design choices and constraints
- Include code comment summaries if needed

### DELIVERABLES
- Markdown file (`.md`) in `/docs/`
- Structured format suitable for GitHub with diagrams, tables, and references

### MANDATORY JSON OUTPUT
Return a JSON summary after documentation generation:
```json
{
  "rtl_files": ["rtl/{{module_name}}.v"],
  "simulation_passed": true,
  "coverage_percentage": 100,
  "plan_item_completed": true,
  "version": "{{issue_number}}_{{YYYYMMDD}}"
}
