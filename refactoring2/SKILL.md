---
name: refactoring2
description: Review and refactor existing code through behavior-preserving, test-backed micro-steps. Use when identifying code smells, planning a safe refactor, improving structure without changing observable behavior, or selecting a named refactoring technique. Do not use for feature work or behavior changes unless those changes are explicitly separated from the refactor.
---

# Refactoring 2

Improve the design of existing code while preserving its externally observable behavior. Optimize for easier understanding and cheaper future change, not for a particular style or maximum abstraction.

## Route the task

- For diagnosis or review only, inspect and report; do not edit code.
- For a refactoring plan, identify the concrete smell, desired design pressure, safety checks, and the smallest ordered transformations.
- For implementation, follow the micro-step loop below and verify every meaningful step.
- For a named technique, consult [references/catalog.md](references/catalog.md).
- When the right technique is unclear, consult [references/code-smells.md](references/code-smells.md).
- For legacy code, databases, performance-sensitive code, shared APIs, or weak tests, read [references/operating-guide.md](references/operating-guide.md).

## Establish the safety boundary

1. Read the local repository instructions and inspect the relevant code, callers, tests, and current diff.
2. State the behavior that must remain unchanged. Include outputs, errors, side effects, ordering, timing-sensitive contracts, persistence, and public API compatibility when relevant.
3. Find the narrowest useful validation command. Prefer existing tests; add characterization tests only when implementation is authorized and behavior is otherwise unprotected.
4. Keep refactoring separate from feature changes, bug fixes, dependency upgrades, and broad formatting. If both are requested, make the behavioral change explicit and validate it independently.

Do not infer desired behavior from an attractive design. When tests disagree with prose, surface the conflict instead of silently choosing one.

## Choose the next change

Name the observed problem in concrete terms: what is hard to understand or change, where duplication or coupling occurs, and what future modification it obstructs. Treat smell names as clues, not verdicts.

Prefer the smallest transformation that improves the current change path. Avoid speculative frameworks, premature inheritance, and abstractions with only hypothetical clients. Preserve useful domain language even when simplifying structure.

## Use a micro-step loop

Repeat:

1. Make one coherent structural change.
2. Run the narrowest relevant automated check.
3. Inspect the diff for accidental behavior, API, data-shape, exception, or evaluation-order changes.
4. Keep the step if the code is clearer and checks pass; otherwise revise or revert only that step.

Use IDE/compiler-supported rename and move operations when available. Keep the code runnable between steps. Broaden the test suite after local checks pass.

If a refactoring exposes a bug, first restore the previous behavior, then handle the fix as a separately authorized change. If preserving behavior is impossible or unverifiable, stop and explain the exact uncertainty.

## Finish with evidence

Report:

- the smell or change pressure addressed;
- the transformations applied, using named techniques where helpful;
- the behavior-preservation evidence and commands run;
- remaining risks, intentionally deferred cleanup, and any public API or migration concern.

Do not claim “no behavior change” without test, static-analysis, or tightly reasoned evidence.

## Source basis

This skill is an original operational distillation of Martin Fowler's *Refactoring, Second Edition*. It does not reproduce the book's examples or chapter prose. For chapter-to-reference provenance, see [references/source-map.md](references/source-map.md).
