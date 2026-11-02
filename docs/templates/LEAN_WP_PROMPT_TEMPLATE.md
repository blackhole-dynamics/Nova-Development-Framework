# LEAN_WP_PROMPT Template

> Purpose: a compact work-package prompt (Lean profile, B1) that references stable NDF rules instead of repeating them.
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
Prompt profile: Lean (B1)   # escalate on any fail-closed trigger

Neue Session nötig?   # separate German session notice outside the header — exact wording for the SESSION value (Execution Contract, Rule 1)

1. Ziel:
2. Scope:
3. Relevante Quellen:
4. Verbindliche Invarianten (nur WP-spezifisch):
5. Konkrete Aufgabe:
6. Abnahmekriterien:
7. Non-Goals:
8. Rückmeldeformat: Short Report + Compact Context Summary (Referenz)

Authority:              # who approves/decides; the agent executes only this contract
Allowed files:
Forbidden files:
Allowed operations:
Forbidden operations:
STOP conditions:        # fail-closed triggers
Human-Maintainer gate:  # staging/commit/push/tag/release stay human-only
Erwartete Commit-Message (Vorschlag):

Referenzierte Standardregeln (nicht wiederholen):
  Rollenmodell · Git-Grenzen · Secret-Grenzen · Public-Neutrality · Self-Check · Skills-first · Execution Contract
```

## Notes

- Use Lean only when no elevated complexity or criticality applies. For release, ADR, security policy, v1.x-compatibility, breaking-change, migration, privacy/permission, unclear scope, contradictory sources → escalate to Standard/Full.
- Select only the skills required (B1: 1–3). Do not force all 38 skills.
- Execution header and replacement semantics: [Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (NDF-WP-153, hardened by NDF-WP-169). `SESSION REASON` is required for every value and names the task-specific factor; the German session notice stays a separate line outside the header and must match `SESSION`. A corrected prompt is re-issued in full as `COMPLETE REPLACEMENT` with `SUPERSEDES`, never as a delta. Complete ≠ verbose: fill the fields, reference the stable rules.
- No secrets, no private data, no private project names or domains.
