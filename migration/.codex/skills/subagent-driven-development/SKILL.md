---
name: superpowers-subagent-driven-development
description: Use when executing a written implementation plan with mostly independent tasks in the current session (e.g., task-by-task delivery with review gates and fast iteration).
---

# Subagent-Driven Development

## Overview

Execute a plan task-by-task with strict review gates after each task.

**Core principle:** implement -> spec review -> quality review -> proceed.

## Capability Gate

This workflow requires task delegation support for full fidelity.

If delegation is available:
- Use a fresh implementation agent per task.
- Use separate review passes after each task.

If delegation is not available:
- Execute tasks sequentially in the main agent.
- Simulate the same review gates explicitly before moving on.

State which mode is active.

## When to Use

Use when:
- A written plan exists
- Tasks are mostly independent
- You want tight per-task quality gates

Use `superpowers-executing-plans` instead when:
- You prefer larger batch checkpoints over per-task gates
- Tasks are tightly coupled

## Process

### Step 1: Load plan and create tracking

- Read plan once
- Extract task list
- Track task state with `update_plan`

### Step 2: Implement one task

For each task:
1. Execute implementation (delegated or sequential)
2. Verify task-local tests/checks
3. Summarize changes and evidence

### Step 3: Spec compliance review

Confirm task output matches plan requirements exactly.
If gaps exist, fix and re-review.

### Step 4: Code quality review

Run `superpowers-requesting-code-review` for this task scope.
If Critical/Important findings exist, fix and re-review.

### Step 5: Mark complete and continue

Only move to next task after both reviews are clear.

### Step 6: Final closeout

After all tasks are complete, use `superpowers-finishing-a-development-branch`.

## Red Flags

Never:
- Skip either review gate
- Move to next task with unresolved Important findings
- Parallelize overlapping tasks without explicit coordination
- Claim completion without verification evidence

## Integration

Required companion skills:
- `superpowers-using-git-worktrees`
- `superpowers-writing-plans`
- `superpowers-requesting-code-review`
- `superpowers-receiving-code-review`
- `superpowers-test-driven-development`
- `superpowers-verification-before-completion`
- `superpowers-finishing-a-development-branch`

Optional accelerator:
- `superpowers-dispatching-parallel-agents` (only when capability and independence are verified)
