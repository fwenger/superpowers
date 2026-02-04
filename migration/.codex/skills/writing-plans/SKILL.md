---
name: superpowers-writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code. Produce a decision-complete, executable plan with small tasks, exact file paths, verifications, and checkpoints.
---

# Writing Plans

## Overview

Write implementation plans assuming the implementer has little context and needs exact guidance. Provide exact file paths, code targets, validation commands, and acceptance criteria. Keep tasks bite-sized. Apply DRY, YAGNI, and verification discipline.

**Announce at start:** "I'm using the superpowers-writing-plans skill to create the implementation plan."

**Save plans to:** `migration/docs/plans/YYYY-MM-DD-<feature-name>.md`

## Bite-Sized Task Granularity

Each step should be one action (2-5 minutes):
- Write failing test
- Run it to confirm failure
- Implement minimum code
- Re-run tests
- Commit/checkpoint

## Plan Document Header

Every plan starts with:

```markdown
# [Feature Name] Implementation Plan

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

## Task Structure

```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

**Step 1: Write the failing test**
[exact test snippet]

**Step 2: Run test to verify it fails**
Run: `[exact command]`
Expected: [specific failure]

**Step 3: Write minimal implementation**
[exact implementation snippet]

**Step 4: Run test to verify it passes**
Run: `[exact command]`
Expected: [specific pass result]

**Step 5: Checkpoint**
[exact command(s)]
```

## Plan Requirements

- Exact file paths always
- Complete code targets (not vague instructions)
- Exact commands with expected output
- Explicit failure modes and rollback notes when needed
- Verification after every meaningful step

## Execution Handoff

After saving the plan, offer execution modes:

1. **Sequential execution (this session)** - execute first 3 tasks, report results, wait for feedback.
2. **Sequential execution (separate session)** - load the same plan and execute in the same batched checkpoint style.

For both modes: do not skip verifications, and stop immediately when blocked.
