---
name: superpowers-verification-before-completion
description: Use before claiming work is complete, fixed, or passing (e.g., handoff, commit, PR, merge). Require fresh verification evidence from explicit commands and outputs before any success claim.
---

# Verification Before Completion

## Overview

Claiming completion without verification is unacceptable.

**Core principle:** Evidence before claims, always.

## The Iron Law

```
NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
```

## Gate Function

Before any success claim:

1. IDENTIFY: which command proves the claim
2. RUN: execute the full command now
3. READ: inspect output and exit code
4. VERIFY: confirm output supports the claim
5. ONLY THEN: state the claim with evidence

## Common Failure Patterns

- "should pass" without running tests
- relying on stale output
- partial verification and broad claim
- trusting agent/tool report without independent confirmation

## Required Verification Patterns

- **Tests pass** -> run test command, report pass/fail counts
- **Build passes** -> run build command, report exit code and key output
- **Bug fixed** -> run reproduction path and regression check
- **Requirements met** -> checklist each requirement explicitly

## Red Flags

Stop if you are about to say:
- done
- fixed
- complete
- works now

without fresh command evidence in the current message.
