# HEARTBEAT.md -- Periodic Maintenance Protocol

> This file defines what the agent checks on a regular cadence to stay healthy.
> Think of it as a cron job for agent self-maintenance.

## Schedule

- **Frequency:** [every run | daily | on-demand]
- **Trigger:** [automatic at session start | manual invocation | cron]

## Health Checks

### 1. Context Freshness
- [ ] Memory files are current (MEMORY/ directory)
- [ ] No stale progress files from aborted runs
- [ ] Git history is clean -- no uncommitted changes from previous sessions

### 2. Environment Integrity
- [ ] Required tools are available (node, git, etc.)
- [ ] Dependencies are installed and up to date
- [ ] Configuration files are valid (no syntax errors)

### 3. Pipeline State
- [ ] No stuck or orphaned workflow runs
- [ ] SQLite tracking database is consistent
- [ ] All agents can communicate through their expected channels

### 4. Quality Metrics
- [ ] Test pass rate from last N runs: [track and report]
- [ ] Average stories per run: [track and report]
- [ ] Retry rate: [track -- high retry rate indicates prompt or criteria issues]

## Maintenance Actions

### On Context Drift
If memory files are stale or inconsistent:
1. Re-read the current git state
2. Update MEMORY/ files to reflect reality
3. Log the drift in the action log

### On Failed Run Cleanup
If a previous run was interrupted:
1. Check for orphaned branches
2. Clean up partial progress files
3. Reset the workflow state in SQLite
4. Document what happened

### On Dependency Rot
If dependencies are outdated:
1. Run dependency audit
2. Flag security vulnerabilities
3. Create a story for the update (do not auto-update in maintenance)

## Reporting

After each heartbeat, append a status line to the action log:

```
[HEARTBEAT] 2026-02-25T10:00:00Z | status: healthy | checks: 4/4 | actions: 0
[HEARTBEAT] 2026-02-25T10:00:00Z | status: degraded | checks: 3/4 | actions: 1 | note: cleaned orphaned branch
```

## Escalation

If any health check fails repeatedly:
1. Log the failure pattern
2. Notify the human operator
3. Pause automated runs until resolved
