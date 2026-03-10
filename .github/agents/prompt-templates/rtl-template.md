# AI RTL Generation Prompt
Issue Description:
{{ISSUE_BODY}}

Instructions:
- Generate synthesizable Verilog module(s) according to the provided PCIe spec section.
- Follow company-style coding guide (2-space indentation, meaningful module header comments).
- Include inline comments for FSM/state explanation.
- Save output files under rtl/ with the module name.
- Include simulation-ready testbench skeleton placeholder if possible.
- Output a JSON summary with:
  "rtl_files": [...],
  "simulation_passed": true/false
