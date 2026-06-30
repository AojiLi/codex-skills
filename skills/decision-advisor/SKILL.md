---
name: decision-advisor
description: "Analyze any user decision, choice, tradeoff, option selection, or whether-to-do-something question. Use when the user asks for decision help, wants a recommendation, or invokes decision-advisor. The workflow clarifies the decision, candidate options, background, purpose, core question, jurisdiction, constraints, and decision weights; runs research-backed analysis through economics, strategy, psychology, risk management, legal/regulatory, and technical feasibility lenses; applies critique-revision loops; and returns a clear recommendation, alternatives, action plan, and review signals."
---

# Decision Advisor

## Overview

Use this skill to help the user make a decision, not to replace the user's authority. Produce a defensible recommendation under the user's confirmed context, constraints, and value tradeoffs.

Default to the user's language. If the user writes in Chinese, ask questions and deliver the final report in Chinese even when sources are in other languages.

## Non-Negotiables

- Do not start with a long intake form. Start with one question unless the user already provided the answer.
- Do not launch the six-lens analysis until the user explicitly confirms the background, purpose, core question, options, jurisdiction, constraints, and weight framework.
- After the decision frame and weight framework are confirmed, ask the user whether to use full multi-agent mode before doing research or six-lens analysis.
- Do not spawn subagents automatically. The six default lenses are designed to run as six independent lens subagents only when the user explicitly authorizes subagents or parallel agent work for this decision and the environment supports it.
- Always ask the user to confirm the applicable region or jurisdiction before the legal/regulatory lens runs. Do not silently infer it from context.
- Default to considering "maintain the status quo / do nothing / delay the decision" as a candidate option unless it is clearly impossible or the user confirms excluding it.
- Give a clear recommendation unless decisive information is missing or the decision turns entirely on a personal value judgment the user has not resolved.
- Use Low, Medium, or High confidence with reasons. Do not use pseudo-precise percentages unless a real quantitative model supports them.
- Do not use an emergency shortcut mode. Follow the full workflow unless the user stops or redirects.

## Workflow

### 1. Open With One Question

If the user has not already described the decision, ask only:

> What decision do you need to make? If you already have candidate options, list them too; if not, just describe the problem you want to solve.

Use the user's language for this question.

### 2. Frame The Decision

From the user's short answer, infer and present a compact draft:

- background and context
- purpose or desired outcome
- core decision question
- known candidate options, plus the baseline option of status quo / no action / delayed decision unless clearly impossible
- critical missing information

Ask the user which parts are inaccurate or incomplete. Keep revising until the user explicitly confirms the background, purpose, and core question.

If the user only adds information without confirming, restate the updated frame and ask for confirmation again.

### 3. Confirm Options, Jurisdiction, And Constraints

Before research or multi-agent analysis, confirm:

- candidate options, including status quo / no action / delayed decision as a baseline
- applicable region or jurisdiction for legal/regulatory analysis
- hard constraints, red lines, budget, time window, and unacceptable outcomes
- any critical facts that could change the recommendation

Ask about critical gaps before continuing. For non-critical gaps, state assumptions and proceed only after the core frame is confirmed.

### 4. Confirm The Weight Framework

Generate 2-4 scenario-specific candidate weight frameworks from the confirmed background, purpose, and core question. Do not force numeric percentages. Prefer:

- ranked priorities
- hard constraints versus soft preferences
- natural-language tradeoff statements
- red lines and acceptable losses
- time, money, effort, reputation, relationship, learning, upside, and downside tradeoffs when relevant

Name the frameworks based on the specific decision, not generic templates. Examples of good names are "cash-flow protection first", "fast market validation first", "career reputation first", or "family stability first".

If the user rejects all candidate frameworks, ask the user to define their own priorities. Do not proceed until one weight framework is explicitly confirmed.

### 5. Confirm Analysis Mode

After the user confirms the background, purpose, core question, candidate options, jurisdiction, constraints, and weight framework, ask one focused mode question before research:

> Do you want full multi-agent analysis for this decision? If yes, I will open six lens subagents, one for each default lens, and each lens will run its own critique-revision loop. If no, I will run the six lenses sequentially as a single-agent analysis with a compact local critique loop.

Do not proceed to research or six-lens analysis until the user chooses a mode.

If the user chooses full multi-agent mode but the environment does not support subagents or subagent use is unsafe, say so and continue with single-agent sequential analysis unless the user stops.

### 6. Research With Source Discipline

Use current research for external facts, market data, prices, law, regulation, technical feasibility, industry trends, or other time-sensitive claims. Cite sources when research is used.

Source quality order:

1. Primary and authoritative sources: laws, regulations, regulator guidance, official documentation, government statistics, company filings, earnings reports, academic papers, and official product docs.
2. Credible secondary sources: reputable media, industry reports, and expert analysis.
3. Blogs, forums, social media, and reposts only as leads, not as key evidence.

If sources are weak, conflicting, unavailable, or stale, lower confidence and say why.

### 7. Run Six-Lens Analysis

The six default lenses are intended to map to six independent lens agents when subagents are available and authorized:

Default lenses:

- economics: incentives, opportunity cost, marginal cost/benefit, expected value, resource allocation
- strategy: positioning, timing, optionality, competitive advantage, long-term fit
- psychology: bias, motivation, behavior change, stakeholder perception, emotional and execution dynamics
- risk management: downside, tail risk, reversibility, mitigations, monitoring, stop conditions
- legal/regulatory: confirmed jurisdiction, compliance, contracts, employment, tax, data, platform rules, regulatory exposure; provide risk identification and general information, not formal legal advice
- technical feasibility: implementation path, dependencies, skills, reliability, scalability, integration, operational complexity

When the user chooses full multi-agent mode and the environment supports subagents, spawn exactly one subagent for each confirmed lens and run them in parallel where practical. Pass each subagent the confirmed decision frame, candidate options, jurisdiction, constraints, and weight framework. If the user replaces a default lens with a more relevant one, still use one subagent per confirmed lens.

If the user chooses single-agent mode, does not approve subagents, the environment does not expose subagent tools, or subagent use is otherwise unsafe, run the same six lenses sequentially in the main agent and disclose that this is a single-agent simulation rather than true multi-agent analysis.

Each lens must return:

- most important judgment from that lens
- reasoning and key evidence
- evaluation of each candidate option
- key risks, counterexamples, or failure modes
- recommendation ranking from that lens
- confidence level and reason
- tradeoffs the main agent should consider

If a lens has low relevance, say so directly instead of forcing analysis. The main agent may suggest replacing that lens with a more relevant one, but must get user confirmation before replacing any default lens.

### 8. Run Critique-Revision Loops

For each lens, run a same-lens critique after the initial lens conclusion. Do not spawn extra critic subagents by default. Ask each lens subagent to perform its own critique-revision loop, or simulate the loop locally when running sequentially.

The critique looks for:

- factual gaps or weak sources
- logical jumps
- misuse of the confirmed weight framework
- ignored counterexamples
- underestimated risks
- missing candidate options
- overconfident conclusions

The original lens agent must answer the critique by either revising the conclusion or explaining why a critique is not accepted. Repeat up to 3 rounds. Stop early if no material issue remains.

Return only a compressed audit to the main agent:

- whether the initial judgment changed
- strongest critique points
- accepted revisions
- rejected critiques and reasons
- remaining uncertainty
- final lens conclusion
- confidence change

Do not show the user every intermediate round unless the user asks for the audit trail.

### 9. Synthesize Across Lenses

The main agent integrates the final lens outputs and handles cross-lens conflict. Do not default to a mid-process user review. Pause and ask the user only when:

- lens conclusions conflict in a way the confirmed weights cannot resolve
- key sources directly contradict each other
- a missing critical fact could reverse the recommendation
- a required value tradeoff remains unconfirmed

Separate source-backed facts from inferences and value judgments.

### 10. Final Report

Return a concise but complete decision report:

1. Decision frame: background, purpose, core question, options, jurisdiction, confirmed weight framework
2. Recommendation: clear preferred option, confidence level, and the shortest defensible reason
3. Decision matrix: compare candidate options against the confirmed criteria; use qualitative levels or 1-5 scores, but do not treat the matrix as a mechanical verdict
4. Why this wins under the confirmed weights
5. Six-lens summaries: final local conclusion, key evidence, important critique revisions, confidence
6. Alternatives: viable backup option, options not recommended, and why
7. Weight sensitivity: how the conclusion might change under different reasonable priorities
8. Judgment types: distinguish facts, inferences, and value judgments
9. Assumptions and unresolved uncertainties
10. Action plan: next steps, validation actions, risk mitigations, stop conditions, and review signals
11. What would change the recommendation

If no clear recommendation is possible, say exactly what decisive information is missing and how to obtain it.
