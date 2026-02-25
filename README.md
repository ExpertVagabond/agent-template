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

## For AI Companies

If you are building multi-agent coding tools -- whether that is an IDE copilot, an agent platform, or an autonomous dev pipeline -- this workspace pattern solves the hard problems you are already hitting:

### The Problem

Autonomous agents lose context between sessions. They forget decisions, repeat mistakes, and have no structured way to hand off work to the next agent in a pipeline. Every AI company building multi-agent dev tools is independently reinventing this wheel.

### The Solution

This template is the workspace pattern that powers [Antfarm](https://github.com/ExpertVagabond/antfarm-devpipe), which has autonomously shipped 33 stories across 3 production Solana repos with zero regressions. Here is how the pieces map:

| File | What It Does | Analogy |
|------|-------------|---------|
| **AGENTS.md** | Operational instructions -- what the agent does, its process, acceptance criteria | What Claude Code's `CLAUDE.md` does for human developers |
| **SOUL.md** | Agent personality and values -- how it reasons, decides, and communicates | Alignment instructions for autonomous agents that make judgment calls |
| **MEMORY/** | Persistent learning across sessions -- context, decisions, lessons, blockers | RAG-lite without the vector database infrastructure |
| **HEARTBEAT.md** | Self-maintenance protocol -- health checks, cleanup, reporting | Keeps long-running agents from accumulating drift |
| **WORKFLOWS.md** | Multi-agent coordination -- how agents hand off work to each other | The orchestration glue between your agent steps |

### Why This Matters for Your Platform

1. **Context persistence without infrastructure** -- No vector DB, no embedding pipeline. Just markdown files in git. Works offline, works at scale, works with any LLM backend.
2. **Agent identity prevents role confusion** -- When you have 6 agents in a pipeline, each one needs to know exactly what it does and does not do. AGENTS.md + SOUL.md eliminate the "planner that starts coding" failure mode.
3. **Memory compounds over sessions** -- Each run makes the next run smarter. `lessons.md` captures patterns. `decisions.md` prevents revisiting settled questions. `blockers.md` routes around known issues.
4. **Fork-and-customize** -- Every agent role gets its own copy of these files. The Planner's AGENTS.md is completely different from the Verifier's. Same structure, different specialization.

### Quick Integration

```bash
# Fork this template for each agent role in your pipeline
gh repo fork ExpertVagabond/agent-template --clone

# Customize identity files for your agent's role
# Point your agent framework to read these files at session start
# Update MEMORY/ at the end of each session
```

Your agents already write code. This template gives them structured memory, clear identity, and reliable handoff -- the missing pieces that turn individual agents into a coordinated team.

## Related

- [Antfarm](https://github.com/ExpertVagabond/antfarm-devpipe) -- Multi-agent development pipeline (33 stories shipped)
- [snarktank/antfarm](https://github.com/snarktank/antfarm) -- Upstream project (1.6k stars)
- [Ralph](https://github.com/snarktank/ralph) -- Single-agent autonomous loop

## License

MIT
