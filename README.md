# Agent Template

A minimal, forkable workspace template for AI agent development. Defines the file structure and conventions used by [Antfarm](https://github.com/ExpertVagabond/antfarm-devpipe) and other multi-agent systems.

## What This Is

When building multi-agent workflows, each agent needs a consistent workspace with clear identity, instructions, and memory. This template provides that structure.

Fork it. Customize it. Use it as the foundation for every agent in your pipeline.

> **New here?** Start with the [Quickstart](QUICKSTART.md).

## Structure

```
agent-template/
  AGENTS.md       -- Operational instructions (what the agent does, its process, acceptance criteria)
  SOUL.md         -- Persona and values (how the agent thinks, decides, and communicates)
  HEARTBEAT.md    -- Periodic maintenance protocol (health checks, cleanup, reporting)
  WORKFLOWS.md    -- Guide to creating multi-agent workflow pipelines
  QUICKSTART.md   -- Get running in 5 minutes
  MEMORY/
    README.md     -- How the memory system works
    context.md    -- Current project state (updated each session)
    decisions.md  -- Decision log with rationale
    lessons.md    -- Patterns learned from past runs
    blockers.md   -- Known issues and workarounds
```

## The Three Identity Files

| File | Purpose | Changes How Often |
|------|---------|-------------------|
| **AGENTS.md** | What the agent does. Process, criteria, tools. | Rarely -- set once per role |
| **SOUL.md** | How the agent thinks. Personality, values, style. | Rarely -- set once per role |
| **HEARTBEAT.md** | Self-maintenance. Health checks, cleanup. | Occasionally -- tuned over time |

## The Memory System

The `MEMORY/` directory persists state across sessions. Each agent session starts fresh -- memory files bridge the gap.

- **context.md** -- Updated every session. "Where are we right now?"
- **decisions.md** -- Append-only log. "Why did we choose this approach?"
- **lessons.md** -- Append-only log. "What did we learn?"
- **blockers.md** -- Active list. "What is broken and how do we work around it?"

## Usage with Antfarm

In Antfarm workflows, each agent gets its own copy of these files:

```yaml
agents:
  - id: planner
    name: Planner
    workspace:
      files:
        AGENTS.md: agents/planner/AGENTS.md
        SOUL.md: agents/planner/SOUL.md
        HEARTBEAT.md: agents/planner/HEARTBEAT.md
```

Customize `AGENTS.md` and `SOUL.md` for each role. The Planner has different instructions and personality than the Developer or Verifier.

## Usage Standalone

Even without Antfarm, this pattern works for any AI agent:

1. Fork this repo
2. Customize the identity files for your agent's role
3. Point your agent framework to read these files at session start
4. Update `MEMORY/` at the end of each session

## Related

- [Antfarm](https://github.com/ExpertVagabond/antfarm-devpipe) -- Multi-agent development pipeline
- [snarktank/antfarm](https://github.com/snarktank/antfarm) -- Upstream project (1.6k stars)
- [Ralph](https://github.com/snarktank/ralph) -- Single-agent autonomous loop

## License

MIT
