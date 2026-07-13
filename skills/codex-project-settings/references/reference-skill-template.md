# Reference Skill Template

Use this only when the project needs reference-backed guidance.

## When To Add

Add a repo-local reference skill when the project depends on:

- papers or research claims
- open-source project comparisons
- protocols, APIs, standards, schemas, or specs
- repeatable reference validation
- design decisions that should cite stable evidence

Do not add it for small projects where existing documentation or a short optional `CONTEXT.md` note is enough.

## Minimal Structure

```text
.agents/
└── skills/
    └── <reference-skill>/
        ├── AGENTS.md
        ├── SKILL.md
        └── references/
            ├── reference-routing.md
            ├── coverage-gaps.md
            ├── review-queue/
            ├── verification/
            ├── rubrics/
            └── decisions/
```

Add `papers/`, `repos/`, `protocols/`, `apis/`, or `schemas/` only when that reference type is actually used.

## Required Behavior

The reference skill must:

- inspect the repo before reference search
- classify the project as empty, existing, or unclear
- confirm project understanding with the user
- keep unverified references in `review-queue/`
- store missing evidence in `coverage-gaps.md`
- write decisions only when references affect architecture, dependencies, safety, or long-term direction
- avoid marking high-risk references accepted without human review

## Naming

Use a project-specific name, for example:

- `<project-name>-references`
- `<domain>-references`
- `<project-name>-research`

Keep names lowercase, hyphenated, and under 64 characters.
