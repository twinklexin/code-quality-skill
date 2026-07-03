# Code Quality Skill

A compact agent skill for disciplined software engineering work: implementation, refactoring, code review, testing, and completion verification.

## What It Does

`code-quality` guides an AI coding agent to:

- read existing code before editing
- keep implementation scope small
- follow the repository's existing style and tools
- refactor while preserving behavior
- write behavior-focused tests
- review diffs for correctness and maintainability
- verify work before claiming completion

It is intentionally small. Most of the value is in the workflow discipline, not in bundled scripts or heavy framework assumptions.

## Install

Install with the open agent skills CLI:

```bash
npx skills add twinklexin/code-quality-skill --skill code-quality
```

To install into a specific agent:

```bash
npx skills add twinklexin/code-quality-skill --skill code-quality -a codex
npx skills add twinklexin/code-quality-skill --skill code-quality -a claude-code
```

## Use

Ask your agent to use the skill explicitly:

```text
Use $code-quality to refactor this module while preserving behavior and adding focused tests.
```

```text
Use $code-quality to review this branch for correctness, maintainability, and missing tests.
```

```text
Use $code-quality to implement this bug fix, then run the relevant verification command before claiming it is complete.
```

## Repository Layout

```text
skills/
  code-quality/
    SKILL.md
    agents/
      openai.yaml
```

## Acknowledgments

This skill is inspired by common software engineering practices around small-step implementation, refactoring, code review, behavior-level testing, and verification gates, as well as the broader open agent skills ecosystem.

No upstream skill text is copied verbatim.

## License

MIT License. See [LICENSE](./LICENSE).
