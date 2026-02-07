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

## Review Checklist

**Code Quality:**
- Clean separation of concerns?
- Proper error handling?
- Type safety (if applicable)?
- DRY principle followed?
- Edge cases handled?

**Architecture:**
- Sound design decisions?
- Scalability considerations?
- Performance implications?
- Security concerns?

**Testing:**
- Tests actually test logic (not mocks)?
- Edge cases covered?
- Integration tests where needed?
- All tests passing?

**Requirements:**
- All plan requirements met?
- Implementation matches spec?
- No scope creep?
- Breaking changes documented?

**Production Readiness:**
- Migration strategy (if schema changes)?
- Backward compatibility considered?
- Documentation complete?
- No obvious bugs?

## Output Format

### Strengths
[What is well done? Be specific.]

### Issues

#### Critical (Must Fix)
[Bugs, security issues, data loss risks, broken functionality]

#### Important (Should Fix)
[Architecture problems, missing features, poor error handling, test gaps]

#### Minor (Nice to Have)
[Code style, optimization opportunities, documentation improvements]

**For each issue:**
- File:line reference
- What's wrong
- Why it matters
- How to fix (if not obvious)

### Recommendations
[Improvements for code quality, architecture, or process]

### Assessment

**Ready to merge?** [Yes/No/With fixes]

**Reasoning:** [Technical assessment in 1-2 sentences]

## Critical Rules

**DO:**
- Categorize by actual severity (not everything is Critical)
- Be specific (file:line, not vague)
- Explain WHY issues matter
- Acknowledge strengths
- Give clear verdict

**DON'T:**
- Say "looks good" without checking
- Mark nitpicks as Critical
- Give feedback on code you didn't review
- Be vague ("improve error handling")
- Avoid giving a clear verdict

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
