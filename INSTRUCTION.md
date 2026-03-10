# AI-Assisted RTL Project Workflow Instructions

This document explains the step-by-step workflow for developing RTL projects using AI-assisted tools (Copilot or other LLM agents). Follow these steps to execute a design from specification to verified implementation.

---

## **Step 1: Generate Architecture Document**

1. Create a new issue using the **AI Task Form** (`ai_task.yml`) with type: **Setup**.
2. Instruct the AI agent to **search for all relevant specifications and references** for your design.
3. The AI generates **ARCHITECTURE.md**, which should include:
   - Functional blocks and modules
   - Interfaces and I/O signals
   - Protocols, timing, and constraints
   - Block diagrams or FSM descriptions (ASCII or markdown)
4. Review ARCHITECTURE.md and approve it as the authoritative design reference.

---

## **Step 2: Devise Implementation Plan**

1. Create a new issue (type: **Setup** or **Documentation**) for the **Implementation Plan**.
2. Based on ARCHITECTURE.md, instruct AI to:
   - Break the design into **modules/features**.
   - Specify **task dependencies**.
   - Define initial **testbench and documentation requirements**.
   - Order tasks logically for incremental implementation.
3. The Implementation Plan becomes the **master roadmap** for your issue list.

---

## **Step 3: Executing Implementation Tasks – Markdown Template for Users**

1. For each module/task, create a new issue using this Markdown template in the AI Task Form (ai_task.yml). Copy-paste this into the Issue Description field:
```
# Task: <Module Name or Feature>

## Reference
- See ARCHITECTURE.md section: <section name or block diagram reference>
- Implementation Plan task: <task ID or description>

## Requirements
- RTL module name: <module_name>
- Inputs / Outputs: <list of signals>
- Functionality description: <brief behavior>
- Constraints: <timing, protocols, coding style, FSM rules>

## Deliverables
1. RTL file in `rtl/<module_name>.v` (CopilotRTL)
2. Testbench file in `tb/<module_name>_tb.v` (CopilotTB)
3. Documentation in `docs/<module_name>.md` (CopilotDoc)
4. JSON summary of files, simulation pass/fail, coverage

## Notes / Additional Instructions
- Include inline comments in RTL for FSM states or key logic
- Include test cases and expected outputs in testbench
- Use Markdown documentation template for docs
```

2. How to use this template:
- Copy this into the Issue Description field of the AI Task Form.
- Select issue type in the dropdown (RTL, Testbench, Documentation, Verification).
- Assign priority if needed.
- The AI pipeline workflow will assign the correct agent, generate draft PRs, and populate rtl/, tb/, and docs/.

---

## **Step 4: Verification and Auto-Merge**

1. When the outputs pass verification:
   - Add the label **ready-to-merge** to the PR.
2. The AI pipeline workflow will automatically merge the PR to the main branch.
3. If coverage or tests fail:
   - Create new issues for gaps or bug fixes.
   - Repeat Step 3 for incremental improvement.

---

## **Step 5: Iterative Refinement**

- Update ARCHITECTURE.md or Implementation Plan if new requirements are identified.
- Add new AI tasks for missing features, test cases, or documentation.
- Ensure all merged PRs maintain **JSON traceability** and simulation/coverage verification.

---

## **Folder Structure**

After executing tasks, your repository should include:
- /rtl/ # RTL modules
- /tb/ # Testbenches
- /docs/ # Markdown documentation
- /results/ # Simulation logs and coverage
- .github/agents/prompt-templates/ # AI templates
- ARCHITECTURE.md

---

## **Best Practices**

- Always **start with ARCHITECTURE.md**; it is the single source of truth.
- Use **structured AI prompts** from `.github/agents/prompt-templates/`.
- Check **JSON outputs** to ensure the AI agent met all requirements.
- Review PRs manually if unsure; do not merge unverified outputs.
- Use hierarchical issues (Epic → Feature → Micro/Verification) for complex designs.

---

## **Summary Workflow**

1. Generate **ARCHITECTURE.md**  
2. Create **Implementation Plan**  
3. Execute module/testbench/documentation tasks via AI issues  
4. Verify outputs → label **ready-to-merge** → auto-merge  
5. Iteratively refine until project is complete
