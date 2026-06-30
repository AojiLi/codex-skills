# Merge Rules

Use these rules when settings files already exist.

## Safety

- Do not overwrite existing user instructions without explicit request.
- Do not delete project facts, commands, status history, or local conventions.
- Do not replace a specific local rule with a generic framework rule.
- Preserve unrelated user edits in the working tree.
- When uncertain, append a clearly marked section instead of rewriting.

## Merge Strategy

For each target file:

1. Read the existing file.
2. Identify its current role.
3. Keep useful existing content.
4. Add missing framework sections.
5. Move content only when the destination role is clearly better.
6. Mark uncertain statements as assumptions.
7. Keep the file concise.

## Conflict Handling

If existing instructions conflict with the framework:

- prefer repository-specific instructions
- surface the conflict to the user
- propose a small merge
- do not silently choose the generic rule

## Existing File Actions

- `AGENTS.md`: merge entry rules and routing; keep repository-specific agent instructions.
- `CONTEXT.md`: preserve durable facts; add missing facts discovered from repo orientation.
- `ACTIVE_CONTEXT.md`: overwrite only if user confirms the active direction changed.
- `STATUS.md`: preserve timeline; append a short new entry when setup changes project status.
- `.agents/`: preserve existing local skills; add optional modules only when requested or clearly needed.
