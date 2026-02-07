# Specloom Generator Spec

This file is the source-of-truth policy for:

1. `generator-prompt.md` (runtime generation prompt)
2. `maintenance-prompt.md` (maintenance/update prompt)

## Scope

Specloom exists to generate high-quality `AGENTS.md` files for arbitrary repositories with strong safety, low ambiguity, and high execution reliability.

## Two-Track Model

All changes must keep these tracks distinct:

1. **AGENTS Content Track**
   - Defines what a generated `AGENTS.md` should contain.
   - Focuses on repository-operational instructions.
2. **Prompt Design Track**
   - Defines how prompts should be written to produce consistent `AGENTS.md` output.
   - Focuses on instruction structure, clarity, and reliability.

## AGENTS Content Policy

Generated `AGENTS.md` should follow these rules:

1. Keep root instructions concise and broadly applicable.
2. Include concrete commands for setup, checks, tests, and validation.
3. Use progressive disclosure:
   - Root file contains high-frequency universal rules.
   - Domain-specific detail belongs in linked docs or scoped agent files.
4. Include an explicit repository map for navigation.
5. Include verification gates and measurable completion criteria.
6. Include explicit guardrails and forbidden actions.
7. Include doc-update triggers when architecture/API/process changes should update docs.
8. Include release/versioning rules when relevant (for example changesets/conventional commits).
9. Avoid speculative or stale filesystem facts.
10. Prefer deterministic enforcement (tooling/commands) over prose-only style mandates.

## Prompt Design Policy

Prompts in this repo should follow:

1. High-priority constraints appear before long context.
2. Required output schema is explicit and deterministic.
3. Language is imperative, concise, and measurable.
4. Negative constraints include positive alternatives.
5. Uncertainty handling is explicit (`Assumptions` instead of guessing).
6. Validation gates are mandatory before final output.
7. Instruction budget is managed to avoid prompt bloat and redundancy.
8. Structure remains stable across revisions.

## Root Instruction Budget Policy

1. Root generated `AGENTS.md` should remain compact.
2. Default target: under ~200 lines unless justified by repository complexity.
3. Add instructions only when they materially improve task success/safety.
4. Remove redundant, low-signal, or contradictory rules during maintenance.

## Required Generated AGENTS Sections

Minimum required sections:

1. Purpose
2. Quick Start Commands
3. Repository Map
4. Development Workflow
5. Verification and Testing Gates
6. Security and Data Rules
7. Git, PR, and Release Rules
8. Safety and Guardrails
9. Progressive Disclosure Pointers
10. Task Execution Protocol
11. Definition of Done
12. Assumptions (only when needed)

## Mandatory Safety Rules

Generated `AGENTS.md` must always prohibit:

1. Destructive git/file operations without explicit user request.
2. Exposure or logging of secrets or credentials.
3. Presenting unverified repository facts as truth.

Generated `AGENTS.md` must always require:

1. Running relevant validation checks before completion.
2. Declaring uncertainty explicitly.
3. Following provided legal/compliance constraints.

## Maintenance Contract

When updating prompts:

1. `generator-prompt.md` must implement this spec directly.
2. `maintenance-prompt.md` must enforce this spec in its quality gate.
3. Changes should map to references with clear rationale.
4. Keep stack-agnostic defaults unless user scope explicitly narrows.

## Acceptance Criteria

A change is acceptable only if:

1. Two-track separation is preserved.
2. Safety guardrails remain explicit and strong.
3. Validation criteria remain measurable.
4. Progressive disclosure and instruction-budget discipline are preserved.
5. No contradictory rules are introduced.

## Source References

AGENTS guidance:

1. [https://raw.githubusercontent.com/openai/codex/refs/heads/main/AGENTS.md](https://raw.githubusercontent.com/openai/codex/refs/heads/main/AGENTS.md)
2. [https://raw.githubusercontent.com/vercel/vercel/refs/heads/main/AGENTS.md](https://raw.githubusercontent.com/vercel/vercel/refs/heads/main/AGENTS.md)
3. [https://raw.githubusercontent.com/vercel/next.js/refs/heads/canary/AGENTS.md](https://raw.githubusercontent.com/vercel/next.js/refs/heads/canary/AGENTS.md)
4. [https://raw.githubusercontent.com/vercel/turborepo/refs/heads/main/AGENTS.md](https://raw.githubusercontent.com/vercel/turborepo/refs/heads/main/AGENTS.md)
5. [https://www.aihero.dev/a-complete-guide-to-agents-md](https://www.aihero.dev/a-complete-guide-to-agents-md)
6. [https://www.humanlayer.dev/blog/writing-a-good-claude-md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
7. [https://developers.openai.com/codex/guides/agents-md/](https://developers.openai.com/codex/guides/agents-md/)

Prompt guidance:

1. [https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api)
2. [https://platform.openai.com/docs/guides/prompt-engineering](https://platform.openai.com/docs/guides/prompt-engineering)
3. [https://platform.openai.com/docs/guides/prompt-optimizer](https://platform.openai.com/docs/guides/prompt-optimizer)
4. [https://cookbook.openai.com/examples/gpt-5/gpt-5-2_prompting_guide](https://cookbook.openai.com/examples/gpt-5/gpt-5-2_prompting_guide)
5. [https://cookbook.openai.com/examples/gpt-5/codex_prompting_guide](https://cookbook.openai.com/examples/gpt-5/codex_prompting_guide)
6. [https://cookbook.openai.com/examples/evaluation/building_resilient_prompts_using_an_evaluation_flywheel](https://cookbook.openai.com/examples/evaluation/building_resilient_prompts_using_an_evaluation_flywheel)
7. [https://developers.openai.com/codex/prompting](https://developers.openapi.com/codex/prompting)
