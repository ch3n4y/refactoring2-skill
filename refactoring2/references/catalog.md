# Refactoring catalog

This is a compact selection index, not a substitute for reading the code and tests. Each entry states the design move and a key caution.

## First set

- **Extract Function** — name and isolate a coherent intention; make inputs and outputs explicit.
- **Inline Function** — remove a function whose body is clearer than its indirection; preserve override or interception semantics.
- **Extract Variable** — name an expression to expose purpose; watch evaluation count and order.
- **Inline Variable** — remove a name that obscures rather than explains; avoid duplicating expensive or stateful evaluation.
- **Change Function Declaration** — improve a function's name or signature; migrate callers safely.
- **Encapsulate Variable** — route access through functions so mutation and migration can be controlled.
- **Rename Variable** — align a local name with its role and scope.
- **Introduce Parameter Object** — turn a recurring argument group into a domain concept without creating a passive dumping ground.
- **Combine Functions into Class** — give shared data and closely related operations a clear owner.
- **Combine Functions into Transform** — derive an enriched result without mutating the source; keep provenance clear.
- **Split Phase** — separate work with different inputs, rules, or rates of change through an explicit intermediate value.

## Encapsulation

- **Encapsulate Record** — hide raw record representation behind an interface when invariants or evolution matter.
- **Encapsulate Collection** — prevent callers from mutating an owned collection through an exposed reference.
- **Replace Primitive with Object** — give a domain value validation and behavior; justify the extra type with real rules.
- **Replace Temp with Query** — centralize a derived calculation; avoid repeated stateful or expensive work.
- **Extract Class** — separate a coherent responsibility and move behavior with its data.
- **Inline Class** — fold a type back when its independent responsibility no longer earns the indirection.
- **Hide Delegate** — shield clients from a dependency chain; do not create a forwarding API for everything.
- **Remove Middle Man** — let clients reach the real collaborator when forwarding dominates.
- **Substitute Algorithm** — replace an implementation wholesale only after its behavior is well characterized.

## Moving features

- **Move Function** — place behavior near the data and collaborators it primarily uses.
- **Move Field** — place state with the structure that owns its lifecycle and invariants.
- **Move Statements into Function** — centralize statements that must accompany a call.
- **Move Statements to Callers** — expose caller-specific work that no longer belongs in a shared function.
- **Replace Inline Code with Function Call** — use an existing named operation instead of reimplementing it.
- **Slide Statements** — group related statements to reveal an extractable unit; preserve dependency and evaluation order.
- **Split Loop** — give distinct loop responsibilities separate passes; measure if traversal cost matters.
- **Replace Loop with Pipeline** — express a data transformation as named stages; keep side effects obvious.
- **Remove Dead Code** — delete unreachable or unused code; rely on version control rather than commented archives.

## Organizing data

- **Split Variable** — give each assignment or role its own variable; preserve intentional accumulators.
- **Rename Field** — make stored meaning explicit; treat serialization and database names as contracts.
- **Replace Derived Variable with Query** — compute derivable state from its source of truth to prevent drift.
- **Change Reference to Value** — use immutable equality-based values when identity and shared mutation are unnecessary.
- **Change Value to Reference** — use a shared identity when updates must be observed consistently; define identity lookup and lifecycle.

## Simplifying conditional logic

- **Decompose Conditional** — name the condition and branches to reveal policy.
- **Consolidate Conditional Expression** — combine checks with the same outcome when their shared meaning can be named.
- **Replace Nested Conditional with Guard Clauses** — handle exceptional or terminal cases early so the main path is visible.
- **Replace Conditional with Polymorphism** — move repeated variant logic behind type-specific behavior; avoid hierarchy for one-off branching.
- **Introduce Special Case** — represent recurring null/unknown behavior once; preserve distinctions that matter to callers.
- **Introduce Assertion** — make an internal assumption executable; do not use assertions for expected user input or recoverable errors.

## Refactoring APIs

- **Separate Query from Modifier** — prevent a value-returning operation from hiding a state change.
- **Parameterize Function** — merge near-duplicate functions when a meaningful parameter captures the variation.
- **Remove Flag Argument** — replace control-flow booleans with intention-revealing entry points; retain data booleans that are genuinely part of the domain.
- **Preserve Whole Object** — pass the source object when a callee needs several of its values; avoid increasing unwanted coupling.
- **Replace Parameter with Query** — let a callee obtain stable context itself when that reduces caller knowledge.
- **Replace Query with Parameter** — inject context to make dependencies explicit, deterministic, or testable.
- **Remove Setting Method** — make construction the only path for state that should not change later.
- **Replace Constructor with Factory Function** — hide creation details or return variants behind a named creator.
- **Replace Function with Command** — use an object when an operation needs staged state, undo, configuration, or several methods.
- **Replace Command with Function** — collapse a command object when the operation is simple and stateless.

## Dealing with inheritance

- **Pull Up Method** — centralize equivalent subclass behavior in a superclass after resolving differences.
- **Pull Up Field** — move identical state to a superclass and verify initialization semantics.
- **Pull Up Constructor Body** — share common initialization while leaving subtype-specific work explicit.
- **Push Down Method** — move behavior used only by certain subtypes out of the superclass.
- **Push Down Field** — move state that only some subtypes need to those subtypes.
- **Replace Type Code with Subclasses** — model stable type-dependent behavior with subtypes; consider delegation when type can change.
- **Remove Subclass** — replace a subtype that adds little value with a field or simpler representation.
- **Extract Superclass** — introduce a shared abstraction for genuine common behavior, not predicted reuse.
- **Collapse Hierarchy** — merge parent and child when their distinction no longer helps.
- **Replace Subclass with Delegate** — move one variation axis into composition when inheritance is too rigid or conflicts with another axis.
- **Replace Superclass with Delegate** — favor composition when a subclass should use, not be, the parent abstraction.

## Common chains

- Long function: Extract Function → Replace Temp with Query → Split Phase.
- Repeated domain primitives: Replace Primitive with Object → Move Function → Change Function Declaration.
- Type-code conditionals: Extract Function → Replace Type Code with Subclasses → Replace Conditional with Polymorphism.
- Tangled responsibilities: Move Function/Field → Extract Class; use Inline Class if the split proves artificial.
- Risky shared API change: Change Function Declaration with a compatibility wrapper → migrate callers → remove wrapper.
