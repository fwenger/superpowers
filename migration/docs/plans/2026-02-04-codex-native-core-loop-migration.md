# Codex-Native Core Loop Skills Migration Plan

**Date:** 2026-02-04
**Workspace:** `migration/`
**Scope:** Migration-only assets for Codex-native workflow.

---

## Goal

Build an isolated migration workspace under `migration/` that contains:
1. Codex-native core-loop skills
2. A Codex-native meta skill named `superpowers-using-superpowers`
3. Side-by-side original and amended AGENTS files

Keep legacy fork assets unchanged.

---

## Public Interface Changes

### New migration-local skill entrypoints
- `migration/.codex/skills/using-superpowers/SKILL.md`
- `migration/.codex/skills/brainstorming/SKILL.md`
- `migration/.codex/skills/writing-plans/SKILL.md`
- `migration/.codex/skills/test-driven-development/SKILL.md`
- `migration/.codex/skills/systematic-debugging/SKILL.md`
- `migration/.codex/skills/verification-before-completion/SKILL.md`

### New migration-local AGENTS contract
- `migration/AGENTS.original.md` (snapshot)
- `migration/AGENTS.md` (Codex-native top sections)

---

## Implementation Tasks

### Task 1: Create migration scaffold
- Create `migration/.codex/skills/`
- Create `migration/docs/plans/`
- Verify with `find migration -maxdepth 4 -type d | sort`

### Task 2: Snapshot original AGENTS
- Copy root `AGENTS.md` to `migration/AGENTS.original.md`
- Verify with `cmp -s AGENTS.md migration/AGENTS.original.md && echo "match"`

### Task 3: Create amended migration AGENTS
- Start from original snapshot
- Rewrite only pre-`# Intro` workflow/bootstrap sections to:
  - remove bootstrap wrapper dependency
  - require native workspace skills in `migration/.codex/skills`
  - preserve compatibility mapping protocol and one-line declaration format
- Keep policy sections from `# Intro` onward functionally unchanged

### Task 4: Create `superpowers-using-superpowers` meta skill
- Preserve strict guardrail intent
- Remove Claude-specific tool assumptions
- Preserve skills-first routing and priority logic

### Task 5: Create `superpowers-brainstorming` skill
- Preserve one-question-at-a-time design refinement
- Use native local references (no namespaced legacy references)
- Keep YAGNI and staged validation

### Task 6: Create `superpowers-writing-plans` skill
- Preserve bite-sized, executable task structure
- Remove dependency on non-migrated execution/subagent skills
- Define sequential checkpoint-based execution handoff

### Task 7: Create `superpowers-test-driven-development` skill
- Preserve failing-test-first RED/GREEN/REFACTOR discipline
- Keep strict anti-rationalization framing

### Task 8: Create `superpowers-systematic-debugging` skill
- Preserve 4-phase root-cause method
- Update related-skill references to migrated names
- Keep 3+ failed-fix architectural stop rule

### Task 9: Create `superpowers-verification-before-completion` skill
- Preserve evidence gate and iron law
- Keep strict claim-validation requirements

### Task 10: Consistency pass
- Normalize names/references across all migration skill files and AGENTS
- Ensure no wrapper bootstrap dependency remains in migration files

### Task 11: Save migration plan artifact
- Save this document at:
  - `migration/docs/plans/2026-02-04-codex-native-core-loop-migration.md`

---

## Validation Checklist

Run:

```bash
find migration -maxdepth 4 -type d | sort
cmp -s AGENTS.md migration/AGENTS.original.md && echo "match"
grep -n "superpowers-codex bootstrap" migration/AGENTS.md
grep -n "^# Intro" migration/AGENTS.md
grep -n "Skill tool\|TodoWrite\|In Claude Code\|Read tool" migration/.codex/skills/using-superpowers/SKILL.md
grep -n "superpowers:" migration/.codex/skills/brainstorming/SKILL.md || true
grep -n "executing-plans\|subagent-driven-development\|superpowers:" migration/.codex/skills/writing-plans/SKILL.md || true
grep -n "superpowers-test-driven-development\|superpowers-verification-before-completion" migration/.codex/skills/systematic-debugging/SKILL.md
grep -R --line-number "superpowers-codex\|~/.codex/superpowers\|Skill tool\|TodoWrite" migration
```

---

## Scenario Checks

1. Feature flow: `superpowers-using-superpowers` -> `superpowers-brainstorming` -> `superpowers-writing-plans` -> `superpowers-test-driven-development` -> `superpowers-verification-before-completion`
2. Bug flow: `superpowers-using-superpowers` -> `superpowers-systematic-debugging` -> `superpowers-test-driven-development` -> `superpowers-verification-before-completion`
3. Policy flow: migration AGENTS enforces native skill usage without helper bootstrap
4. Isolation: root `skills/`, `commands/`, docs, and root `AGENTS.md` remain untouched

---

## Assumptions

- Migration workspace is intentionally separate from legacy fork assets.
- Backward compatibility with wrapper-based bootstrap is not part of this phase.
- Legacy command shims remain out of scope.
- Validation is lightweight/manual.
