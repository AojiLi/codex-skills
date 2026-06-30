# Implementation Slicing

Use this reference after choosing a direction. The goal is to turn an engineering recommendation into safe, inspectable work.

## Slice Rules

- Start with the smallest change that proves or disproves the direction.
- Keep each slice independently reviewable and testable.
- Separate mechanical movement from behavior changes.
- Separate schema or data migrations from application behavior when possible.
- Add observability or tests before risky behavior changes when the current system is under-covered.
- Prefer compatibility shims or adapters before broad call-site migrations.
- Stop expanding scope when a slice reveals a wrong assumption.

## Slice Template

For each slice, write:

```text
Slice:
- Goal:
- Files likely touched:
- Behavior change:
- Validation:
- Rollback or stop condition:
- Decision after this slice:
```

## Verification Planning

Include the most direct checks:

- existing targeted tests
- new tests needed
- build, typecheck, lint, or static checks
- migration dry run or fixture replay
- API/schema compatibility check
- manual flow when automated coverage is missing

If a check cannot run, state why and what residual risk remains.

## Stop Conditions

Stop or re-evaluate when:

- tests reveal behavior different from the system model
- the change touches more modules than expected
- migration or compatibility risk grows
- implementation requires a new abstraction not justified by current evidence
- the user goal changes
