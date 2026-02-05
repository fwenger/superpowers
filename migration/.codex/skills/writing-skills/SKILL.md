---
name: superpowers-writing-skills
description: Use when creating or editing skill definitions (e.g., new SKILL.md files, trigger/description tuning, migration of legacy skills, pre-deployment skill validation).
---

# Writing Skills

## Overview

Write and improve skills with discipline: validate trigger quality, keep instructions concise, and verify the skill works before treating it as ready.

**Core principle:** Skill writing follows test-driven thinking: baseline behavior, targeted instructions, validation, iteration.

## Process

### Step 1: Define trigger intent

Clarify:
- What user request should trigger this skill?
- What similar requests should not trigger it?

### Step 2: Draft frontmatter correctly

Frontmatter requirements:
- `name`: lowercase letters, digits, hyphens only (max 64 chars)
- `description`: starts with `Use when`/`Use before`, focused on trigger conditions
- Avoid workflow summaries in description

### Step 3: Write focused body guidance

- Keep high-signal instructions
- Prefer concrete checklists and decision rules
- Remove generic filler
- Add examples only when they reduce ambiguity

### Step 4: Validate and audit

Run basic checks:

```bash
# Name and description quality checks
# (project-local grep/python checks are acceptable)
```

If available, run formal validator:

```bash
python3 /Users/felix/.codex/skills/.system/skill-creator/scripts/quick_validate.py <skill-dir>
```

### Step 5: Iterate from observed failures

When testing a skill reveals misses:
1. Capture failure pattern
2. Add minimal instruction to close the gap
3. Re-check trigger clarity and brevity

## Skill Quality Checklist

- Trigger phrasing is explicit and specific
- Name is validator-safe
- Description is trigger-focused, not process summary
- Body is actionable and concise
- References/cross-skill links are consistent
- Validation checks are recorded

## Red Flags

Never:
- Use invalid names (`:`/spaces/special chars)
- Write vague descriptions ("for coding" / "for quality")
- Add long narrative history or motivational prose
- Skip validation before claiming readiness

## Integration

- Supports migration and maintenance of all `superpowers-*` skills
- Pairs with `superpowers-requesting-code-review` for final review before rollout
