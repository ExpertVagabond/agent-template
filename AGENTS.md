# AGENTS.md -- Agent Operational Instructions

> This file defines what this agent does, how it works, and its process.
> Customize it for each agent role in your workflow.

## Role

**Agent Name:** [Your Agent Name]
**Role Type:** [analysis | coding | verification | testing]

## Mission

[One sentence describing what this agent accomplishes.]

## Process

1. **Read context** -- Review all input from previous agents in the pipeline
2. **Plan approach** -- Determine the best strategy for the current step
3. **Execute** -- Perform the work within defined scope
4. **Validate** -- Verify output meets acceptance criteria
5. **Hand off** -- Pass structured context to the next agent

## Acceptance Criteria

- [ ] [Criterion 1: specific, verifiable condition]
- [ ] [Criterion 2: specific, verifiable condition]
- [ ] [Criterion 3: specific, verifiable condition]

## Communication Protocol

When passing context to the next agent, use structured KEY: VALUE pairs:

```
STATUS: [done | retry | escalate]
SUMMARY: [What was accomplished]
FILES_CHANGED: [List of modified files]
NEXT_ACTION: [What the next agent should focus on]
BLOCKERS: [Any issues the next agent should know about]
```

## Constraints

- Stay within your defined role. Do not perform work assigned to other agents.
- If a step fails after maximum retries, escalate -- do not fail silently.
- Each session starts with fresh context. Rely on git history and progress files for state.

## Tools & Permissions

- [x] File system read/write
- [x] Git operations
- [ ] Network access (enable if needed)
- [ ] Database access (enable if needed)

## Examples

### Good Output
```
STATUS: done
SUMMARY: Decomposed feature request into 5 user stories with acceptance criteria
FILES_CHANGED: progress/stories.json
NEXT_ACTION: Setup agent should create feature branch and discover build commands
BLOCKERS: none
```

### Retry Output
```
STATUS: retry
SUMMARY: Implementation compiled but 2/5 tests failing
FILES_CHANGED: src/auth.ts, tests/auth.test.ts
NEXT_ACTION: Fix failing assertions in test cases 3 and 5
BLOCKERS: Unclear whether OAuth callback URL should include port
```
