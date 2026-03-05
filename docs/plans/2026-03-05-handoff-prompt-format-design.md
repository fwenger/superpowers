# Handoff Prompt Format Design

**Date:** 2026-03-05
**Author:** Codex & Felix
**Status:** Approved

## Overview

Standardize migrated skill handoff outputs so reviewer and implementer prompts are easier to copy and reuse across Codex Mac app, VSCode, and terminal workflows.

## Problem Statement

Current handoff responses sometimes include extra text around prompt content that is meant for Felix, not the receiving reviewer/implementer agent. This creates friction when copying prompts into a new thread.

Two concrete issues:
- Reviewer handoff prompt still includes `# Reviewer Prompt` heading in template output.
- Writing-plans parallel handoff lacks a consistent, copyable implementer prompt format.

## Goals

- Keep prompt content clean and directly reusable in another agent conversation.
- Use fenced code blocks for handoff prompts (v1) so output is visually bounded and easy to copy.
- Remove `# Reviewer Prompt` heading from the actual reviewer prompt body.
- Add a consistent implementer handoff prompt template for writing-plans parallel-session flow.
- Ensure all required execution metadata is present in implementer handoff output.

## Non-Goals

- No app-specific UI changes (copy buttons, custom renderer behavior).
- No changes to non-migrated skill copies under `skills/`.

## Evaluated Approaches

### Approach 1: Strict Prompt-Only (No Surrounding Text)

Output contains only the filled prompt text with no extra lines.

- Pros: Lowest risk of copy noise.
- Cons: Less readable status messaging in chat.

### Approach 2: Prompt with Marker Lines

Wrap prompt with explicit markers like `BEGIN PROMPT` / `END PROMPT`.

- Pros: Clear visual boundaries.
- Cons: Marker lines are copied and require cleanup.

### Approach 3: Single Fenced Code Block (Chosen for v1)

Output prompt inside one fenced code block. Allow optional explanatory text outside the block.

- Pros: Clear visual boundaries and simple copy interaction in current workflow.
- Cons: Some clients may include fence markup when copying.

**Decision:** Implement Approach 3 first. If real usage shows friction, switch to Approach 1.

## Approved Output Contract

### Requesting Code Review

- Filled reviewer prompt is emitted in exactly one fenced code block.
- Prompt body must not include `# Reviewer Prompt`.
- Prompt must be fully filled (no unresolved placeholders).
- Optional context text outside the code block is allowed.

### Writing Plans (Parallel Session Handoff)

- When delegation/subagent capability is unverified, continue offering only parallel session.
- Include one fenced code block containing the fully filled implementer handoff prompt.
- Implementer prompt must include:
  - Explicit instruction to use `superpowers-executing-plans`
  - Design document path
  - Implementation plan path
  - Branch
  - Worktree
  - Relevant commits

## File-Level Design

### Files to Modify

- `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
  - Remove heading line and keep only prompt body.

- `migration/.codex/skills/requesting-code-review/SKILL.md`
  - Update handoff formatting instructions to require one fenced code block.
  - Require fully filled values (no placeholders).
  - Remove contradictory guidance about avoiding outer fences.

- `migration/.codex/skills/writing-plans/SKILL.md`
  - Extend execution handoff section with required implementer prompt output format.
  - Require one fenced code block with complete parallel-session handoff prompt.

### File to Add

- `migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
  - Reusable template for parallel-session implementer handoff.
  - Contains placeholders for required metadata fields.

## Data Flow

1. Skill gathers handoff context values (requirements, SHAs, doc paths, branch/worktree, commits).
2. Skill fills placeholders in corresponding prompt template.
3. Skill emits exactly one fenced code block containing the filled prompt.

## Error Handling Rules

- If required metadata is missing, resolve it via local git/filesystem commands before output.
- Do not output partially filled placeholders in final handoff prompt.
- If a required field cannot be determined, state the missing field explicitly and stop before declaring handoff complete.

## Verification Strategy

- Reviewer handoff check:
  - Output contains one fenced code block.
  - Prompt body has no `# Reviewer Prompt` heading.
  - No unresolved placeholders remain.

- Writing-plans handoff check:
  - Output contains one fenced code block.
  - Includes all required fields (executing-plans note, design path, plan path, branch, worktree, commits).
  - No unresolved placeholders remain.

- Manual acceptance check:
  - Copy output from Codex app and paste into a new thread.
  - Verify prompt is directly usable with no structural edits.

## Rollout and Fallback

- Rollout scope is migrated skills only.
- If fenced block copy behavior causes friction, switch to strict prompt-only output (Approach 1) in a follow-up change.
