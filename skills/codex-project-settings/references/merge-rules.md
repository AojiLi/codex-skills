# Merge Rules

Use these rules when settings files already exist.

## Safety

- Do not overwrite existing user instructions without explicit request.
- Do not silently discard durable project facts, commands, useful history, or local conventions.
- Do not replace a specific local rule with a generic framework rule.
- Preserve unrelated user edits in the working tree.
- When uncertain, append a clearly marked section instead of rewriting.

## Budget Handling

- Apply the optional context-file soft and hard budgets in `framework-files.md`.
- Treat Codex's discovered `AGENTS.md` byte limit separately from the framework's optional context budget.
- At the soft budget, compact the file during the next substantive update.
- At the hard budget, do not append. Remove duplication, rewrite stale material, or move detail to a linked source of truth first.
- For English prose, check words with tools such as `wc -w`. For Chinese or other languages without reliable word boundaries, use approximate tokens or a project-calibrated character count.
- Treat 200 lines per file as a secondary maximum, not as a substitute for content-density review.

## Merge Strategy

For each target file:

1. Read the existing file.
2. Identify its current role.
3. Keep useful existing content.
4. Add missing framework sections.
5. Move content only when the destination role is clearly better.
6. Mark uncertain statements as assumptions.
7. Remove cross-file duplication by keeping one canonical copy and linking to it.
8. Keep the file concise.

## Conflict Handling

If existing instructions conflict with the framework:

- prefer repository-specific instructions
- surface the conflict to the user
- propose a small merge
- do not silently choose the generic rule

## Existing File Actions

- `AGENTS.md`: merge natively discovered commands, rules, verification requirements, and routing; keep repository-specific agent instructions and avoid current task state.
- `CONTEXT.md`: preserve durable facts, replace verified stale facts in place, and move detailed history or subsystem material to authoritative linked documents. Remove commands or rules already canonical in `AGENTS.md`.
- `.agents/`: preserve existing local skills; add optional modules only when requested or clearly needed.

Do not create a missing optional file merely because the framework names it. Re-evaluate whether the repository still needs that role before restoring or adding it.
