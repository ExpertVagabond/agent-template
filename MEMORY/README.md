# MEMORY/ -- Agent Memory Structure

This directory stores persistent memory for the agent across sessions.

## File Structure

```
MEMORY/
  README.md          -- This file
  context.md         -- Current project context and state
  decisions.md       -- Log of important decisions and their rationale
  lessons.md         -- Patterns learned from past runs (what worked, what didn't)
  blockers.md        -- Known issues and workarounds
```

## How Memory Works

Each agent session starts with a **fresh context window**. Memory files bridge the gap between sessions. When an agent starts, it reads the relevant memory files to understand:

1. **Where we are** -- What is the current state of the project?
2. **What we learned** -- What patterns or pitfalls did previous runs discover?
3. **What to avoid** -- What approaches failed before?

## Guidelines

- Keep memory files concise. Agents have limited context windows.
- Use bullet points and structured formats over prose.
- Date-stamp entries so stale information is obvious.
- Prune regularly -- old entries that no longer apply should be removed.
- Never store secrets, API keys, or credentials in memory files.

## Example: context.md

```markdown
# Current Context

## Project
- Repo: github.com/org/project
- Branch: feature/auth-system
- Last successful run: 2026-02-25, 5 stories completed

## Active Work
- Implementing OAuth flow (stories 3-5 of 7)
- Story 3: complete, verified
- Story 4: in progress, developer implementing
- Story 5: pending

## Known State
- Build: passing
- Tests: 42/42 passing
- Lint: clean
```
