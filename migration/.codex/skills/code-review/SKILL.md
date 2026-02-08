---
name: superpowers-code-review
description: Use when reviewing completed implementation work in an independent reviewer thread/agent (e.g., task batch handoff, pre-merge verification, external review request).
---

# Code Review

Review completed changes for spec compliance, quality, risk, and production readiness.

**Core principle:** Independent reviewer perspective catches issues implementers miss.
**Repository default:** Review in local mode (new reviewer thread + git SHA range) unless Felix explicitly requests PR mode.

## Review Mode

Preferred mode in this repository:
- Start a new thread/new agent as reviewer.
- Run this skill in that reviewer thread against local git range handoff.

PR mode (optional):
- Use when Felix explicitly requests PR-based review.
- Review against PR URL plus PR discussion/context.

Fallback mode (lower assurance):
- If independent reviewer thread is unavailable, run this skill in the current thread and explicitly state reduced independence.

## Inputs Required

- `{WHAT_WAS_IMPLEMENTED}`
- `{PLAN_OR_REQUIREMENTS}`
- `{DESCRIPTION}`
- Local mode: `{BASE_SHA}` and `{HEAD_SHA}`
- PR mode: `{PR_URL}` (plus `{BASE_SHA}`/`{HEAD_SHA}` when provided)

## Process

1. Read the implementation scope and requirements.
2. Determine review source:
   - Local mode: inspect `git diff --stat {BASE_SHA}..{HEAD_SHA}` and full diff.
   - PR mode: inspect PR diff and review context at `{PR_URL}`.
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

**Prompt for Implementer:** If available, use skill superpowers-receiving-code-review now.

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
