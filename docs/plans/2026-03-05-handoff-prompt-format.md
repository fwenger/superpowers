# Handoff Prompt Format Implementation Plan

> **For Codex:** REQUIRED SUB-SKILL: Use superpowers-executing-plans to implement this plan task-by-task.

**Goal:** Standardize migrated reviewer and parallel-session implementer handoff outputs to use one fenced code block with fully filled prompts and no reviewer heading in prompt body.

**Architecture:** Keep changes doc-only and template-only inside migrated skills. Update prompt templates and their governing skill instructions so output behavior is explicit, consistent, and verifiable via repository text checks.

**Tech Stack:** Markdown skills/docs, git, ripgrep

---

### Task 1: Remove Reviewer Heading from Prompt Body

**Files:**
- Modify: `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
- Verify: `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`

**Step 1: Write the failing verification check**

Run: `rg -n "^# Reviewer Prompt$" migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
Expected: one match (current state violates desired output contract)

**Step 2: Edit prompt template to match desired output**

Update file to remove heading and keep only prompt body content.

Target content opening should be:

```markdown
You are the reviewer agent. Use the skill superpowers-code-review. Review these completed changes for production readiness.

**Your task:**
1. Review `{WHAT_WAS_IMPLEMENTED}`
2. Compare against `{PLAN_OR_REQUIREMENTS}`
```

**Step 3: Run verification check for passing state**

Run: `rg -n "^# Reviewer Prompt$" migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
Expected: no matches

**Step 4: Commit**

```bash
git add migration/.codex/skills/requesting-code-review/reviewer-prompt.md
git commit -m "docs(skills): remove reviewer prompt heading from handoff template"
```

### Task 2: Enforce Fenced-Block Output Rules in Requesting-Code-Review Skill

**Files:**
- Modify: `migration/.codex/skills/requesting-code-review/SKILL.md`
- Verify: `migration/.codex/skills/requesting-code-review/SKILL.md`

**Step 1: Write failing verification checks**

Run:
- `rg -n "Do not wrap the entire prompt in an outer triple-backtick code fence" migration/.codex/skills/requesting-code-review/SKILL.md`
- `rg -n "If you must wrap the entire prompt in a code fence, use four backticks" migration/.codex/skills/requesting-code-review/SKILL.md`
Expected: matches found (old guidance conflicts with new fenced-block decision)

**Step 2: Implement minimal instruction update**

In section "2.5 Present the filled prompt to Felix to copy/paste into a new thread", replace conflicting fence guidance with explicit rules:
- Present the fully filled prompt in exactly one fenced code block.
- Ensure no unresolved placeholders remain.
- Optional context text may appear outside the fenced block.

**Step 3: Verify updated rules are present and old rules removed**

Run:
- `rg -n "exactly one fenced code block|fully filled|no unresolved placeholders" migration/.codex/skills/requesting-code-review/SKILL.md`
- `rg -n "Do not wrap the entire prompt|four backticks" migration/.codex/skills/requesting-code-review/SKILL.md`
Expected:
- first command finds expected new guidance
- second command returns no matches

**Step 4: Commit**

```bash
git add migration/.codex/skills/requesting-code-review/SKILL.md
git commit -m "docs(skills): require single fenced reviewer handoff block"
```

### Task 3: Add Reusable Parallel-Session Implementer Prompt Template

**Files:**
- Create: `migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
- Verify: `migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`

**Step 1: Write failing verification check**

Run: `test -f migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
Expected: command exits non-zero (file does not exist yet)

**Step 2: Add minimal complete template**

Create a template that includes placeholders for required context and mandates `superpowers-executing-plans`.

Template must contain these fields verbatim as section labels:
- `Required skill`
- `Design document`
- `Implementation plan`
- `Branch`
- `Worktree`
- `Relevant commits`

Template body must instruct implementer to execute plan tasks with `superpowers-executing-plans`.

**Step 3: Verify required fields exist in template**

Run:
- `rg -n "^Required skill|^Design document|^Implementation plan|^Branch|^Worktree|^Relevant commits" migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
- `rg -n "superpowers-executing-plans" migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
Expected: all required markers and skill reference found

**Step 4: Commit**

```bash
git add migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md
git commit -m "docs(skills): add parallel-session implementer handoff template"
```

### Task 4: Wire Writing-Plans Handoff Contract to New Template

**Files:**
- Modify: `migration/.codex/skills/writing-plans/SKILL.md`
- Verify: `migration/.codex/skills/writing-plans/SKILL.md`

**Step 1: Write failing verification checks**

Run:
- `rg -n "parallel-session-implementer-prompt\.md" migration/.codex/skills/writing-plans/SKILL.md`
- `rg -n "fenced code block|fully filled" migration/.codex/skills/writing-plans/SKILL.md`
Expected: no matches for new template-specific/output-contract text (current state incomplete)

**Step 2: Implement handoff instructions**

In "Execution Handoff" section, keep existing capability gate and add explicit parallel-session output requirements:
- Output one fenced code block containing the fully filled implementer prompt.
- Use `parallel-session-implementer-prompt.md` as source template.
- Require inclusion of design document path, plan path, branch, worktree, and relevant commits.
- Require explicit instruction to use `superpowers-executing-plans`.

**Step 3: Verify final instructions**

Run:
- `rg -n "parallel-session-implementer-prompt\.md|one fenced code block|fully filled|design document path|plan path|branch|worktree|relevant commits|superpowers-executing-plans" migration/.codex/skills/writing-plans/SKILL.md`
Expected: all new requirements present

**Step 4: Commit**

```bash
git add migration/.codex/skills/writing-plans/SKILL.md
git commit -m "docs(skills): define parallel handoff prompt output contract"
```

### Task 5: Cross-File Consistency Verification

**Files:**
- Verify: `migration/.codex/skills/requesting-code-review/SKILL.md`
- Verify: `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
- Verify: `migration/.codex/skills/writing-plans/SKILL.md`
- Verify: `migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`

**Step 1: Run consistency checks**

Run:
- `rg -n "# Reviewer Prompt" migration/.codex/skills/requesting-code-review/reviewer-prompt.md`
- `rg -n "Do not wrap the entire prompt|four backticks" migration/.codex/skills/requesting-code-review/SKILL.md`
- `rg -n "one fenced code block|fully filled" migration/.codex/skills/requesting-code-review/SKILL.md migration/.codex/skills/writing-plans/SKILL.md`
- `rg -n "superpowers-executing-plans|Design document|Implementation plan|Branch|Worktree|Relevant commits" migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md`
Expected:
- no outdated reviewer heading/fence-conflict guidance
- new fenced-block rules present in both skill docs
- implementer template contains all required fields and skill reference

**Step 2: Review diff scope**

Run: `git diff --stat HEAD~4..HEAD`
Expected: only migrated skill files for this feature and intended docs/template edits

**Step 3: Commit final touch-ups if needed**

```bash
git add migration/.codex/skills/requesting-code-review/SKILL.md \
        migration/.codex/skills/requesting-code-review/reviewer-prompt.md \
        migration/.codex/skills/writing-plans/SKILL.md \
        migration/.codex/skills/writing-plans/parallel-session-implementer-prompt.md
git commit -m "docs(skills): align reviewer and implementer handoff prompt formats"
```

Skip this commit if there are no remaining unstaged changes.

## Notes for Executor

- Use `@superpowers-executing-plans` as required by this plan header.
- Keep scope strictly to migrated skills under `migration/.codex/skills/`.
- Do not modify non-migrated copies under `skills/`.
