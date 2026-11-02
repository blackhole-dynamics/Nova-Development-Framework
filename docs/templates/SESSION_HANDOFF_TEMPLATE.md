# SESSION_HANDOFF Template

> Purpose: resume an interrupted session without the whole old chat. Builds on the Compact Context Summary and adds *Do not reload* and *Forbidden work*.
> Part of the [Token Efficiency & Context Budget Baseline](../guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) (NDF-WP-152). Additive, docs-only. Handoff is not an implementation mode.

```text
Keep this file short.
Do not duplicate completed history.
Reference stable NDF rules instead of repeating them.
Escalate context budget when scope, safety, release, ADR, privacy or compatibility risk increases.
```

## Template

```text
Project:
NDF version:
Branch / revision:             # repository revision the handoff was written against
Active WP:
Active contract:               # contract ID / revision · STATUS · SUPERSEDES (replacements only)
Scope:
Completed:
Open:
Decisions:
Open Human-Maintainer decisions:
Blockers:
Relevant files:
Do not reload:
Next action:
Session for next step:        # one of the four SESSION values + task-specific reason (every value)
Session notice:               # matching German notice, e.g. "Neue Session nötig? Ja – neue Session erforderlich."
Recommended prompt profile:
Forbidden work:
Compact Context Summary:
```

## Handoff types

- Implementation continuation
- Review
- Fix
- Human-maintainer decision
- Nova handoff

## Notes

- One screen maximum (~30 lines). It replaces chat history, not the safety/gate/human-review checks.
- `Session for next step`: `SAME_SESSION_ALLOWED` / `SAME_SESSION_RECOMMENDED` / `NEW_SESSION_RECOMMENDED` / `NEW_SESSION_REQUIRED`; give a concise, task-specific reason for every value and the matching German notice ([Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md), Rule 1, NDF-WP-153 / NDF-WP-169).
- **Freshness check on resumption** (Execution Contract, Rule 5): confirm the `Active contract` is still current (not superseded or contradicted). A changed repository revision is not automatically `BLOCKED` — check what changed and whether it touches the contract's files or assumptions; a material deviation or a superseded / conflicting contract → STOP / `BLOCKED`, never silent execution.
- `Recommended prompt profile`: Lean / Handoff / Review-only / Fix / Standard / Full — escalate on any fail-closed trigger.
- No secrets, no private data, no private project names or domains.
