# Specloom

Specloom is an ultra-flat, Markdown-only project with:

1. a source-of-truth generator spec
2. a production prompt to generate `AGENTS.md`
3. a maintenance prompt to evolve that production prompt over time

## How To Use

1. Open `generator-prompt.md`.
2. Paste it into your preferred AI model.
3. Provide your project context.
4. Save the output as `AGENTS.md` in your target repository.

## How To Maintain

1. Open `generator.md` to confirm source-of-truth policy.
2. Open `maintenance-prompt.md`.
3. Provide current `generator-prompt.md`, current `generator.md`, and new references/notes.
4. Use the returned updated prompt text to replace `generator-prompt.md`.
5. Run the validation checklist in `generator-prompt.md`.
6. Use Git commit history as the only change log.

## Scope

- General-purpose prompt (stack-agnostic by default).
- Designed for simplicity, portability, and low maintenance overhead.
