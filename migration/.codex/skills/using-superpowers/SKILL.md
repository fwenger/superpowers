---
name: superpowers-using-superpowers
description: Use when starting any conversation in this migration workspace. Enforce skills-first workflow, load relevant Codex-native skills before acting, and apply explicit mappings/fallbacks when capabilities differ.
---

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply, you MUST load and use it.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.
</EXTREMELY-IMPORTANT>

# Using Skills

## The Rule

Invoke relevant or requested skills BEFORE any response or action.

## How to Load Skills in This Workspace

- Prefer Codex native skill selection/invocation from the workspace skill set.
- Primary migration skill location: `migration/.codex/skills/`.
- If a skill cannot be loaded, state the blocker and use the closest reproducible fallback.

## Required One-Line Declaration

Before starting work, write:

`Skills: <...>. Mappings/fallbacks: <...>.`

## Checklist Tracking

If a loaded skill contains checklist-style steps, track them explicitly with `update_plan`.

## Skill Priority

When multiple skills could apply, use this order:

1. Process skills first (superpowers-brainstorming, superpowers-systematic-debugging)
2. Implementation skills second (superpowers-writing-plans, superpowers-executing-plans, superpowers-using-git-worktrees, superpowers-test-driven-development, superpowers-verification-before-completion)
3. Review skills as checkpoint gates (superpowers-requesting-code-review, superpowers-receiving-code-review)

"Let's build X" -> superpowers-brainstorming first, then superpowers-writing-plans and implementation skills.
"Fix this bug" -> superpowers-systematic-debugging first, then superpowers-test-driven-development and superpowers-verification-before-completion.

## Red Flags

These thoughts mean STOP and load skills first:

- "This is just a simple question"
- "I need context first"
- "I'll do one quick thing before loading a skill"
- "I remember the skill already"
- "This doesn't need a formal skill"

## Non-Negotiable

User instructions define WHAT to do.
Skills define HOW to do it.
