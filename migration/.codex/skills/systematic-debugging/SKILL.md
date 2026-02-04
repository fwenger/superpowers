---
name: superpowers-systematic-debugging
description: Use when encountering any bug, failing test, or unexpected behavior. Enforce root-cause investigation before fixes, hypothesis-driven testing, and verified remediation.
---

# Systematic Debugging

## Overview

Random fixes waste time and create new bugs.

**Core principle:** ALWAYS find root cause before proposing or implementing fixes.

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

## Four Phases

### Phase 1: Root Cause Investigation

Before any fix:
1. Read error messages and stack traces fully.
2. Reproduce consistently.
3. Check recent changes (code, config, dependencies, environment).
4. Gather evidence across component boundaries.
5. Trace data flow backward to source.

### Phase 2: Pattern Analysis

1. Find similar working examples.
2. Compare broken vs working behavior.
3. List meaningful differences.
4. Confirm hidden dependencies and assumptions.

### Phase 3: Hypothesis and Testing

1. State one specific hypothesis.
2. Run the smallest test to validate it.
3. Verify outcome before continuing.
4. If wrong, form a new hypothesis (do not stack random fixes).

### Phase 4: Implementation

1. Create a failing reproduction test (use `superpowers-test-driven-development`).
2. Implement one root-cause fix.
3. Verify original issue and regression coverage.
4. If multiple attempts fail, stop and reassess architecture with Felix.

## Red Flags

Stop and return to Phase 1 if you catch:
- "quick fix now, investigate later"
- "let me just try this"
- multiple simultaneous fixes
- proposing solutions before evidence is complete

## Related Skills

- `superpowers-test-driven-development`
- `superpowers-verification-before-completion`
