---
name: superpowers-receiving-code-review
description: Use when receiving review feedback before implementing suggestions (e.g., PR comments, inline notes, batch review findings), especially when feedback is unclear or technically questionable.
---

# Receiving Code Review

## Overview

Code review requires technical evaluation, not performative agreement.

**Core principle:** Verify before implementing. Technical correctness over social comfort.

## Response Pattern

When receiving feedback:

1. **Read** all items fully.
2. **Understand** each requirement (or ask clarifying questions).
3. **Verify** against actual codebase behavior.
4. **Evaluate** technical soundness for this repository.
5. **Respond** with concrete action or reasoned pushback.
6. **Implement** one item at a time with verification.

## Forbidden Responses

Never:
- "You're absolutely right!"
- performative praise instead of technical evaluation
- blind implementation before verification

Instead:
- Restate technical requirement
- Ask specific clarifying questions
- Implement directly and show evidence
- Push back with technical reasoning when needed

## Handling Unclear Feedback

If any item is unclear:
- Stop and clarify before implementing anything.
- Do not implement only the parts you understand if ambiguity could affect scope/correctness.

## Source-Specific Handling

### Feedback from Felix

- Treat as high-priority direction.
- Still clarify scope when ambiguous.
- Move quickly to concrete implementation.

### Feedback from external reviewers/tools

Before implementing, verify:
- Is it technically correct for this codebase?
- Does it break existing behavior?
- Is there context the reviewer might be missing?
- Does it conflict with explicit Felix decisions?

If conflict exists, stop and discuss with Felix.

## YAGNI Gate

If feedback suggests adding "professional" extras:
1. Check real usage in codebase.
2. If unused, propose removal/defer instead of adding complexity.
3. If used, implement the smallest correct change.

## Implementation Order

1. Blocking defects (crashes, security, correctness)
2. Simple correctness fixes
3. Complex structural changes

Verify each item after implementation.

## Pushback Rules

Push back when suggestion:
- breaks working behavior
- violates constraints or architecture
- adds unjustified complexity
- is not applicable to this stack

Push back with evidence, not tone.

## Acknowledge Correct Feedback

Use factual acknowledgment:
- "Fixed: <what changed>."
- "Verified and updated: <what changed>."

Keep it brief and technical.

## Bottom Line

Review feedback is input to evaluate, not instructions to execute blindly.
