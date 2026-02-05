---
name: superpowers-dispatching-parallel-agents
description: Use when handling 2+ independent tasks that can run concurrently (e.g., unrelated failing test files, separate subsystems, non-overlapping change sets) without shared-state conflicts.
---

# Dispatching Parallel Agents

## Overview

When multiple failures are truly independent, parallel investigation reduces cycle time.

**Core principle:** One independent domain per agent/execution lane.

## Capability Gate

Before parallel dispatch, verify a real parallel mechanism exists in this session.

If verified parallel capability exists:
- Dispatch one lane per independent domain.

If not available:
- Use sequential fallback in small batches with explicit checkpoints.

State this explicitly before execution.

## When to Use

Use when:
- There are 2+ failures with unrelated root causes
- Tasks touch different files/subsystems
- Work can proceed without shared-state interference

Do not use when:
- Failures are likely coupled
- Tasks edit overlapping code paths
- Ordering dependencies exist

## Process

1. Partition work into independent domains.
2. Write focused task prompts with scope, constraints, expected output.
3. Dispatch in parallel if capability is verified.
4. Collect results and integrate carefully.
5. Run full verification suite.

## Prompt Requirements

Each lane prompt should include:
- Exact scope (file/test/subsystem)
- Success criteria
- Constraints (what not to change)
- Required evidence in output

## Integration Safety

After lanes return:
- Check for edit conflicts
- Resolve integration issues
- Re-run full test/verification suite
- Do not assume lane-local green means system-level green

## Red Flags

Never:
- Parallelize coupled tasks
- Skip capability verification
- Skip full integration verification
- Accept incomplete lane outputs as done

## Integration

- Pairs with `superpowers-subagent-driven-development`
- Alternative to strictly sequential execution in `superpowers-executing-plans`
