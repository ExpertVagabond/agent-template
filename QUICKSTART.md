# Quickstart

Get an agent running in under 5 minutes.

## Steps

1. **Fork this repo** -- Click "Fork" on GitHub or `gh repo fork ExpertVagabond/agent-template`

2. **Define the role** -- Edit `AGENTS.md` with your agent's mission, process, and acceptance criteria

3. **Set the personality** -- Edit `SOUL.md` with your agent's decision style, tone, and values

4. **Initialize memory** -- Create files in `MEMORY/` as your agent learns (context, decisions, lessons)

5. **Add to Antfarm** -- Register the workspace:
   ```bash
   antfarm add-workspace ./
   ```

6. **Run it** -- Execute a workflow with your agent:
   ```bash
   antfarm run feature-dev "Build a login page with OAuth support"
   ```

## What to Read Next

- [AGENTS.md](AGENTS.md) -- Template for agent instructions
- [SOUL.md](SOUL.md) -- Template for agent personality
- [WORKFLOWS.md](WORKFLOWS.md) -- How to build multi-agent pipelines
- [Antfarm DevPipe](https://github.com/ExpertVagabond/antfarm-devpipe) -- The orchestration layer
