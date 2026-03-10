# AI-Assisted RTL Project Workflow Instructions

This document explains the step-by-step workflow for developing RTL projects using AI-assisted tools (Copilot or other LLM agents). The flow is organized around three phases:

- **Specification** – capture the high-level idea and architecture.
- **Planning** – break the design into modules and tasks.
- **Implementation** – generate RTL, testbenches, and documentation for each module.

Verification tasks can be added at any point to improve coverage and test quality.

---

## **Step 1: Specification – Generate Architecture Document**

Goal: turn your rough idea (e.g. “commercial server-grade DDR4 controller”) into a structured architecture.

1. Create a new issue using the **AI Task Form** (`ai_task.yml`) with:
   - **Select Issue Type**: `Specification`
   - **Module name**: `N/A`
   - **Issue Description**: describe your idea in plain language, for example:
     - “Implement a commercial server-grade DDR4 controller with ECC, refresh logic, and configurable timing parameters. Target typical server DIMMs and JEDEC DDR4 timing.”
2. The AI agent reads any existing specs in the repo and generates **`docs/ARCHITECTURE.md`** (or updates it) with:
   - Functional blocks and modules
   - Interfaces and I/O signals
   - Protocols, timing, and constraints
   - Block diagrams or FSM descriptions (ASCII or markdown)
3. Review `docs/ARCHITECTURE.md` and refine it until it is the **authoritative design reference**.

Key point: at this stage you only describe *what* you want; no module names are required yet.

---

## **Step 2: Planning – Devise Implementation Plan**

Goal: turn the architecture into a concrete implementation roadmap.

1. Create a new issue using the **AI Task Form** with:
   - **Select Issue Type**: `Planning`
   - **Module name**: `N/A`
   - **Issue Description**: e.g.
     - “Create an implementation plan for the DDR4 controller described in ARCHITECTURE.md. Break it into modules, define dependencies, and specify initial testbench and documentation requirements.”
2. The AI agent uses `docs/ARCHITECTURE.md` to generate or update **`docs/PLAN.md`**, including:
   - A list of **modules/features** (e.g. `ddr4_ctrl_top`, `phy_if`, `cmd_queue`, `refresh_fsm`, etc.).
   - **Task dependencies** between modules.
   - Initial **testbench and documentation requirements**.
   - A proposed order for **incremental implementation**.
3. `docs/PLAN.md` becomes the **master roadmap** for all subsequent Implementation and Verification issues.

---

## **Step 3: Implementation – End-to-End Module Generation**

Goal: for each module in the plan, generate RTL, a testbench, and documentation automatically.

For each module or feature, you only need to provide:

- **The module name** (must match `ARCHITECTURE.md`)
- **A short description of what you want** (your idea / behavior in plain language)

Everything else (context building, prompts, JSON, PRs) is handled by the automation.

### 3.1 Create an Implementation issue

For each module (for example `ddr4_ctrl_top`):

1. Go to **New issue → AI-Assisted Task**.
2. Fill in:
   - **Select Issue Type**: `Implementation`
   - **Module name**: the exact name from `ARCHITECTURE.md`, e.g. `ddr4_ctrl_top`.
   - **Issue Description**: describe the intended behavior for this module, e.g.:
     - “Implement `ddr4_ctrl_top` as the top-level DDR4 controller. It interfaces to the PHY, schedules commands, enforces timing constraints from TESTPLAN, and exposes a simple request/response interface to the host.”

You do **not** need to specify file paths or JSON; the workflow will handle that.

### 3.2 What the automation does for an Implementation issue

Once you submit the issue:

1. The **`ai-pipeline.yml` workflow** triggers on `issues: opened`.
2. It parses:
   - The **selected Issue Type**:
     - If it is **Implementation**, it enables all three generation jobs: RTL, Testbench, and Documentation.
     - For **Specification / Planning / Verification**, it does **not** auto-generate code/docs (those issues are for high-level work).
   - The **Module name**:
     - Required for Implementation; used for filenames and inside the prompts.
3. It builds a **context file** for the AI using:
   - `docs/ARCHITECTURE.md` (or `ARCHITECTURE.md` in repo root)
   - `docs/PLAN.md` (Implementation Plan), if present
   - Optional spec files if they exist:
     - `INTERFACE_SPEC.md`
     - `NAMING_CONVENTIONS.md`
     - `TESTPLAN.md`
     - (either in repo root or under `docs/`)
4. It calls the appropriate AI agents (`github/agents@v1`) with:
   - The constructed context
   - The relevant prompt templates from `.github/agents/prompt-templates/`
   - The target module name
5. The agents generate:
   - **RTL** in `rtl/<module_name>.v`
   - **Testbench** in `tb/<module_name>_tb.v`
   - **Documentation** in `docs/<module_name>.md`
   - A **JSON summary** (simulation status, coverage, etc.) in `results/`:
     - `results/rtl_output.json`
     - `results/tb_output.json`
     - `results/doc_output.json`
6. The workflow:
   - Commits the changes on a new `ai/...` branch (e.g. `ai/rtl-<module>-<run_id>` etc.).
   - Opens one or more **pull requests** pointing back to your issue, with instructions to label them `ready-to-merge` when you are satisfied.

You can repeat this process for each module listed in `docs/PLAN.md`.

---

## **Step 4: Verification and Auto-Merge**

Verification can be done both manually and via additional AI-assisted issues.

1. For **Implementation PRs**:
   - Review the generated RTL, testbench, docs, and JSON summaries.
   - Run additional local simulations or checks if desired.
2. When you are satisfied that a PR is correct:
   - Add the label **`ready-to-merge`** to the pull request.
3. The **same `ai-pipeline.yml` workflow** listens for `pull_request: labeled` events:
   - When it sees the label **`ready-to-merge`**, it will automatically merge the PR into the main branch.
4. If coverage or tests fail, or behavior is not as expected:
   - Create new issues (type **Verification**) to:
     - Add more tests.
     - Tighten constraints.
     - Refine RTL or documentation.
   - Repeat Step 3 for incremental improvement.

---

## **Step 5: Iterative Refinement**

You can iterate on all three phases as the design evolves:

- Update `docs/ARCHITECTURE.md` if new requirements or blocks are identified.
- Update `docs/PLAN.md` when you add modules, change priorities, or discover new dependencies.
- Add new AI issues for:
  - Missing features (Implementation).
  - Additional tests or coverage (Verification).
  - Documentation improvements (either Implementation for a module, or Planning for higher-level docs).
- Ensure all merged PRs maintain:
  - **JSON traceability** in `results/`.
  - **Simulation/coverage verification** where applicable.

---

## **Folder Structure**

After executing tasks, your repository should include:

- `rtl/` – RTL modules (`rtl/<module_name>.v`)
- `tb/` – Testbenches (`tb/<module_name>_tb.v`)
- `docs/` – Markdown documentation (per module and high-level docs)
- `results/` – Simulation logs and JSON summaries
- `.github/agents/prompt-templates/` – AI prompt templates used by the workflow
- `docs/ARCHITECTURE.md` – architecture specification
- `docs/PLAN.md` – implementation plan

---

## **Best Practices**

- Always **start with `docs/ARCHITECTURE.md`**; it is the single source of truth for modules and interfaces.
- Keep `docs/PLAN.md` up to date; it drives which Implementation issues you create.
- Use **structured AI prompts** from `.github/agents/prompt-templates/` as a reference when refining templates or agent behavior.
- Check **JSON outputs** in `results/` to ensure the AI agents met all requirements (simulation_passed, coverage, plan_item_completed).
- Review PRs manually when unsure; do not rely solely on automation for critical changes.
- For complex designs, use hierarchical issues (Epic → Specification → Planning → Implementation / Verification) to keep work organized.

---

## **Summary Workflow**

1. **Specification**: Generate / refine `docs/ARCHITECTURE.md` via Specification issues.  
2. **Planning**: Create / update `docs/PLAN.md` via Planning issues.  
3. **Implementation**: For each module, create an Implementation issue to generate RTL, Testbench, and Documentation.  
4. **Verification & Merge**: Review outputs, label PRs **`ready-to-merge`** to auto-merge.  
5. **Refine**: Iterate on specification, planning, implementation, and verification until the project is complete.
