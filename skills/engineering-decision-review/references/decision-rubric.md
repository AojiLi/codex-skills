# Engineering Decision Rubric

Use this rubric to compare options. Do not average away a severe risk.

## Dimensions

- Requirement fit: solves the real user or product problem, not a nearby technical itch.
- Local fit: matches the existing architecture, naming, abstractions, ownership, and style.
- Simplicity: removes or contains complexity instead of spreading it.
- Blast radius: limits affected modules, data, permissions, deployment, and user-visible behavior.
- Reversibility: can be rolled back, feature-flagged, migrated gradually, or abandoned.
- Testability: has direct unit, integration, e2e, fixture, or manual verification paths.
- Data safety: protects migrations, persistence, queues, state, cache, and external side effects.
- Runtime safety: handles latency, concurrency, resource use, retries, failures, and observability.
- Compatibility: preserves public APIs, schemas, file formats, events, and expected workflows.
- Maintenance cost: future engineers can understand, extend, and debug it without hidden coupling.

## Option Review

For each option, answer:

- What changes?
- Which files or contracts prove this option fits?
- What breaks if the assumption is wrong?
- What is the smallest reversible slice?
- Which tests or checks would give confidence?
- What would make this option unacceptable?

## Recommendation Rules

- Prefer the smallest option that satisfies the goal and keeps future options open.
- Prefer reversible steps when repo coverage or product intent is incomplete.
- Prefer local patterns unless there is evidence that the local pattern is the problem.
- Reject clever abstractions unless they remove repeated, proven complexity.
- Reject broad rewrites unless the current structure blocks the goal and incremental paths were considered.

## Red Flags

- Advice based on only one side of a call graph.
- Refactor proposal without reading tests.
- Architecture claim without reading config or deployment assumptions.
- Migration suggestion without inspecting schema, persistence, or compatibility.
- "Best practice" rationale that is not tied to this repository.
