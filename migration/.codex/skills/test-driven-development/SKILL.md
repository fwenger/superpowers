---
name: superpowers-test-driven-development
description: Use when implementing any feature or bugfix, before writing implementation code. Enforce failing-test-first RED-GREEN-REFACTOR workflow with explicit verification at each phase.
---

# Test-Driven Development (TDD)

## Overview

Write the test first. Watch it fail. Write minimal code to pass.

**Core principle:** If you didn't watch the test fail, you don't know if it tests the right thing.

## The Iron Law

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

Write code before the test? Delete it and start over.

## Red-Green-Refactor

### RED - Write Failing Test

Write one minimal test for one behavior with a clear name.

### Verify RED - Watch It Fail

Run the test and confirm:
- It fails (not errors)
- The failure is expected
- It fails for missing behavior, not typos

### GREEN - Minimal Code

Write the smallest implementation that makes the failing test pass.
Do not add unrelated features.

### Verify GREEN - Watch It Pass

Re-run tests and confirm:
- New test passes
- Relevant suite still passes
- Output is clean

### REFACTOR - Clean Up

Refactor only after green:
- Reduce duplication
- Improve naming
- Keep behavior unchanged

## Rationalization Checks

- "Too simple to test" -> Test it anyway.
- "I'll add tests after" -> Not TDD.
- "Manual testing is enough" -> Not reproducible.
- "I already wrote the code" -> Delete and restart from RED.
