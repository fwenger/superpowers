---
name: superpowers-code-review
description: Use when reviewing completed implementation work in an independent reviewer thread/agent (e.g., task batch handoff, pre-merge verification, external review request).
---

# Code Review

Review completed changes for spec compliance, quality, risk, and production readiness.

**Core principle:** Independent reviewer perspective catches issues implementers miss.

## Review Mode

Preferred mode:
- Start a new thread/new agent as reviewer.
- Run this skill in that reviewer thread.

Fallback mode (lower assurance):
- If independent reviewer thread is unavailable, run this skill in the current thread and explicitly state reduced independence.

## Inputs Required

- `{WHAT_WAS_IMPLEMENTED}`
- `{PLAN_OR_REQUIREMENTS}`
- `{DESCRIPTION}`
- `{BASE_SHA}`
- `{HEAD_SHA}`

## Process

1. Read the implementation scope and requirements.
2. Inspect `git diff --stat {BASE_SHA}..{HEAD_SHA}` and full diff.
3. Evaluate code quality, architecture, testing, requirements, and production readiness.
4. Categorize findings by severity: Critical, Important, Minor.
5. Give a merge-readiness verdict with technical reasoning.

## Output Requirements

For each issue:
- file:line reference
- what is wrong
- why it matters
- concrete fix direction

Always include:
- Strengths
- Issues by severity
- Recommendations
- Assessment (`Yes/No/With fixes`)

## Red Flags

Never:
- Approve without checking the actual diff
- Treat all issues as Critical
- Give vague feedback without file references
- Skip a clear merge-readiness verdict
