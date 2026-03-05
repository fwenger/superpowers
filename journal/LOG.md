### E-20260305-0905 | tags: skills handoff-format prompt-output process

- context: Felix reported friction with migrated-skill handoffs where copy/paste prompts included extra surrounding text and reviewer template heading noise.
- decision/root-cause: Standardized v1 handoff format on a single fenced code block for both reviewer and parallel-session implementer handoffs, removed reviewer template heading from prompt body, and added fallback rule to move to strict prompt-only output if fence copying proves noisy.
- evidence (test/log/observation): Approved design captured in docs/plans/2026-03-05-handoff-prompt-format-design.md and implementation plan in docs/plans/2026-03-05-handoff-prompt-format.md.
- reuse-rule: "Next time, when handoff prompts are copied across clients (app/IDE/CLI), define one explicit output contract in the skill and enforce it through reusable templates with required fields."
