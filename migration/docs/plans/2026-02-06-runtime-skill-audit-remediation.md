# Runtime Skill Audit Remediation Plan

**Date:** 2026-02-06  
**Workspace:** `migration/`  
**Scope:** Runtime `SKILL.md` normalization and `README.md` updates only

---

## Summary

Apply a focused remediation pass for migrated runtime skills:

1. Save this plan artifact first.
2. Normalize runtime naming and legacy references in `SKILL.md` files.
3. Set default worktree location to `~/.worktrees/<repo>/<branch>` when no local worktree directory exists.
4. Update migration README to document behavior and scope boundaries.

---

## Chosen Default

- Default worktree location for new setups: `~/.worktrees/<repo>/<branch>`
- Precedence remains:
  - Existing `.worktrees/` wins
  - Existing `worktrees/` is second
  - Then instruction-file preference
  - Then fallback default `~/.worktrees/<repo>/<branch>`

---

## Task List

### Task 1: Save plan artifact

- Create this file at:
  - `migration/docs/plans/2026-02-06-runtime-skill-audit-remediation.md`

### Task 2: Patch primary worktree skill

File:
- `migration/.codex/skills/using-git-worktrees/SKILL.md`

Changes:
- Canonicalize announce text to `superpowers-using-git-worktrees`
- Replace `CLAUDE.md` references with workspace instruction wording
- Remove personal references and legacy path examples
- Default new global location to `~/.worktrees/<project-name>/`
- Normalize integration references to canonical `superpowers-*` names

### Task 3: Normalize runtime naming consistency

Files:
- `migration/.codex/skills/executing-plans/SKILL.md`
- `migration/.codex/skills/finishing-a-development-branch/SKILL.md`
- `migration/.codex/skills/writing-plans/SKILL.md`
- `migration/.codex/skills/using-superpowers/SKILL.md`
- `migration/.codex/skills/subagent-driven-development/SKILL.md`
- `migration/.codex/skills/receiving-code-review/SKILL.md`
- `migration/.codex/skills/writing-skills/SKILL.md`

Changes:
- Canonicalize announce lines and integration references to `superpowers-*`
- Replace `CLAUDE.md` wording in runtime guidance where needed
- Preserve capability gates and behavior

### Task 4: Update migration README

File:
- `migration/README.md`

Changes:
- Document `~/.worktrees/<repo>/<branch>` default
- Document precedence for existing repo-local worktree dirs
- Document scope boundary: runtime `SKILL.md` normalized; support/reference files may still contain archival legacy terms
- Canonicalize any skill-name references to `superpowers-*`

### Task 5: Final read-only audit

Run checks for:
- Legacy runtime markers (`CLAUDE.md`, personal references, hardcoded old user paths)
- Non-canonical runtime skill naming
- Diff scope limited to planned files

---

## Validation Commands

```bash
test -f /Users/felix/src/superpowers/migration/docs/plans/2026-02-06-runtime-skill-audit-remediation.md

grep -nE "CLAUDE\\.md|Per Jesse|/Users/jesse" /Users/felix/src/superpowers/migration/.codex/skills/using-git-worktrees/SKILL.md
grep -n "~/.worktrees" /Users/felix/src/superpowers/migration/.codex/skills/using-git-worktrees/SKILL.md
grep -nE "\\*\\*brainstorming\\*\\*|\\*\\*executing-plans\\*\\*|\\*\\*finishing-a-development-branch\\*\\*|\\*\\*subagent-driven-development\\*\\*" /Users/felix/src/superpowers/migration/.codex/skills/using-git-worktrees/SKILL.md

grep -R -nE "I'm using the (writing-plans|executing-plans|finishing-a-development-branch|using-git-worktrees) skill" /Users/felix/src/superpowers/migration/.codex/skills/*/SKILL.md
grep -R -nE "\\*\\*(brainstorming|executing-plans|finishing-a-development-branch|using-git-worktrees|subagent-driven-development)\\*\\*" /Users/felix/src/superpowers/migration/.codex/skills/*/SKILL.md
grep -R -n "CLAUDE\\.md" /Users/felix/src/superpowers/migration/.codex/skills/*/SKILL.md

grep -nE "~/.worktrees|superpowers-using-git-worktrees|runtime SKILL\\.md|support/reference" /Users/felix/src/superpowers/migration/README.md

git -C /Users/felix/src/superpowers diff -- /Users/felix/src/superpowers/migration/.codex/skills /Users/felix/src/superpowers/migration/README.md /Users/felix/src/superpowers/migration/docs/plans
```

---

## Scope Boundary

- This pass targets runtime behavior and naming in `SKILL.md` files.
- Support/reference artifacts are deferred unless explicitly requested:
  - `CREATION-LOG.md`
  - examples and research references
  - helper scripts and imported external notes

