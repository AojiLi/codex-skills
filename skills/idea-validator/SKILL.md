---
name: idea-validator
description: Clarify vague ideas through dialogue, run parallel research, challenge assumptions with skeptic loops, and produce feasibility, value, and implementation conclusions. Use when the user has an idea, proposal, product concept, research direction, project plan, or architecture thought and wants to know whether it is reasonable, valuable, differentiated, or how to execute it.
---

# Idea Validator

Use this skill before implementation when the user has an incomplete idea and needs a rigorous path from vague concept to grounded decision.

## Workflow

### 1. Clarify The Idea

Interview the user one question at a time until the idea has a stable brief. Use `references/interview-rubric.md`.

Do not research or judge the idea too early. First clarify:

- problem
- target user
- proposed solution
- why now
- success criteria
- constraints
- unknowns

Stop this phase when you can summarize the idea in one paragraph and the user agrees or corrects it.

### 2. Research Fan-Out

Spawn multiple subagents when available. Give each subagent a narrow, independent lens and ask for sources, evidence, and caveats.

Recommended lanes:

- existing products, projects, papers, or competitors
- technical feasibility
- user value and market value
- risks, failure cases, and counterexamples
- implementation paths and architecture patterns

If subagents or web access are unavailable, do the same lanes sequentially and disclose the limitation.

Use `references/research-rubric.md`.

### 3. Synthesize

Merge research results into:

- facts
- assumptions
- inferences
- open questions
- promising angles
- weak points

Keep source-backed evidence separate from your own reasoning.

### 4. Skeptic Loop

Run a skeptic pass using `references/skeptic-rubric.md`.

Loop up to 5 times:

1. skeptic identifies the strongest objections
2. main agent answers or modifies the idea
3. skeptic checks whether major objections remain

Stop when there are no unresolved major objections, or after 5 rounds. Do not try to remove every minor concern.

### 5. Final Conclusion

Use `references/final-report-structure.md`.

Return:

- feasibility verdict
- value verdict
- differentiation
- modified idea
- MVP
- implementation path
- validation experiments
- major risks
- remaining unknowns
- recommended next step

Be willing to say the idea is not worth doing, or worth doing only after modification.

## Output Rules

- Ask clarifying questions before research when the idea is underspecified.
- Use multiple independent research lanes for serious ideas.
- Cite sources when web research is used.
- Separate evidence from inference.
- Do not present consensus if sources disagree.
- Prefer a useful modified idea over a polite approval.
