---
name: ndf-compact-context-summary-runner
description: Produce the mandatory NDF closing and handover content — Report to Nova, Compact Context Summary, and next-step session/handoff essentials — fitted into the active prompt's return format instead of a fixed block shape. USE WHEN closing an NDF work package or handing over to Nova, the Human Maintainer, or a new session. DO NOT USE to start or route a WP (use ndf-work-package-runner). Docs-only, fail-closed, no private data, no chain-of-thought.
---

# ndf-compact-context-summary-runner

## Title

NDF Compact Context Summary Runner (docs-only, ADR-0032-compliant).

## Purpose

Standardize the mandatory closing content of an NDF work package — the **Report to Nova**, the **Compact Context Summary**, and the next-step handoff essentials — in a short, copyable form that fits the active prompt's return format, so it need not be re-templated in every prompt.

## When to use

- **USE WHEN** closing any NDF work package, or when a compact handover to Nova (ChatGPT), the Human Maintainer, or a new session is needed.
- **DO NOT USE** to start or route a WP → `ndf-work-package-runner`; for Context Pack upkeep → `ndf-context-pack-maintainer`; for a CHANGELOG entry → `ndf-changelog-writer`.

## Required inputs

- The active prompt's return format (if any) and its declared profile / budget.
- The honest WP result (the executor's self-assessment — not a Nova verdict or Human-Maintainer acceptance) and the honest gate / validation status.
- Changed and created files, next steps, open notes, and the relevant unchanged governance invariants.

## Format precedence

Select the shape in this order ([Execution Contract](../../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md), Rule 4):

1. **Active authorised prompt format** — if the prompt defines a return format (including its blocked variant), use exactly that structure.
2. **Mandatory minimum NDF content** — always present, fitted into the chosen structure: honest result, changed files, validation / gate status, open notes or risks, next step, Human-Maintainer gate, Compact Context Summary content.
3. **Short Report** ([guide §13](../../../docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md)) — for B0 / B1 where no stronger format exists.
4. **Standard Report to Nova** (result, changed files, key notes, next step, proposed commit message) plus Compact Context Summary — for larger work where no stronger format exists; full report for B3 / B4.
5. **Blocked report** ([lifecycle §12](../../../framework/standards/WORK_PACKAGE_LIFECYCLE.md)) — when blocked and no prompt format exists.

No fixed block count: never add a parallel block the prompt did not ask for, and never drop mandatory content for compression.

## Next-step and handoff essentials

When a next step or handoff is produced, include or fit in (cf. the [`SESSION_HANDOFF` template](../../../docs/templates/SESSION_HANDOFF_TEMPLATE.md)):

- the next authorised action — never pre-start a WP that still awaits acceptance;
- the active contract the next step builds on — contract ID / revision, `STATUS`, `SUPERSEDES` for a replacement, and the repository revision — so the resumption can run the freshness check (Execution Contract, Rule 5);
- the session for the next step — exactly one `SESSION` value with a task-specific reason for every value, plus the matching German session notice as a separate line (Execution Contract, Rule 1);
- the recommended prompt profile / budget — escalated on any fail-closed trigger;
- a do-not-reload list;
- forbidden work;
- relevant invariants where needed.

If the active prompt already requests equivalent fields (e.g. its own `SESSION_HANDOFF` section), fill those instead of adding a second handoff block.

## Expected outputs

- The closing content in the shape selected under Format precedence: Report-to-Nova content and Compact Context Summary content (WP, result, status, changed files, next steps, open notes, unchanged governance invariants) — short and copyable — plus the handoff essentials wherever a next step is given.

## Allowed actions

- Generate the closing content from the provided WP result.
- Reflect the result, gate status, and any Nova verdict honestly, keeping them distinct from Human-Maintainer acceptance.

## Forbidden actions

- Force long justifications; keep it short and copyable.
- Insert private context details, secret values, or private project names.
- Invent missing decisions, verdicts, commit hashes, or releases; embellish a WP result.
- Hide gate failures or replace the Human Maintainer's decision.
- Duplicate fields the active prompt already carries.
- Document chain-of-thought.

## Fail-closed behavior

If the result, verdict, or gate status is unclear, report conservatively (REWORK / notes, or BLOCKED) rather than GO, and mark the uncertainty explicitly. Never report acceptance, a commit, or a release without authoritative evidence. Anything not explicitly allowed is forbidden.

## Public-neutrality requirements

No private project names, real private domains, secret values, private search patterns, real reviewer identities, org-internal names, or personal data. The secret name `NDF_PUBLIC_NEUTRALITY_DENYLIST` may be named; its value never. Allowed role phrasing — DE: "Nova (ChatGPT) – die ChatGPT-basierte Planungs-, Architektur- und Review-Rolle."; EN: "Nova (ChatGPT) – the ChatGPT-based planning, architecture and review role."

## ADR-0032 safety boundaries

Docs-only, fail-closed; no scripts; no network; no secrets; no private data; no autonomous git/release/tag actions; Public Quality Gate and Public Neutrality mandatory.

## Human-maintainer-only boundaries

The closing content is a suggestion. Nova (ChatGPT) issues review verdicts (evaluations, not acceptance); the Human Maintainer accepts governed changes and performs staging, commit, push, tag, and release.

## Output contract

The closing content in the shape selected under Format precedence — no fixed block count. The mandatory content is always present and reflects the true result.

## Compact Context Summary / Report-to-Nova requirements

This skill **is** the enforcement point for the mandatory closing content: Report-to-Nova and Compact-Context-Summary content (or the active prompt's equivalents) is always present and never dropped for compression; only its shape follows the active prompt.
