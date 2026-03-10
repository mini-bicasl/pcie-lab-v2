# AI RTL Generation Prompt

## Issue Description
{{ISSUE_BODY}}

## Instructions for AI Agent

You are generating synthesizable RTL modules for a digital hardware project. Follow these rules:

1. **Naming & Style**  
   - Use clear module names reflecting functionality.  
   - 2-space indentation.  
   - Include module header comments describing purpose, inputs, outputs, and FSM states if applicable.  
2. **Specification Reference**  
   - Always reference the specification or design document provided in the issue.  
3. **Deliverables**  
   - RTL Verilog files for each module in `rtl/`.  
   - Ensure modules are **syntactically correct**.  
   - Include a minimal simulation block to verify syntax.  
4. **Documentation**  
   - Include inline comments for FSMs, states, and key logic.  

## Mandatory JSON Output
```json
{
  "rtl_files": ["rtl/<module>.v", "..."],
  "simulation_passed": true,
  "coverage_percentage": 85,
  "module_summary": "Short description of module purpose and main states",
  "version": "<issue_number>_<YYYYMMDD>"
}
