# Repo Coverage Gate

Use this gate before giving engineering advice. The goal is relevant coverage, not reading every line in the repository.

## Minimum Coverage

Inspect enough of the repo to understand:

- repository structure and active branch state
- README, AGENTS, CONTEXT, ACTIVE_CONTEXT, STATUS, docs, and runbooks when present
- package manager, build, test, lint, deploy, env, schema, migration, and CI config
- main application entry points
- modules directly related to the user's question
- callers and callees of the affected modules
- related tests, fixtures, mocks, and validation commands
- public API, database, file format, queue, event, auth, permission, or network boundaries

## Coverage Fan-Out

Use subagents when the repo is too large, the decision crosses modules, or context pressure would cause missed evidence.

Ask subagents for evidence, not opinions. Each subagent response should include:

- files inspected
- commands or searches run
- key facts with paths
- uncertainties
- unread but possibly relevant areas
- how the findings affect the decision

The main agent must personally inspect critical files before making the final recommendation.

## Coverage Note Template

Before engineering advice, write:

```text
Repo coverage:
- Read:
- Relevant area appears to be:
- Still not inspected:
- Confidence: low | medium | high
- I should not make strong claims about:
```

## Confidence Rules

- `high`: relevant modules, callers, callees, tests, config, and constraints were inspected.
- `medium`: core path was inspected, but some adjacent tests, configs, or runtime constraints remain unknown.
- `low`: only a partial scan was possible, or important modules/config/tests remain unread.

If confidence is `low`, give an investigation plan or tentative recommendation only.

## Stop Conditions

Stop and ask or investigate further when:

- the repo purpose is unclear
- relevant files are generated, missing, or inaccessible
- tests/config contradict code behavior
- there are multiple plausible owners or entry points
- a recommendation depends on deployment, data, auth, migration, or compatibility facts not yet inspected
