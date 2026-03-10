# AI Documentation Generation Prompt

## Context
Use the following context files to generate documentation:
- `docs/ARCHITECTURE.md`
- `docs/PLAN.md`

## Instructions for AI Agent
Generate Markdown documentation for the next unimplemented item in the PLAN.md checklist.

1. Read `docs/ARCHITECTURE.md` for module purpose, I/O, and behavioral overview.
2. Identify the next unchecked documentation item in `docs/PLAN.md`.
3. Produce a Markdown file in `docs/` describing:
   - Module Name
   - Purpose
   - Inputs and Outputs
   - Functionality (FSM, pipeline, protocols)
   - Testbench linkage
   - Relevant simulation results if available

## Mandatory JSON Output
```json
{
  "doc_files": ["docs/<module>.md", "..."],
  "linked_rtl": ["rtl/<module>.v"],
  "linked_tb": ["tb/<module>_tb.v"],
  "plan_item_completed": true,
  "version": "<issue_number>_<YYYYMMDD>"
}
