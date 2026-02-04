---
name: superpowers-brainstorming
description: Use when starting creative work that creates or changes behavior (e.g., new features, behavior changes, architecture/design changes). Clarify intent and constraints, explore alternatives, and produce a validated design before implementation.
---

# Brainstorming Ideas Into Designs

## Overview

Turn ideas into fully formed designs and specs through collaborative dialogue.

Start by understanding the current project context, then ask questions one at a time to refine the idea. Once the design is clear, present it in small sections (200-300 words), validating each section before moving on.

## The Process

**Understanding the idea:**
- Check project state first (files, docs, recent commits)
- Ask one question at a time
- Prefer multiple choice when useful
- Focus on purpose, constraints, and success criteria

**Exploring approaches:**
- Propose 2-3 approaches with trade-offs
- Lead with your recommendation and why

**Presenting the design:**
- Present in sections of 200-300 words
- Validate each section before continuing
- Cover architecture, components, data flow, error handling, testing

## After the Design

**Documentation:**
- Write the validated design to `migration/docs/plans/YYYY-MM-DD-<topic>-design.md`

**Implementation setup:**
- Ask: "Ready to write the implementation plan?"
- Use the `superpowers-writing-plans` skill to create a decision-complete execution plan

## Key Principles

- One question at a time
- Multiple choice preferred when it reduces ambiguity
- YAGNI ruthlessly
- Explore alternatives before committing
- Validate incrementally
