# Specloom Generator Prompt

## Mission

Generate a production-grade `AGENTS.md` for any repository.

This prompt must produce output that is:

1. Operationally useful for coding agents.
2. Safe and non-speculative.
3. Portable across repositories and machines.

## Inputs Required

If missing, request focused follow-up input before final output:

1. Project purpose and primary stack.
2. Repository layout and key directories/files.
3. Build, test, lint, typecheck, and format commands.
4. Security, secrets, and data-handling constraints.
5. Git/PR/release workflow rules.
6. Explicit forbidden actions.
7. Definition of done for code changes.
8. Optional: monorepo sub-areas needing scoped instructions.

If critical commands, paths, or policies are unknown, ask instead of guessing.

## Generation Workflow

1. Discover facts first from provided context.
2. Keep root instructions concise and broadly applicable.
3. Use progressive disclosure: root rules first, then links to deeper docs when needed.
4. Prefer deterministic enforcement via tooling/commands over vague prose.
5. Include only high-signal instructions that affect execution quality or safety.

## Output Contract

1. Return exactly one complete Markdown file intended as `AGENTS.md`.
2. Return only file content with no preface and no code fences around the entire file.
3. Use repo-relative paths only (for example `app/routes/api.ts`), never machine-specific absolute paths.
4. Use concrete command examples and format command groups in fenced `bash` blocks.
5. Do not state unverified repo governance/policy/runtime facts as mandatory rules.
6. If a policy is uncertain, place it in `Assumptions` with `[Inferred]`.
7. Distinguish required vs recommended guidance without repeating bulky `Mandatory:`/`Recommended:` subheadings in every section.
8. Keep wording imperative, concise, and execution-ready.
9. If any heading/order/portability/validation rule is violated, regenerate before returning final output.
10. Mark deployment and infrastructure-changing commands as explicit-request-only.
11. Do not present formatting commands as mandatory verification gates unless a non-mutating format-check command is explicitly provided.
12. Keep verification requirements consistent across `Quick Start Commands`, `Verification and Testing Gates`, and `Definition of Done`.

## Markdown Format Rules (Strict)

1. Use exactly one H1 at the top: `# AGENTS.md`.
2. Every required section must be an H2 heading (`## Section Name`).
3. Do not use H1 for section headings.
4. Use H3 only when truly needed for short subsection grouping; avoid deep nesting.
5. Keep section order exactly as defined in this prompt.
6. Prefer flat lists and short paragraphs for scanability.
7. Add language info strings to fenced code blocks (for example `bash`, `text`, `md`).

## Required Sections In Generated AGENTS.md (Exact H2 Order)

- `## Purpose`
- `## Quick Start Commands`
- `## Repository Map`
- `## Development Workflow`
- `## Verification and Testing Gates`
- `## Security and Data Rules`
- `## Git, PR, and Release Rules`
- `## Safety and Guardrails`
- `## Progressive Disclosure Pointers`
- `## Task Execution Protocol`
- `## Definition of Done`
- `## Assumptions` (only when needed; max 3 high-impact items)

## Section Writing Style Rules

1. Do not repeat `Mandatory:` and `Recommended:` subheadings under every section.
2. Prefer one flat bullet list per section with concise, action-first rules.
3. If distinction is necessary, use inline text labels `Required:` and `Recommended:` within bullets.
4. Never use bracketed pseudo-labels like `[Required]` or `[Recommended]` because strict Markdown linters interpret them as reference links.
5. Keep most sections to 3-8 bullets unless command/reference-heavy.
6. Avoid prose-heavy policy dumps in root `AGENTS.md`.

## AGENTS.md Quality Rules

1. Root guidance should be compact (default target under ~200 lines unless complexity requires more).
2. Include only verified paths, commands, and workflows.
3. For monorepos, clarify path-based scope and package-specific command patterns.
4. Include documentation-update triggers when architecture/API/workflow changes.
5. Prefer stable guidance over brittle file-path memorization.
6. Include anti-pattern warnings only when verified and high-frequency.
7. Avoid contradictory, duplicated, or low-value instructions.
8. If writing/tone rules are relevant, keep root guidance short and link deeper writing docs in Progressive Disclosure.
9. Do not embed long external style guides directly in root `AGENTS.md`.
10. Prefer concise command-first guidance; include a clear package-manager rule when known.
11. Include high-signal "Do Not" constraints in Safety and Guardrails for risky operations.
12. Treat formatting/fixing commands as remediation steps; verification gates should be non-mutating where possible.
13. Avoid unconditional build/test requirements unless explicitly required by repository policy; default to scope-aware gating.

## Safety and Non-Negotiables

Generated `AGENTS.md` must require:

1. No destructive git/file operations without explicit request.
2. No exposure or logging of secrets/credentials/tokens.
3. Running relevant validation checks before completion.
4. Explicit uncertainty handling instead of fabrication.
5. Respect for provided legal/compliance constraints.
6. No deploy/infrastructure-changing command execution unless explicitly requested.
7. Generated or vendored artifacts must not be edited casually; only allow edits through documented maintenance/regeneration workflows when explicitly relevant.

## Definition of Done Rule

When defining completion criteria:

1. Require checks relevant to the changed scope.
2. Do not force full-suite validation for every task when scope does not justify it.
3. Require clear reporting of which checks were run, skipped, or failed.
4. Ensure completion criteria do not conflict with the `Verification and Testing Gates` section.

## Verification Command Rules

1. Mandatory verification gates should be non-mutating checks where available (for example lint/type/test/build checks).
2. Format or autofix commands are remediation steps, not pass/fail verification gates, unless an explicit check-only format command exists.
3. If only mutating format commands are available, list them outside mandatory gates and label them as optional remediation.
4. Build checks should be scope-gated by default (for example runtime/config/packaging changes), unless repository policy explicitly mandates build on every change.
5. Require reporting in `run/skipped/failed` format for all listed verification gates.

## Assumptions Rules

1. Include `Assumptions` only when unresolved uncertainty materially impacts execution.
2. Maximum 3 assumptions, each concise and high-impact.
3. Every assumption must include:
   - `[Inferred]` prefix
   - why it is uncertain
   - potential impact if wrong
4. Do not add low-value assumptions (for example generic commit-style speculation) unless directly relevant to task execution.
5. Do not include assumptions about commit message style unless enforcement exists in repository policy files.
6. If inferred claims are used anywhere in the document, `## Assumptions` must be present.
7. If the document uses uncertain language (for example "prefer", "likely", "assume", "not documented"), include `## Assumptions` or remove the uncertain claim.

## Validation Checklist

Before returning final output, verify:

- [ ] All required sections are present.
- [ ] Exactly one H1 exists, and it is `# AGENTS.md`.
- [ ] Required sections are H2 headings in the exact order.
- [ ] Commands are concrete and in runnable `bash` blocks where grouped.
- [ ] Deploy/infra-changing commands are explicitly marked request-only.
- [ ] Paths are repo-relative and portable.
- [ ] Unverified policy claims are not presented as facts.
- [ ] Commit-message conventions are only stated when enforcement is verified from repository policy.
- [ ] Quick Start commands do not contradict Verification and Definition of Done requirements.
- [ ] Section formatting avoids repetitive `Mandatory:`/`Recommended:` heading bloat.
- [ ] No bracketed pseudo-labels are used (for example `[Required]`, `[Recommended]`).
- [ ] Forbidden actions and safety guardrails are explicit.
- [ ] Verification gates are measurable and scope-aware.
- [ ] Verification section distinguishes non-mutating gates from optional mutating remediation commands.
- [ ] Verification reporting explicitly requires `run/skipped/failed`.
- [ ] Generated/vendored artifact rules allow documented maintenance workflows when explicitly needed.
- [ ] Instructions are concise, non-redundant, and contradiction-free.
- [ ] `Assumptions` exists only if needed, uses `[Inferred]`, and contains only high-impact items.
- [ ] If any uncertain/inferred claim exists, `## Assumptions` is present.
- [ ] Any fenced code block includes a language info string.
- [ ] Output is directly usable as `AGENTS.md`.
