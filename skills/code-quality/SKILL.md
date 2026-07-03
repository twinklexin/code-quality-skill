---
name: code-quality
description: "Composite software engineering quality skill for writing code, refactoring code, code review, testing, and completion verification. Use when the user asks to implement, fix, optimize, refactor, clean up, improve code quality, review a diff/PR/branch, add tests, or verify that coding work is complete. Triggers include code quality, refactor, review, tests, TDD, bug fix, cleanup, architecture, ugly code, technical debt, 重构, 代码质量, 代码审查, 测试, 修 bug, 优化代码."
---

# Code Quality

Use this skill to keep coding work small, readable, testable, and verified. Prefer the repo's existing style and tools over new abstractions, new dependencies, or broad rewrites.

## Mode Selection

Pick the narrowest mode that satisfies the user request:

- **Implement/Fix**: add or change behavior.
- **Refactor**: improve structure while preserving behavior.
- **Review**: inspect a diff, branch, PR, or file set without editing unless asked.
- **Test**: add or improve behavior-level tests.
- **Verify**: prove that a change is complete with fresh command output.

If a task combines modes, use this order: understand -> test/protect -> implement/refactor -> review -> verify.

## Universal Workflow

1. **Read before editing**: inspect the relevant files, nearby patterns, project docs, and available commands. If `.sh` scripts exist, check whether one already provides the needed workflow.
2. **State scope**: list what will change and what will not change. Keep the scope smaller than the temptation.
3. **Plan tiny steps**: each step should leave the codebase understandable and, when possible, runnable.
4. **Use existing patterns**: naming, file layout, helpers, error handling, and test style should match the repo.
5. **Avoid speculative design**: add an abstraction only when it removes real duplication, hides meaningful complexity, or creates a clear test seam.
6. **Edit narrowly**: do not mix refactors with unrelated feature changes. Do not reformat unrelated code.
7. **Self-review the diff**: look for behavior changes, duplicated logic, weak names, oversized functions, hidden coupling, and untested critical paths.
8. **Verify freshly**: run the command that proves the claim before saying the work is done.

## Implement/Fix

- Start from the user-visible behavior or failing symptom, not from a guessed code shape.
- Prefer one vertical slice at a time: one behavior, one implementation, one verification.
- Keep names honest. If a function or variable needs a vague name like `handleData`, the design is probably unclear.
- Preserve existing contracts unless the user explicitly asked to change them.
- Treat error handling, empty states, and boundary cases as part of the implementation, not cleanup.

## Refactor

Refactoring must preserve behavior. Before moving code:

1. Identify the current public interface and expected behavior.
2. Check existing tests. If coverage is weak and the refactor is risky, add focused behavior tests first or state the test gap.
3. Split the refactor into small reversible steps.
4. Move structure without changing behavior. Behavior changes require a separate explicit step.
5. Run tests or the best available verification after meaningful steps.

Prefer deep modules: small interfaces hiding useful implementation. Avoid shallow wrappers, pass-through helpers, and "manager/service" layers that mostly delegate.

Use the deletion test: if deleting a module merely moves the same complexity into callers, the module may be useful; if deleting it removes complexity, it may be unnecessary.

## Testing

- Test through public interfaces or stable seams, not private implementation details.
- Good tests describe behavior and should survive internal refactors.
- Use known expected values, fixtures, or user-visible outcomes; avoid tautological assertions that repeat the implementation.
- Add the smallest tests that protect the risky behavior.
- If the repo has no test framework or no obvious test command, report that clearly and use build/typecheck/lint/manual verification as the fallback.

For TDD-style work:

1. Write one failing behavior test.
2. Implement only enough code to pass it.
3. Refactor only after the test is green.
4. Repeat by vertical slice.

## Review

When reviewing, lead with findings. Do not summarize first.

Check two axes:

- **Standards**: does the diff follow repo conventions and basic code-quality expectations?
- **Spec**: does the diff implement what was actually requested, without missing requirements or scope creep?

Look specifically for:

- unclear names
- duplicated logic
- speculative abstraction
- shallow wrappers or middlemen
- scattered changes for one concept
- one file changed for unrelated reasons
- primitive strings/numbers standing in for domain concepts
- tests coupled to implementation details
- success claims without verification evidence

Report issues with severity:

- **Critical**: correctness, data loss, security, broken build, or behavior regression.
- **Important**: maintainability, architecture, missing tests, incomplete requirement.
- **Minor**: naming, cleanup, small readability improvement.

Use file and line references when available. If there are no issues, say so and mention remaining test gaps or residual risk.

## Completion Gate

Before claiming completion, identify and run the proof command:

- tests for behavior claims
- build/typecheck for compilation claims
- lint/format for style claims
- targeted reproduction for bug-fix claims
- manual smoke check when no automated command exists

Read the full output and exit code. If verification fails, report the actual status and continue fixing if feasible. Do not say "done", "fixed", "passes", or equivalent without fresh evidence.

## Final Response

For implementation or refactor work, include:

- what changed
- what verification ran and the result
- any remaining risks or test gaps

For review work, include:

- findings first, ordered by severity
- open questions or assumptions
- brief summary only after findings
