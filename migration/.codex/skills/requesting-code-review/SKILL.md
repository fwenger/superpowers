---
name: superpowers-requesting-code-review
description: Use when completing major tasks or before merge to verify implementation quality (e.g., end of execution batch, major feature completion, pre-PR readiness checks).
---

# Requesting Code Review

## Overview

Request structured review early so defects are caught before they compound.

**Core principle:** Review early, review often.

## When to Request Review

Mandatory:
- After each implementation batch in `superpowers-executing-plans`
- After major feature completion
- Before merge or PR finalization

Optional but useful:
- When stuck on design/quality tradeoffs
- Before large refactors
- After complex bug fixes

## Review Request Procedure

### 1) Define review scope

Capture commit range and requirements:

```bash
BASE_SHA=$(git rev-parse HEAD~1)
HEAD_SHA=$(git rev-parse HEAD)
```

Record:
- What was implemented
- Which requirements/plan items this should satisfy
- Any known risks

### 2) Run review mode

Use the strongest available mode:

1. **Delegated review** (if verified capability exists): assign a dedicated reviewer agent to inspect the commit range.
2. **Direct review** (fallback): perform a strict self-review pass using the checklist below.

### 3) Apply review checklist

For the selected range, check:
- Requirement/spec compliance
- Behavioral regressions
- Missing or weak tests
- Error handling and edge cases
- Security/privacy risks
- Performance footguns
- Maintainability/readability

### 4) Classify findings

- **Critical**: must fix now
- **Important**: fix before continuing
- **Minor**: track for later if not blocking

### 5) Act and report

- Fix Critical and Important items before proceeding.
- For disputed feedback, push back with technical reasoning and evidence.
- Report concise outcome and readiness state.

## Output Template

Use this structure:

```text
Review scope: <BASE_SHA>..<HEAD_SHA>
Requirements checked: <plan section or requirement list>
Findings:
- Critical: <count>
- Important: <count>
- Minor: <count>
Actions taken:
- <fixes applied or rationale for deferral>
Status: <ready / blocked>
```

## Red Flags

Never:
- Skip review because change "looks simple"
- Ignore Critical findings
- Continue with unresolved Important findings
- Accept questionable feedback without verification

## Integration

- Used by `superpowers-executing-plans` after each batch checkpoint
- Pairs with `superpowers-receiving-code-review` for handling feedback rigorously
