---
name: superpowers-using-superpowers
description: Use when starting any conversation in this workspace. Enforce skills-first workflow, load relevant skills before acting, and apply explicit mappings/fallbacks when capabilities differ.
---

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. This is not optional. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## How to Access Skills

**For Codex:** Use the available skills list (provided in-session) to select the right skill.

**In other environments:** Check your platform's documentation for how skills are loaded.

# Using Skills

## The Rule

**Invoke relevant or requested skills BEFORE any response or action.** Even a 1% chance a skill might apply means that you should invoke the skill to check. If an invoked skill turns out to be wrong for the situation, you don't need to use it.

## Required Declaration

Before starting task execution, write one line:

`Skills used: <...>. Mappings/fallbacks: <...>.`

```dot
digraph skill_flow {
    "User message received" [shape=doublecircle];
    "Might any skill apply?" [shape=diamond];
    "Select skill from in-session list" [shape=box];
    "Announce/declare: Skills used: <...>. Mappings/fallbacks: <...>. Using [skill] to [purpose]." [shape=box];
    "Has checklist?" [shape=diamond];
    "Create update_plan todo per item" [shape=box];
    "Follow skill exactly" [shape=box];
    "Respond (including clarifications)" [shape=doublecircle];

    "User message received" -> "Might any skill apply?";
    "Might any skill apply?" -> "Select skill from in-session list" [label="yes, even 1%"];
    "Might any skill apply?" -> "Respond (including clarifications)" [label="definitely not"];
    "Select skill from in-session list" -> "Announce/declare: Skills used: <...>. Mappings/fallbacks: <...>. Using [skill] to [purpose].";
    "Announce/declare: Skills used: <...>. Mappings/fallbacks: <...>. Using [skill] to [purpose]." -> "Has checklist?";
    "Has checklist?" -> "Create update_plan todo per item" [label="yes"];
    "Has checklist?" -> "Follow skill exactly" [label="no"];
    "Create update_plan todo per item" -> "Follow skill exactly";
}
```

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Skill Priority

When multiple skills could apply, use this order:

1. **Process skills first** (superpowers-brainstorming, superpowers-writing-plans, superpowers-systematic-debugging) - these determine HOW to approach the task
2. **Implementation skills second** (superpowers-executing-plans, superpowers-test-driven-development, superpowers-verification-before-completion, superpowers-using-git-worktrees) - these guide execution

"Let's build X" → superpowers-brainstorming first, then implementation skills.
"Fix this bug" → debugging first, then domain-specific skills.
"Need an independent review" → `superpowers-requesting-code-review`, then run `superpowers-code-review` in a new reviewer thread, then `superpowers-receiving-code-review`.
"Request code review" in implementer thread → `superpowers-requesting-code-review`.
"Review this diff/branch" in reviewer thread → `superpowers-code-review`.

## Skill Types

**Rigid** (TDD, debugging): Follow exactly. Don't adapt away discipline.

**Flexible** (patterns): Adapt principles to context.

The skill itself tells you which.

## User Instructions

Instructions say WHAT, not HOW. "Add X" or "Fix Y" doesn't mean skip workflows.
