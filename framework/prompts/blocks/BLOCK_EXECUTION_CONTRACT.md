# Prompt Block – Execution Contract

> NDF-WP-153 — Prompt Execution Contract Baseline; hardened by NDF-WP-169 (session reason and notice, replacement re-assessment, handoff freshness). Docs-only governance rule: no runtime, tooling, or enforcement machinery.
> Sprachstatus: EN mit deutscher Kernaussage. / English with a German key statement.

**Kernaussage:** Jede Ausführungsanweisung ist ein vollständiger, eigenständiger aktiver Vertrag — nach jeder Korrektur vollständig neu ausgegeben, nie als Delta.

**Scope:** framework-wide, for every execution instruction in every prompt mode and profile — AI/agent prompts and Human-Maintainer command sequences (PowerShell, Bash/sh, CMD, Git, Docker/Docker Compose, infrastructure CLI, other executable command blocks).

## Execution header

```text
SESSION:         SAME_SESSION_ALLOWED | SAME_SESSION_RECOMMENDED | NEW_SESSION_RECOMMENDED | NEW_SESSION_REQUIRED
SESSION REASON:  one concise, task-specific line (required for every value; Rule 1)
STATUS:          COMPLETE | COMPLETE REPLACEMENT
SUPERSEDES:      <instruction ID / WP revision>                          (COMPLETE REPLACEMENT only)
RULE:            Do not merge this instruction with earlier versions.   (COMPLETE REPLACEMENT only)
```

No further metadata is required. The human-readable session notice (Rule 1) is given outside this header; the header fields stay as listed.

## Rule 1 – Session Declaration

- **Cut-over:** "legacy" means an execution instruction authored before the Human-Maintainer commit accepting NDF-WP-153; an instruction authored under the accepted baseline after that commit is new. No commit hash is embedded here.
- Every new execution instruction declares exactly one `SESSION` value; session continuity is never implicit.
- A missing declaration in a new instruction is a prompt defect → `REWORK` and a `COMPLETE REPLACEMENT`.
- **Legacy fallback (non-breaking):** a legacy instruction is not blocked solely because the declaration is missing; treat it as `NEW_SESSION_RECOMMENDED` and report `SESSION_DECLARATION_MISSING_LEGACY`.
- **Session reason (NDF-WP-169):** `SESSION REASON` is required for every one of the four values and names the actual, task-specific factor — e.g. a work-package change, the state of the available contract context, or a relevant authority or safety-boundary difference. Generic reasons ("Neue Aufgabe.", "Sicherheitshalber.", "Besser für Claude.") are insufficient. A missing or generic reason in a newly authored instruction is a prompt defect → `REWORK`.
- **Session notice (NDF-WP-169):** every newly authored execution instruction — including standalone NDF planning, review, read-only, and design-only prompts — additionally gives the human-readable German notice for its `SESSION` value as a separate line outside the header; an English equivalent is optional. A notice that contradicts `SESSION` in a newly authored instruction → `REWORK`.

| `SESSION` | Required German notice |
|---|---|
| `SAME_SESSION_ALLOWED` | Neue Session nötig? Nein – Fortsetzung zulässig. |
| `SAME_SESSION_RECOMMENDED` | Neue Session nötig? Nein – bestehende Session empfohlen. |
| `NEW_SESSION_RECOMMENDED` | Neue Session nötig? Nicht zwingend – neue Session empfohlen. |
| `NEW_SESSION_REQUIRED` | Neue Session nötig? Ja – neue Session erforderlich. |

**Decision aids (not host assumptions):**

| `SESSION` | Typically indicated by |
|---|---|
| `SAME_SESSION_ALLOWED` | continuation of the same active contract; a trivial option selection under the Rule 3 exception |
| `SAME_SESSION_RECOMMENDED` | a necessary correction within the same contract and authority, where the current session context is complete and still current |
| `NEW_SESSION_RECOMMENDED` | a new, independent work package without an authority change; session context that is stale, long, or partly superseded |
| `NEW_SESSION_REQUIRED` | a relevant change of authority or safety boundary (e.g. read-only → write-authorised); conflicting active contracts in the session; context known to be incomplete for the new contract |

`NEW_SESSION_REQUIRED` needs a traceable reason and is never a blanket default. The criteria assume no host feature: a prompt that makes a host-specific mechanism (e.g. one tool's session forking, memory, or worktrees) a universal NDF obligation → `REWORK`.

- **Prospective transition (NDF-WP-169):** the WP-153 cut-over and legacy fallback above stay unchanged. The WP-169 obligations — reason for every value, no generic reason, session notice — apply to instructions authored after the formal Human-Maintainer acceptance of the completed NDF-WP-169; no commit hash or date is embedded here. Earlier instructions are judged by the rules in force when they were authored (e.g. a WP-153-era `SAME_SESSION_ALLOWED` without reason, or a prompt without the notice, stays valid). No new error code is introduced.

## Rule 2 – Complete Execution Instruction

- One self-contained active contract: neither the executor nor the Human Maintainer has to merge earlier messages to know what to execute.
- Contains, where relevant: goal · scope · authoritative sources · authority · task-specific invariants · allowed/forbidden files · allowed/forbidden operations · task · acceptance criteria · STOP conditions · Human-Maintainer gate · return/output requirements.
- Stable NDF rules are referenced, not copied.
- **Human-Maintainer command sequences** additionally name, where applicable: target shell · working directory · required baseline/preconditions · complete ordered command sequence for the authorised gate · expected result · verification · STOP condition.

```text
COMPLETE != VERBOSE
COMPLETE WITHIN AUTHORIZED SCOPE != REPEAT THE WHOLE PROJECT WORKFLOW
```

## Rule 3 – Complete Replacement

- Triggers: prompt defect · command defect · `REWORK` · resolution of `BLOCKED` · scope correction · authority clarification · review-driven correction · changed allowed/forbidden scope · changed executable instruction.
- The successor is regenerated in full as `STATUS: COMPLETE REPLACEMENT` with `SUPERSEDES`; it reuses the compact current contract, not the conversation history.
- Delta-only executable corrections are invalid — e.g. "use the previous PowerShell block, but replace command 4". Valid: a complete corrected block marked `COMPLETE REPLACEMENT`.
- **Option-selection exception:** a Human-Maintainer selection among options already fully defined in the active instruction needs no replacement — only if it changes none of: scope · authority · allowed/forbidden files · allowed/forbidden operations · executable commands · acceptance criteria · STOP conditions. Otherwise → `COMPLETE REPLACEMENT`.
- **Session re-assessment (NDF-WP-169):** every `COMPLETE REPLACEMENT` re-assesses `SESSION` and `SESSION REASON`. The previous value is carried over only if the re-assessment supports it; relevant changes (authority, safety boundary, scope, context state) are stated in the reason. A replacement without `SUPERSEDES`, or one that carries over a session value the changed contract no longer supports, is a prompt defect → `REWORK`.
- **No silent scope expansion (NDF-WP-169):** a `COMPLETE REPLACEMENT` never widens without authorisation: allowed write paths · allowed/forbidden operations · permissions · work-package scope · git rights · external system actions · acceptance or release rights. An authorised widening is marked as such in the replacement — what is widened, on whose authority. Unauthorised or unclear widening → STOP / `BLOCKED`.
- The existing replacement rules above and the command-sequence rule (Rule 2) stay authoritative and unchanged; NDF-WP-169 adds no script-comment obligation.

## Rule 4 – Prompt-over-Skill Output Precedence

- If a generic Skill output contract conflicts with the explicit return format of the active authorised prompt, the prompt's format wins.
- Mandatory minimum reporting content required by higher NDF authority (e.g. Report to Nova, Compact Context Summary, Human-Maintainer gates) stays binding and is fitted into the prompt's structure.
- A Skill never silently replaces or weakens the active execution contract; a real normative conflict is reported and fails closed.

## Rule 5 – Handoff Freshness

> NDF-WP-169.

- A session handoff references traceably: project / work package · active contract ID or revision · contract `STATUS` · `SUPERSEDES` where the contract is a replacement · repository revision · open Human-Maintainer decisions · the session classification for the next step (`SESSION`, reason, notice).
- On resumption the executor first checks that the referenced contract is still current — not superseded, withdrawn, or contradicted by a later contract.
- A changed repository revision is not automatically `BLOCKED`: it requires a traceable freshness and scope check (what changed, and whether it touches the contract's files, sources, or assumptions). A material deviation → `BLOCKED` with a report; otherwise continue and record the check.
- A superseded, no longer valid, or conflicting contract is never executed silently → STOP / `BLOCKED`; request the current contract or a `COMPLETE REPLACEMENT`.
- This rule adds no runtime and no automatic session management.

## Authority and fail-closed

- `DERIVE != DECLARE` · `VERIFY != APPROVE` · `EVIDENCE != AUTHORITY` · `EXECUTED != ACCEPTED` · `AGENT_COMPLETE != HUMAN_APPROVED` · `NOVA_REVIEW != HUMAN_ACCEPTANCE`.
- Nova (ChatGPT) – the ChatGPT-based planning, architecture and review role – issues review verdicts (GO / GO WITH NOTES / REWORK / STOP / BLOCKED). A verdict is an evaluation: it does not itself accept governed changes, expand scope, accept ADRs, or perform any Git/release action.
- The Human Maintainer remains the final owner: normative acceptance of governed changes, scope changes, ADR acceptance, and staging, commit, push, tag, and release. This block grants no new authority to any agent or Skill; no AI role stages, commits, pushes, tags, or releases.
- Missing, ambiguous, or conflicting instruction state → STOP / `BLOCKED` with a report; never guess, never merge instruction versions.
