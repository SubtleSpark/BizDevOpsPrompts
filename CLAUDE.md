# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this prompt generation repository.

## Project Purpose

This repository is designed for generating high-quality prompts using collected templates and patterns. It contains:

1. **Prompt Templates** - Examples collected from https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools
2. **Generated Prompts** - Custom prompts created based on learned patterns and techniques

## Repository Structure

- `templates/system-prompts-and-models-of-ai-tools/` - Contains collected prompt templates from various AI tools
- `generated/` - Contains generated prompts organized by scenarios (e.g., code-assistant, data-analysis)
  - Each scenario contains a README.md with usage guide and relevant prompt files tailored to that specific use case
- `patterns/` - Analysis of common prompt patterns and techniques
  - `prompt_analysis.md` - 10 core prompt patterns identified from template analysis
  - `generation_template.md` - Reusable framework for generating new prompts

## Workflow

1. Study prompt templates to understand effective patterns and techniques
2. Identify key elements: structure, tone, specificity, constraints, examples
3. Apply learned patterns when generating new prompts for specific requirements
4. Iterate and refine based on effectiveness

## Key Prompt Patterns to Learn

- Clear role definition and context setting
- Specific instructions with examples
- Output format specifications
- Constraint definitions
- Step-by-step reasoning approaches
- Few-shot learning examples

## Technical Notes

### XML Tag Conflicts
When creating prompts that include tool usage examples with XML tags (like `<function_calls>`, `<invoke>`, `<parameter>`), these will conflict with Claude Code's internal parsing system. 

**Solution**: Add `user_` prefix to example tags to avoid conflicts:
- `<function_calls>` → `<user_function_calls>`
- `<invoke>` → `<user_invoke>`
- `<parameter>` → `<user_parameter>`
- `<function_results>` → `<user_function_results>`

This ensures the examples are treated as documentation rather than actual tool calls.