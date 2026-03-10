# AI Agents for Verilog Lab

This folder defines **agent configs** and **prompt templates** used by the AI-driven RTL workflow. The actual automation runs in **`.github/workflows/`**.

## Workflow

1. **Trigger:** Open an issue with the [AI Task Form](.github/ISSUE_TEMPLATE/ai_task.yml) (or add a label to an existing issue).
2. **Labels:** For RTL / Testbench / Documentation tasks, use (or get auto-added) label **`rtl requested`**, **`tb requested`**, or **`doc requested`**.
3. **Pipeline:** [ai-pipeline.yml](../workflows/ai-pipeline.yml) runs, parses the issue (module name, task type), builds context from `docs/ARCHITECTURE.md` and `docs/PLAN.md`, and runs the matching agent.
4. **Outputs:** Generated RTL, testbench, or docs are committed to a branch and a PR is opened. JSON summaries go to **`results/`**.
5. **Merge:** Add label **`ready-to-merge`** on the PR to auto-merge ([ready-to-merge.yml](../workflows/ready-to-merge.yml)).

See **`docs/INSTRUCTION.md`** for the full step-by-step workflow.

## Contents

| File | Purpose |
|------|--------|
| **rtl-generator.yml** | Agent spec for RTL generation (trigger, context, deliverables, JSON schema). |
| **tb-generator.yml** | Agent spec for testbench generation. |
| **doc-generator.yml** | Agent spec for documentation generation. |
| **prompt-templates/rtl-template.md** | Prompt template for RTL agent. |
| **prompt-templates/tb-template.md** | Prompt template for testbench agent. |
| **prompt-templates/doc-template.md** | Prompt template for documentation agent. |
| **prompt-templates/PLAN.md** | Reference for Implementation Plan structure (actual plan: `docs/PLAN.md`). |
| **prompt-templates/ARCHITECTURE.md** | Reference for architecture structure (actual doc: `docs/ARCHITECTURE.md`). |

## Context files

- **Required:** `docs/ARCHITECTURE.md` (or root `ARCHITECTURE.md`) — single source of truth for interfaces and blocks.
- **Optional:** `docs/PLAN.md`, and if present: `INTERFACE_SPEC.md`, `NAMING_CONVENTIONS.md`, `TESTPLAN.md` (under repo root or `docs/`).

The workflow builds one context file per run and passes it to the agent; templates describe the expected JSON output for traceability in **`results/`**.
