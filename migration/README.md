# Migration Workspace: Codex-Native Superpowers Skills

This folder isolates skill migration work from the legacy fork so we can iterate safely, preserve fidelity, and install only validated outputs.

## Why This Exists

- Keep migration artifacts separate from root `skills/` and root `AGENTS.md`.
- Preserve original behavior while adapting only what is required for Codex.
- Maintain a reversible, auditable migration path before global rollout.

## What We Migrated

The migrated skill set lives under:

- `migration/.codex/skills/`

Current migrated skills (15):

- `superpowers-using-superpowers`
- `superpowers-brainstorming`
- `superpowers-writing-plans`
- `superpowers-test-driven-development`
- `superpowers-systematic-debugging`
- `superpowers-verification-before-completion`
- `superpowers-using-git-worktrees`
- `superpowers-executing-plans`
- `superpowers-requesting-code-review`
- `superpowers-code-review`
- `superpowers-receiving-code-review`
- `superpowers-finishing-a-development-branch`
- `superpowers-writing-skills`
- `superpowers-dispatching-parallel-agents`
- `superpowers-subagent-driven-development`

## AGENTS Migration

- `migration/AGENTS.original.md`: preserved baseline copy of the original repo `AGENTS.md`.
- `migration/AGENTS.md`: migration-local Codex-native top sections with compatibility mapping rules; policy from `# Intro` onward remains functionally aligned.

## Migration Strategy (High-Fidelity)

We performed a high-fidelity restore pass: near-verbatim skill content, with only minimal Codex adapters.

Adapters applied:

- Skill naming uses `superpowers-*` (validator-safe, source-faithful).
- Legacy references `superpowers:<name>` mapped to `superpowers-<name>`.
- `TodoWrite` mapped to `update_plan`.
- Claude-specific tool wording mapped to Codex-native wording.
- Capability gates added where the original workflow depends on delegation/parallel features that may not be available in-session.

## Capability-Gated Skills

These skills explicitly declare fallback behavior when required capabilities are unavailable:

- `migration/.codex/skills/subagent-driven-development/SKILL.md`
- `migration/.codex/skills/dispatching-parallel-agents/SKILL.md`

## Worktree Default (Current)

- Canonical worktree skill: `superpowers-using-git-worktrees`
- Default for new setups: `~/.worktrees/<repo>/<branch>`
- Precedence remains:
  - Existing repo-local `.worktrees/`
  - Existing repo-local `worktrees/`
  - Instruction-file preference (for example, `AGENTS.md`)
  - Then fallback default `~/.worktrees/<repo>/<branch>`

## Installation Status (Current)

Phase 1-3 rollout to `/Users/felix/.codex/skills` is complete via symlinks for fast iteration.

Installed (symlinked from migration workspace): 13 skills

- `brainstorming`
- `code-review`
- `executing-plans`
- `finishing-a-development-branch`
- `receiving-code-review`
- `requesting-code-review`
- `systematic-debugging`
- `test-driven-development`
- `using-git-worktrees` (skill: `superpowers-using-git-worktrees`)
- `using-superpowers`
- `verification-before-completion`
- `writing-plans`
- `writing-skills`

Exception (intentionally not installed yet):

- `subagent-driven-development` (held back pending verified delegation capability for full-fidelity use)
- `dispatching-parallel-agents` (held back pending verified true parallel delegation capability)

Validation performed:

- Verified each installed link points to `migration/.codex/skills/<skill>`.
- Verified each installed skill contains `SKILL.md` and valid frontmatter `name`.

## Supporting Files Migration Status

High-fidelity support-file migration is complete for all migrated skills.

- Copied all non-`SKILL.md` files from `skills/<skill>/...` to matching paths in `migration/.codex/skills/<skill>/...`.
- Support files were added across:
  - `requesting-code-review`
  - `subagent-driven-development`
  - `systematic-debugging`
  - `test-driven-development`
  - `writing-skills`
- Verified support-file parity relative to source skills, with one intentional migration divergence:
  - `skills/requesting-code-review/code-reviewer.md` was replaced by `migration/.codex/skills/requesting-code-review/reviewer-prompt.md` as part of the dedicated `superpowers-code-review` split.

## Code Review Skill Split

To support Codex-native independent review threads, reviewer prompt content was split out of `requesting-code-review` into a dedicated skill:

- New skill: `migration/.codex/skills/code-review/SKILL.md`
- Reviewer handoff template: `migration/.codex/skills/requesting-code-review/reviewer-prompt.md`

`superpowers-requesting-code-review` now defines "new thread reviewer" mode as preferred and references `superpowers-code-review` for review execution.

Because installed entries in `/Users/felix/.codex/skills` are directory symlinks into `migration/.codex/skills`, these copied support files are immediately available for installed skills without extra per-file linking.

Runtime scope note:
- This remediation pass normalized runtime `SKILL.md` files.
- Some support/reference files intentionally retain archival legacy terminology for high-fidelity provenance.

## Planning Artifacts

- `migration/docs/plans/2026-02-04-codex-native-core-loop-migration.md`
- `migration/docs/plans/2026-02-06-runtime-skill-audit-remediation.md`

This captures the implementation plan and verification checkpoints used for the migration effort.

## Scope Boundary

Migration work is intentionally local to `migration/`. Root repository behavior and legacy assets remain untouched until explicit rollout/installation.

## Upstream Sync Notes (2026-02-13)

Compared against upstream `main` changes through `e16d611`, we intentionally updated three migrated skills:

- `migration/.codex/skills/brainstorming/SKILL.md`
  - Added hard-gate and checklist/process-flow enforcement, while keeping Codex-native naming and references.
- `migration/.codex/skills/using-superpowers/SKILL.md`
  - Added Codex collaboration-mode `Plan` gate so brainstorming is required before plan-mode execution if not already completed.
- `migration/.codex/skills/writing-plans/SKILL.md`
  - Applied nested markdown fence fix (` ````markdown ... ```` `) for correct rendering.

Out-of-scope for this migration pass:

- `tests/subagent-driven-dev/run-test.sh`
  - Claude-specific harness for `subagent-driven-development` workflow tests.
  - Not currently relevant to Codex migration because `subagent-driven-development` remains intentionally not installed (see installation exceptions above).
