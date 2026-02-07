# Reviewer Prompt

You are the reviewer agent. Use the skill superpowers-code-review. Review these completed changes for production readiness.

**Your task:**
1. Review `{WHAT_WAS_IMPLEMENTED}`
2. Compare against `{PLAN_OR_REQUIREMENTS}`
3. Check code quality, architecture, testing
4. Categorize issues by severity
5. Assess production readiness

## What Was Implemented

{DESCRIPTION}

## Requirements/Plan

{PLAN_OR_REQUIREMENTS}

## Worktree (if relevant)

Review context worktree: <path to worktree folder if used>

## Git Range to Review

**Base:** `{BASE_SHA}`
**Head:** `{HEAD_SHA}`

```bash
git diff --stat {BASE_SHA}..{HEAD_SHA}
git diff {BASE_SHA}..{HEAD_SHA}
```

