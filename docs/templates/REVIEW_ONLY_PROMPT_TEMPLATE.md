# REVIEW_ONLY_PROMPT Template

> Purpose: a Nova/maintainer review prompt (Review-only profile, B1–B2) that works from an Evidence Pack and starts no new implementation.
> Part of the [Token Efficiency & Context Budget Baseline](../guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) (NDF-WP-152). Additive, docs-only.

```text
Keep this file short.
Do not duplicate completed history.
Reference stable NDF rules instead of repeating them.
Escalate context budget when scope, safety, release, ADR, privacy or compatibility risk increases.
```

## Template

```text
WP-ID / Titel:
SESSION:          # SAME_SESSION_ALLOWED | SAME_SESSION_RECOMMENDED | NEW_SESSION_RECOMMENDED | NEW_SESSION_REQUIRED
SESSION REASON:   # required for every SESSION value — task-specific, never generic
STATUS:           # COMPLETE | COMPLETE REPLACEMENT
SUPERSEDES:       # COMPLETE REPLACEMENT only — do not merge with earlier versions
Prompt profile: Review-only (B1–B2)   # starts no new implementation

Neue Session nötig?   # separate German session notice outside the header — exact wording for the SESSION value (Execution Contract, Rule 1)

Review-Auftrag:
Abnahmekriterien:

## Evidence Pack       # format: guide §12; obligations: Execution Contract, Rule 6
Evidence tier:         # E1 – Basis | E2 – Regulär | E3 – Erweitert — declared or derived, with reason
Relevant files:
Relevant diffs:
Checks run:            # actual result; exit status for process checks; kind of check
Checks not run:        # and why
Scope / integrity:     # comparison basis and what it proves
Acceptance criteria:   # met / not met
Known risks:
Open questions:
Evidence limits:       # source classes, unverified claims, local vs. CI

Erwartetes Review-Ergebnis: GO / GO WITH NOTES / REWORK / STOP / BLOCKED
```

## Notes

- Review-only never edits code or starts implementation; it evaluates the Evidence Pack against the acceptance criteria. A review prompt or verdict grants no implicit implementation authority — implementation needs its own complete execution contract.
- If evidence is missing or contradictory → request it or escalate the budget; do not guess.
- Evidence fields and Evidence Tiers follow the [guide](../guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) §12 and [Rule 6 – Execution Evidence](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (NDF-WP-167): the review checks that the evidence matches the tier and the specific claim; the tier sets the evidence scope, not the review depth or any authority.
- Execution header per the [Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (NDF-WP-153, hardened by NDF-WP-169): `SESSION REASON` for every value and a matching German session notice outside the header, as for every other execution prompt. A REWORK verdict is followed by a `COMPLETE REPLACEMENT` execution prompt, not a delta; a corrected review prompt is likewise re-issued in full with `SUPERSEDES`.
- Governance/release/security reviews stay Full where the fail-closed rules require it.
- No secrets, no private data, no private project names or domains.
