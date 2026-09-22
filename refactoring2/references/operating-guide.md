# Operating guide

Read this guide when the ordinary test-backed micro-step loop needs extra safeguards.

## Weak or missing tests

Capture current behavior before changing structure. Favor focused characterization tests around the seam being edited: representative happy paths, boundaries, errors, and observable side effects. Do not freeze incidental implementation details unless callers depend on them.

If the code cannot be tested cheaply, first create a seam with a behavior-preserving extraction, dependency parameter, or wrapper. Keep that change narrow. A rewrite is not a substitute for understanding behavior.

## Public or shared APIs

Search all in-repository callers and identify external consumers. Use a compatibility wrapper, staged migration, or deprecation period when callers cannot change atomically. Treat serialized shapes, error types, event names, and call ordering as API surface even when the language does not enforce them.

## Databases and persisted data

Separate code refactoring from schema migration. Prefer expand-and-contract changes:

1. add a compatible representation;
2. support old and new reads/writes;
3. migrate and verify data;
4. remove the old path only after consumers have moved.

Make rollback and mixed-version operation explicit. Never assume an in-memory rename is equivalent to renaming persisted data.

## Performance-sensitive code

Preserve semantics first. Record a representative baseline before structural changes, then measure again. Optimize only demonstrated hot paths. Keep performance tuning separate from structural refactoring when possible so regressions can be attributed.

## Concurrency and asynchronous behavior

Extraction and movement can change evaluation order, lock scope, scheduling, retries, or cancellation. Record these as behavior. Test ordering and failure paths, not only returned values.

## Long-running refactors

Avoid a long-lived “cleanup” branch. Find intermediate designs that can be integrated safely. Use adapters and parallel paths when a subsystem cannot move atomically. Each merge should leave the system deployable and make the next step easier.

## When not to refactor

Do not refactor merely because code looks unfamiliar or unfashionable. Pause when:

- the code will be deleted soon and no current change depends on it;
- behavior cannot be established and the risk exceeds the value;
- a clean rewrite is demonstrably cheaper and the existing behavior need not be preserved;
- the requested outcome is actually a feature or bug fix and has not been authorized as such.

## Review checklist

- Is the before/after behavior boundary explicit?
- Does each new name reveal domain intent?
- Did duplication actually disappear, or merely move?
- Is data owned by the code that uses it most?
- Are dependencies clearer and less surprising?
- Are public contracts and persistence compatible?
- Did test quality improve or stay intact?
- Is the result simpler for the next likely change?
