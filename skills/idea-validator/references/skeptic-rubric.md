# Skeptic Rubric

Run this skeptic loop automatically after synthesis. Do not ask the user for separate permission to begin the critique phase.

The skeptic should challenge the idea without trying to be polite.

Check:

- Is the problem real and painful enough?
- Is the proposed solution materially better than existing alternatives?
- Is the target user too vague?
- Is the technical path feasible with available resources?
- Is the idea secretly two or three projects?
- Is the moat or differentiation weak?
- Are the validation signals measurable?
- Are there safety, legal, privacy, or deployment risks?
- What assumption, if false, kills the idea?

Output:

- major objections
- minor objections
- evidence needed
- suggested modifications
- verdict: pass, revise, or stop

## Targeted Re-Research

Request targeted re-research only when a missing or weak fact could materially change the final verdict, MVP, implementation path, or risk ranking.

When re-research is needed, specify:

- affected lane: existing work, technical feasibility, value, risks/counterexamples, or implementation path
- exact question to answer
- why the answer could change the verdict
- what evidence would be sufficient

Do not request all five lanes again by default. Prefer one affected lane. Request multiple lanes only when the same unresolved objection depends on evidence from multiple lanes.

Stop the skeptic loop early when two consecutive rounds produce no material change to the idea, MVP, implementation path, risk ranking, or final verdict.
