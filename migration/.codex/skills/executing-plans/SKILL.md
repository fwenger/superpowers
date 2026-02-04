---
name: superpowers-executing-plans
description: Use when you have a written implementation plan and need disciplined execution with review checkpoints (e.g., multi-task plans, phased migrations, handoff-ready delivery).
---

# Executing Plans

## Overview

Load a written plan, review it critically, execute tasks in batches, and report verification evidence between batches.

**Core principle:** Batch execution with checkpoints.

**Announce at start:** "I'm using the superpowers-executing-plans skill to implement this plan."

## The Process

### Step 1: Load and Review Plan

1. Read the plan file completely.
2. Identify concerns or ambiguities.
3. If concerns exist, raise them with Felix before starting.
4. If clear, create `update_plan` items and proceed.

### Step 2: Execute Batch

Default first batch: first 3 tasks.

For each task:
1. Mark in progress.
2. Follow plan steps exactly.
3. Run required verifications.
4. Mark completed.

### Step 3: Report

When batch completes:
- Report what changed.
- Report verification results.
- Say: "Ready for feedback."

### Step 4: Continue

Based on feedback:
- Apply requested corrections.
- Execute next batch.
- Repeat until all tasks complete.

### Step 5: Complete Development

After all tasks complete and verifications pass:
- Announce: "I'm using the superpowers-finishing-a-development-branch skill to complete this work."
- Use `superpowers-finishing-a-development-branch` for final verification and integration decision.

## Stop Conditions

Stop immediately and ask Felix when:
- A blocker appears mid-batch (dependency, failing verification, unclear instruction)
- The plan has critical gaps
- You do not understand an instruction
- Verification fails repeatedly

Do not guess through blockers.

## Remember

- Review critically before action
- Follow plan steps exactly
- Never skip verification
- Report only after batch checkpoints
- Do not start implementation on main/master without explicit permission

## Integration

Required workflow skills:
- `superpowers-using-git-worktrees` - setup isolated workspace
- `superpowers-writing-plans` - provides the plan structure
- `superpowers-finishing-a-development-branch` - closes out work safely
