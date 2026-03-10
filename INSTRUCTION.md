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

## **Step 3: Execute Implementation Tasks**

1. For each module/task in the Implementation Plan:
   - Create a new AI task issue using the AI Task Form.
   - Select appropriate **issue type**:
     - `RTL` → CopilotRTL generates the module.
     - `Testbench` → CopilotTB generates testbench.
     - `Documentation` → CopilotDoc generates Markdown docs.
     - `Verification` → CopilotTB adds simulation/coverage tasks.
   - Fill in the **Issue Description** with references from ARCHITECTURE.md and Implementation Plan.
2. Each AI agent:
   - Generates output files in the repository (`rtl/`, `tb/`, `docs/`).
   - Produces a **JSON summary** indicating simulation results, coverage, and generated files.
3. Draft PRs are created automatically by the AI pipeline.
4. Review outputs:
   - Check RTL correctness and coding style.
   - Run simulations and verify coverage.
   - Review documentation completeness.

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
