# WORKFLOWS.md -- Creating Custom Antfarm Workflows

> Workflows define multi-agent pipelines as YAML. Each step runs an agent,
> passes context forward, and the pipeline orchestrates the sequence.

## Workflow YAML Structure

```yaml
name: feature-dev
description: Build a feature from spec to merged PR

steps:
  - id: plan
    agent: planner
    prompt: "Decompose this into implementable stories"
    output: progress/stories.json

  - id: implement
    agent: developer
    prompt: "Implement stories from {plan.output}"
    input: progress/stories.json
    output: progress/implementation.json

  - id: verify
    agent: verifier
    prompt: "Run tests and verify {implement.output}"
    input: progress/implementation.json
    output: progress/verification.json
```

Key fields: `id` (unique step name), `agent` (role from agents directory),
`prompt` (task description), `input`/`output` (context files passed between steps).

## How Agents Pass Context

Each agent writes a structured handoff to its `output` file:

```
STATUS: done
SUMMARY: Decomposed feature into 5 user stories
FILES_CHANGED: progress/stories.json
NEXT_ACTION: Implement story 1 (auth endpoint)
BLOCKERS: none
```

The next agent reads this handoff plus any referenced files. Context flows
forward through the pipeline -- agents never reach backward.

## Adding a New Agent Role

1. Create a directory: `agents/your-role/`
2. Copy the template files: `AGENTS.md`, `SOUL.md`, `HEARTBEAT.md`
3. Customize `AGENTS.md` with the role's process and acceptance criteria
4. Customize `SOUL.md` with the role's personality and decision style
5. Reference it in your workflow YAML by its directory name

```yaml
steps:
  - id: review
    agent: your-role    # matches agents/your-role/
    prompt: "Review the implementation for security issues"
```

## Example: Content Pipeline Workflow

A four-agent pipeline that researches, writes, edits, and publishes content.

```yaml
name: content-pipeline
description: Research a topic and produce a published article

steps:
  - id: research
    agent: researcher
    prompt: "Gather sources and key facts about {topic}"
    output: progress/research.json

  - id: write
    agent: writer
    prompt: "Draft an article using {research.output}"
    input: progress/research.json
    output: progress/draft.md

  - id: edit
    agent: editor
    prompt: "Review and improve {write.output} for clarity and accuracy"
    input: progress/draft.md
    output: progress/final.md

  - id: publish
    agent: publisher
    prompt: "Format and publish {edit.output} to the target platform"
    input: progress/final.md
    output: progress/published.json
```

Each agent has its own identity files. The researcher is thorough and
citation-focused. The writer is creative. The editor is critical. The
publisher is precise and format-aware.

## Tips

- Keep steps small and focused. One agent, one job.
- Use `BLOCKERS` in handoff to signal when a step needs human input.
- Add retry logic in your orchestrator, not in the workflow YAML.
- Test workflows with a single step first, then chain them.
