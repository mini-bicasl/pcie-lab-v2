# AI RTL Generation Prompt

## Context
You should use the content of the following files for context:
- `docs/ARCHITECTURE.md` — design specifics, module descriptions
- `docs/PLAN.md` — checklist of items to implement

## Instructions for AI Agent
Generate synthesizable RTL modules for the next unimplemented item in the PLAN.md checklist.

1. Read and understand `docs/ARCHITECTURE.md` (functional blocks, interfaces, diagrams).
2. Locate the next unchecked RTL implementation item in `docs/PLAN.md`.
3. Generate RTL code for the specified module.
4. Place the resulting Verilog files in `rtl/`.
5. Follow project naming and style conventions.
6. Include inline comments where appropriate.
7. Do not change other parts of `docs/ARCHITECTURE.md` unless adding missing definitions.

## Mandatory JSON Output
```json
{
  "rtl_files": ["rtl/<module>.v", "..."],
  "simulation_passed": <true/false>,
  "coverage_percentage": <number>,
  "plan_item_completed": true,
  "version": "<issue_number>_<YYYYMMDD>"
}
