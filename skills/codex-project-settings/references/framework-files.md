# Framework Files

Use these roles when generating Codex project settings.

## AGENTS.md

Purpose: agent-facing repository entrypoint.

Include:

- where durable context lives
- always-on work rules
- how to handle current direction and status files
- routing to optional repo-local skills
- safety rules for local changes and verification

Avoid:

- long project history
- detailed architecture narratives
- large checklists better placed in `CONTEXT.md` or repo-local skills

## CONTEXT.md

Purpose: durable project facts for agents.

Include:

- project purpose
- target users or use case
- tech stack
- important commands
- architecture summary
- important paths
- external services and integrations
- invariants and constraints
- known decisions
- assumptions that need confirmation

Avoid:

- temporary task state
- detailed chronological status
- speculative plans that are not confirmed

## ACTIVE_CONTEXT.md

Purpose: current working direction. Overwrite it when the active direction changes.

Include:

- last updated date
- current broad direction
- current narrow focus
- current goal
- scope boundaries
- confirmed and uncertain judgments
- next step

Avoid:

- old directions
- long history
- unrelated backlog

## STATUS.md

Purpose: human-facing scan of project state.

Include:

- last updated date
- one-sentence status
- current main line
- concise timeline
- current thinking
- next step
- risks or blockers

Keep it short enough to scan quickly.

## Optional .agents/skills

Create repo-local skills only when useful:

- `<reference-skill>` for project-specific reference collection and validation
- workflow skills for project-specific build/check/release/eval loops

Do not copy optional skills into every project by default.
