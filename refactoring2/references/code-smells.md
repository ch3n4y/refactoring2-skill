# Code-smell decision guide

Use smells as search heuristics. Confirm the concrete cost before editing, then choose the smallest relevant technique from the catalog.

| Smell | Look for | Usually consider |
|---|---|---|
| Mysterious name | A reader must inspect implementation to learn meaning | Rename Variable, Rename Field, Change Function Declaration |
| Duplicated code | The same knowledge must be updated in several places | Extract Function, Slide Statements, Pull Up Method |
| Long function | Multiple intentions, comments as section labels, hard-to-name locals | Extract Function, Replace Temp with Query, Decompose Conditional, Split Loop |
| Long parameter list | Repeated argument groups or callers supplying data already reachable | Introduce Parameter Object, Preserve Whole Object, Replace Parameter with Query |
| Global data | Uncontrolled reads/writes across modules | Encapsulate Variable, Move Function, Combine Functions into Class |
| Mutable data | Aliasing, temporal coupling, updates from many places | Encapsulate Variable, Split Variable, Change Reference to Value, Combine Functions into Transform |
| Divergent change | One module changes for unrelated reasons | Split Phase, Extract Class, Move Function |
| Shotgun surgery | One business change touches many modules | Move Function, Move Field, Combine Functions into Class, Inline Class |
| Feature envy | Logic reads more from another object than its own | Move Function, Extract Function |
| Data clumps | The same values travel together repeatedly | Extract Class, Introduce Parameter Object, Preserve Whole Object |
| Primitive obsession | Strings/numbers encode domain rules or states | Replace Primitive with Object, Replace Type Code with Subclasses |
| Repeated switches | The same type-based branch recurs | Replace Conditional with Polymorphism |
| Loops | A loop mixes selection, transformation, aggregation, or side effects | Split Loop, Replace Loop with Pipeline, Extract Function |
| Lazy element | A function/class adds indirection without meaning | Inline Function, Inline Class, Collapse Hierarchy |
| Speculative generality | Hooks, parameters, or types have no real client | Remove Dead Code, Inline Function, Collapse Hierarchy, Change Function Declaration |
| Temporary field | Fields are valid only during one workflow | Extract Class, Replace Function with Command |
| Message chain | Callers navigate deep object structure | Hide Delegate, Move Function; avoid replacing every chain with a middle man |
| Middle man | A type mostly forwards calls | Remove Middle Man, Inline Function |
| Insider trading | Modules reach into one another's internals | Move Function, Move Field, Hide Delegate, Replace Subclass with Delegate |
| Large class | Too many responsibilities or related subsets of fields | Extract Class, Extract Superclass, Replace Type Code with Subclasses |
| Alternative classes, different interfaces | Equivalent concepts expose incompatible APIs | Change Function Declaration, Move Function, Extract Superclass |
| Data class | Behavior that owns the data lives elsewhere | Move Function, Encapsulate Record, Encapsulate Collection |
| Refused bequest | A subtype rejects or ignores inherited behavior | Push Down Method, Push Down Field, Replace Subclass with Delegate, Replace Superclass with Delegate |
| Comments masking complexity | Comments explain what unclear code should express | Extract Function, Change Function Declaration, Introduce Assertion; keep comments that explain why |

## Selection rules

- Prefer a rename when the structure is sound but intent is hidden.
- Prefer extraction when a unit contains multiple intentions.
- Prefer movement when behavior and the data it uses are separated.
- Prefer encapsulation when mutation or representation leaks.
- Prefer polymorphism only when variation is stable and repeated; a single clear conditional can be simpler.
- Prefer delegation when inheritance couples concepts that vary independently.
- Use inline/removal techniques when an abstraction no longer pays for itself.

Many techniques have an inverse. The context, not the technique name, decides the direction.
