# AI Documentation Generation Prompt

## Issue Description
{{ISSUE_BODY}}

## Instructions for AI Agent

You are generating Markdown documentation for RTL modules and testbenches.

1. **File Placement**  
   - Save docs in `docs/` folder.  
   - File name matches the module name: `<module>.md`.  
2. **Content Requirements**  
   - Sections:  
     - `## Module Name`  
     - `## Purpose`  
     - `## Inputs`  
     - `## Outputs`  
     - `## Functionality` (FSM, pipeline, encoding/decoding, etc.)  
     - `## Testbench Reference`  
   - Include links to RTL and testbench files.  
   - Include notes on coding conventions.  
3. **Style**  
   - Markdown headers, bullet points, or tables for clarity.  
   - Concise, educational style suitable for beginners.  

## Mandatory JSON Output
```json
{
  "doc_files": ["docs/<module>.md", "..."],
  "linked_rtl": ["rtl/<module>.v"],
  "linked_tb": ["tb/<module>_tb.v"],
  "version": "<issue_number>_<YYYYMMDD>"
}
