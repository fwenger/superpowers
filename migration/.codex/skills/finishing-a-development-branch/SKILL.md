---
name: superpowers-finishing-a-development-branch
description: Use when implementation is complete and you need to decide integration path (e.g., local merge, PR creation, keep branch for later, or discard safely) after verifying test status.
---

# Finishing a Development Branch

## Overview

Complete development work by verifying quality, presenting explicit integration options, executing the chosen path, and cleaning up safely.

**Core principle:** Verify -> decide -> execute -> clean up.

**Announce at start:** "I'm using the superpowers-finishing-a-development-branch skill to complete this work."

## Process

### Step 1: Verify Tests

Run the project's test suite first.

If tests fail:
- Report failures clearly.
- Do not proceed to merge/PR/discard options until resolved.

### Step 2: Identify base branch

Determine likely base branch (`main` or `master`) and confirm if uncertain.

### Step 3: Present options

Present exactly these options:

1. Merge back to base branch locally
2. Push and create a Pull Request
3. Keep the branch as-is for later
4. Discard this work

Ask Felix to choose one.

### Step 4: Execute selected option

#### Option 1: Merge locally
1. Checkout base branch
2. Pull latest changes
3. Merge feature branch
4. Re-run tests on merged result
5. Delete merged feature branch

#### Option 2: Push and create PR
1. Push branch
2. Open PR with concise summary and test plan
3. Keep branch/worktree unless Felix asks cleanup

#### Option 3: Keep as-is
- Report branch name and worktree path
- Do not cleanup

#### Option 4: Discard
Require explicit typed confirmation (`discard`) before destructive actions.

After confirmation:
1. Checkout base branch
2. Delete feature branch forcefully if needed
3. Remove associated worktree if applicable

### Step 5: Worktree cleanup rules

- Cleanup for options 1 and 4
- Keep worktree for options 2 and 3 unless Felix asks otherwise

## Red Flags

Never:
- Proceed with failing tests
- Merge without post-merge verification
- Delete work without explicit confirmation
- Force-push or rewrite history without explicit request

## Integration

Called by:
- `superpowers-executing-plans`
- `superpowers-subagent-driven-development`

Pairs with:
- `superpowers-using-git-worktrees`
