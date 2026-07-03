---
name: idea-validator
description: Clarify vague ideas through dialogue, ask for explicit approval before multi-agent research fan-out, automatically challenge assumptions with skeptic loops after synthesis, and produce feasibility, value, and implementation conclusions. Use when the user has an idea, proposal, product concept, research direction, project plan, or architecture thought and wants to know whether it is reasonable, valuable, differentiated, or how to execute it.
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

### 2. Confirm Research Mode

After the user confirms the stable brief, ask one focused mode question before research:

> Do you want full multi-agent research fan-out for this idea? If yes, I will open five independent research-lane subagents, which Codex may show as visible child/forked conversations: existing work, technical feasibility, user/market value, risks and counterexamples, and implementation path. If no, I will run the same lanes sequentially in the main agent.

Do not proceed to research until the user chooses a mode. Do not treat a request for depth, rigor, or thoroughness as permission to spawn subagents.

If the user chooses full multi-agent mode but the environment does not support subagents or subagent use is unsafe, say so and continue with sequential single-agent research unless the user stops.

### 3. Research Fan-Out

When the user chooses full multi-agent mode and the environment supports subagents, spawn exactly one subagent for each research lane. Give each subagent a narrow, independent lens and ask for sources, evidence, caveats, and unresolved questions.

Treat those subagents as evidence collectors, not final decision makers. The main agent owns synthesis, skeptic loop, and final conclusion.

Recommended lanes:

- existing products, projects, papers, or competitors
- technical feasibility
- user value and market value
- risks, failure cases, and counterexamples
- implementation paths and architecture patterns

If the user chooses single-agent mode, does not approve subagents, subagents are unavailable, or web access is unavailable, do the same lanes sequentially and disclose the limitation.

Do not synthesize or start the skeptic loop until all five research lanes have returned or been completed sequentially.

Use `references/research-rubric.md`. Require each lane to return the structured lane output defined there.

### 4. Synthesize

The main agent synthesizes the five research lanes. Do not delegate final synthesis to a subagent.

Merge research results into:

- facts
- assumptions
- inferences
- open questions
- promising angles
- weak points

Keep source-backed evidence separate from your own reasoning.

### 5. Skeptic Loop

Immediately and automatically run a skeptic pass after synthesis using `references/skeptic-rubric.md`. Do not ask the user whether to start the skeptic loop; it is a required part of this skill.

Run the skeptic loop in the main agent by default. Do not spawn an extra skeptic subagent unless the user has explicitly authorized an additional skeptic subagent, separate from the five research-lane subagents.

If the skeptic identifies a specific evidence gap that could materially change the final verdict, run targeted re-research for only the affected lane. Do not rerun all five research lanes unless multiple verdict-changing gaps span all lanes.

Loop up to 5 times:

1. skeptic identifies the strongest objections
2. main agent answers or modifies the idea
3. skeptic checks whether major objections remain

Stop when there are no unresolved major objections, or after 5 rounds. Do not try to remove every minor concern.

### 6. Final Conclusion

Only produce the final conclusion after clarification, research lanes, main-agent synthesis, and the skeptic loop are complete.

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
- Do not spawn subagents until the user confirms the stable brief and explicitly chooses multi-agent research fan-out.
- Always run the skeptic loop automatically after synthesis, regardless of whether research used subagents or sequential single-agent lanes.
- Use multiple independent research lanes for serious ideas.
- Cite sources when web research is used.
- Separate evidence from inference.
- Do not present consensus if sources disagree.
- Prefer a useful modified idea over a polite approval.
