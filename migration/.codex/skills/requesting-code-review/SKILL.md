---
name: superpowers-requesting-code-review
description: Use when you need to request an independent code review from another thread/agent (e.g., user asks to "request code review", end of execution batch, major feature completion, pre-PR readiness checks).
---

# Requesting Code Review

Request independent review early so issues are caught before they cascade.

**Core principle:** Review early, review often.
**Repository default:** In this repository, use local reviewer-thread handoff unless Felix explicitly asks for PR-based review.

## When to Request Review

Trigger cues (invoke this skill):
- "request code review"
- "ask another agent/thread to review this"
- "prepare reviewer prompt/handoff"
- "get an independent review before merge"

**Mandatory:**
- After each task in subagent-driven development
- After completing major feature
- Before merge to main

**Optional but valuable:**
- When stuck (fresh perspective)
- Before refactoring (baseline check)
- After fixing complex bug

## Review Modes

### Mode A (Default in this repository): Local New Thread Reviewer

Use a separate thread/new agent as reviewer and run `superpowers-code-review` there.

Why preferred:
- Independent reviewer perspective
- Better chance to catch implementer blind spots
- No remote push/PR requirement for routine review handoff in this repo

### Mode B (Optional): PR-Based Reviewer Handoff

Use when Felix explicitly asks for PR-based review or when external collaboration requires PR threads.

Required:
- Push branch and provide PR URL
- Put review context directly into PR body/comment
- Ask reviewer thread to review using PR URL + requirements

### Mode C (Fallback): Same Thread Self-Review

Use only when a separate reviewer thread is not available.

Required:
- Explicitly state reduced independence
- Follow `superpowers-code-review` checklist exactly
- Treat findings conservatively

## How to Request (Mode A)

**1. Get git SHAs:**
```bash
BASE_SHA=$(git rev-parse HEAD~1)  # or origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. Start a reviewer thread and paste review prompt:**

Use template at `reviewer-prompt.md`, fill placeholders:

**Placeholders:**
- `{WHAT_WAS_IMPLEMENTED}` - What you just built
- `{PLAN_OR_REQUIREMENTS}` - What it should do
- `{BASE_SHA}` - Starting commit
- `{HEAD_SHA}` - Ending commit
- `{DESCRIPTION}` - Brief summary

**2.5 Present the filled prompt to Felix to copy/paste into a new thread:**
- Provide the fully filled prompt text directly in chat.
- Instruct Felix to paste it into a new Codex thread/agent.

**3. Process reviewer feedback:**
- Use `superpowers-receiving-code-review` for feedback handling, pushback, and fix ordering.

## How to Request (Mode B: PR-Based)

1. Push branch and open/update PR.
2. Add a PR context block (body or comment) containing:
   - `WHAT_WAS_IMPLEMENTED`
   - `PLAN_OR_REQUIREMENTS`
   - `DESCRIPTION`
   - `BASE_SHA`
   - `HEAD_SHA`
3. Start reviewer thread, provide PR URL and ask it to run `superpowers-code-review`.
4. Process reviewer feedback with `superpowers-receiving-code-review`.

## Integration with Workflows

**Subagent-Driven Development:**
- Review after EACH task
- Catch issues before they compound
- Fix before moving to next task

**Executing Plans:**
- Review after each batch (3 tasks)
- Get feedback, apply, continue

**Ad-Hoc Development:**
- Review before merge
- Review when stuck

Companion skill:
- `superpowers-code-review` - Reviewer protocol and output format
- `superpowers-receiving-code-review` - Apply feedback correctly

## Red Flags

**Never:**
- Skip review because "it's simple"
- Ignore Critical issues
- Proceed with unfixed Important issues
- Argue with valid technical feedback

**If reviewer wrong:**
- Push back with technical reasoning
- Show code/tests that prove it works
- Request clarification

Template path:
- `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
