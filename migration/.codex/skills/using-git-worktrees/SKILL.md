---
name: superpowers-using-git-worktrees
description: Use when starting feature work that needs isolation from the current workspace or before executing implementation plans (e.g., risky refactors, parallel branches, multi-task delivery). Create an isolated git worktree with safety and baseline verification.
---

# Using Git Worktrees

## Overview

Git worktrees create isolated workspaces that share one repository, so you can work on multiple branches without branch-switching churn.

**Core principle:** Systematic directory selection + safety verification = reliable isolation.

**Announce at start:** "I'm using the superpowers-using-git-worktrees skill to set up an isolated workspace."

## Directory Selection Process

Follow this priority order:

### 1) Check Existing Directories

```bash
ls -d .worktrees 2>/dev/null
ls -d worktrees 2>/dev/null
```

- If found, use it.
- If both exist, `.worktrees` wins.

### 2) Check Project Guidance

```bash
grep -i "worktree.*director" AGENTS.md 2>/dev/null
```

- If preference is specified, use it.

### 3) Ask Felix

If no directory exists and no project preference exists, ask Felix:

1. `.worktrees/` (project-local, hidden)
2. `~/.codex/worktrees/<project-name>/` (global)

## Safety Verification

### Project-local worktrees (`.worktrees` or `worktrees`)

MUST verify the directory is ignored before creating a worktree:

```bash
git check-ignore -q .worktrees 2>/dev/null || git check-ignore -q worktrees 2>/dev/null
```

If NOT ignored:
1. Add ignore entry to `.gitignore`
2. Commit the `.gitignore` change
3. Continue worktree creation

### Global worktree path

No project `.gitignore` verification required for `~/.codex/worktrees/...`.

## Creation Steps

### 1) Detect project name

```bash
project=$(basename "$(git rev-parse --show-toplevel)")
```

### 2) Create worktree

```bash
# Project-local
# git worktree add .worktrees/<branch-name> -b <branch-name>

# Global
# git worktree add ~/.codex/worktrees/$project/<branch-name> -b <branch-name>
```

Then `cd` into the new worktree.

### 3) Run setup

```bash
# Node
[ -f package.json ] && npm install

# Rust
[ -f Cargo.toml ] && cargo build

# Python
[ -f requirements.txt ] && pip install -r requirements.txt
[ -f pyproject.toml ] && poetry install

# Go
[ -f go.mod ] && go mod download
```

### 4) Verify clean baseline

Run project-appropriate tests and verify baseline before implementation.

If tests fail, report and ask Felix whether to proceed.

### 5) Report readiness

Report full path, baseline result, and readiness.

## Red Flags

Never:
- Create a project-local worktree before ignore verification
- Skip baseline test verification
- Proceed on failing baseline without Felix's approval
- Assume directory location when ambiguous

Always:
- Follow directory priority
- Verify ignore state for project-local directories
- Run setup and baseline verification

## Integration

Called by:
- `superpowers-brainstorming`
- `superpowers-executing-plans`
- `superpowers-subagent-driven-development`

Pairs with:
- `superpowers-finishing-a-development-branch`
