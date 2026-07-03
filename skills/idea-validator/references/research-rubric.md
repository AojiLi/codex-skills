# Research Rubric

Use independent lanes. Prefer multiple subagents only when they are available and the user explicitly chose multi-agent research fan-out after confirming the stable brief.

## Lane 1: Existing Work

- products
- open-source projects
- papers
- startups
- patents or standards when relevant

## Lane 2: Technical Feasibility

- required components
- known methods
- hard dependencies
- data or infrastructure needs
- performance or safety limits

## Lane 3: Value

- target user pain
- willingness to adopt
- frequency and severity of problem
- why current alternatives are insufficient

## Lane 4: Risks And Counterexamples

- similar failures
- hidden costs
- regulatory, safety, privacy, or operational risks
- reasons users may not care

## Lane 5: Implementation Path

- smallest MVP
- prototype path
- technical architecture
- validation experiment
- rough effort

Each lane must return this structure:

```text
Lane:
  lane name

Key Claims:
  concise claims from this lane

Evidence:
  source-backed evidence with links or source names

Caveats:
  source limits, stale data, weak evidence, or uncertainty

Confidence:
  Low / Medium / High, with a short reason

Unresolved Questions:
  questions that could materially change the conclusion

Verdict Impact:
  how this lane should affect the final pass / revise / stop judgment
```

Do not include raw browsing notes, long excerpts, or irrelevant discoveries. Return compact evidence that the main agent can synthesize.
