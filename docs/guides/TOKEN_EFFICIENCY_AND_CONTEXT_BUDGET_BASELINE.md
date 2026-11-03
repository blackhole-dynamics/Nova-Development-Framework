# Token Efficiency & Context Budget Baseline

> Work Package: `NDF-WP-152` — Token Efficiency & Context Budget Baseline
> Type: docs-only / additive baseline (no new skill, no subsystem)
> Basis: [WP-151 Skills Real-use and Context Efficiency Review](../validation/v1-1/SKILLS_REAL_USE_AND_CONTEXT_EFFICIENCY_REVIEW.md)
> Sprachstatus: EN mit deutschen Kernaussagen. / English with German key statements.

## 1. Purpose

This guide gives NDF a small, additive baseline for **token and context efficiency**: it lets normal work packages load less context, repeat stable rules less often, select skills more deliberately, and resume interrupted sessions through short handoffs — **without** weakening any safety, review, neutrality, or release gate. It is a documentation baseline, not a subsystem and not a new skill.

## 2. Problem statement

Real NDF-based Claude sessions hit usage limits after only a few large prompts. The proven causes (WP-151): every WP prompt re-carries the full stable frame (role model, hard limits, git/network/secret rules, neutrality rules, report + Compact-Context-Summary templates); mandatory reports run 15–17 sections even for small WPs; status documents grow additively; and sessions really were interrupted (documented resume WPs). Hypotheses still to measure: skill enumerations (10–15 per prompt), prompt↔report duplication, a missing lightweight handoff artifact.

## 3. Design principle — less context, same control

**Less context, same control.** A leaner budget removes *unnecessary* context, never diligence. Safety, neutrality, evidence, review depth, and every Human-Maintainer gate stay intact at every budget. When in doubt, the larger budget applies (fail-closed, section 16).

## 4. What WP-152 changes

- Adds **Context Budgets B0–B4** as a shared vocabulary for how much context a WP loads.
- Adds **additive prompt profiles** — Lean, Handoff, Review-only, Fix — as refinements of the existing Full/Standard/Short modes.
- Adds a compact **Work-Package Prompt Core** (8 elements) so normal prompts reference stable rules instead of repeating them.
- Adds small **templates**: `CURRENT_STATE`, `SESSION_HANDOFF`, Lean-WP / Review-only / Fix prompts.
- Adds a **Short Report** format and an **Evidence Pack** format.
- Adds a **skill-selection rule** (do not activate all 38 skills by default).
- Adds a **fail-closed rule set** and a neutral **project-local pilot** proposal.

## 5. What WP-152 does not change

No new skills; no skill removed or renamed; no incompatible change to Full/Standard/Short semantics; no new governance layer; no requirements-engineering system; no external tool, MCP, API, OAuth, network, or memory automation as NDF core; no scripts; no automated git/tag/release; ADR-0031/0032 unchanged; no v1.1 scope lock and no v1.1 release prep. Full reports and full context remain available and mandatory where the fail-closed rules require them.

## 6. Context classes

| Class | Purpose | Typical artifact |
|---|---|---|
| **Framework context** | invariant NDF rules (roles, hard limits, gate, ADRs) | reference the durable prompt blocks / skills — do not repeat |
| **Project context** | what the project is (goal, modules, key files) | project profile / optional `PROJECT_MAP` (project-local) |
| **Current state** | where the project stands now | `CURRENT_STATE` (small) |
| **Task context** | the concrete WP | the WP prompt (8-element core) |
| **Handoff context** | resume without chat history | `SESSION_HANDOFF` (small) |
| **Evidence context** | proof for a review | Evidence Pack |

Keep the six classes separate; deliver only the classes a WP actually needs.

## 7. Context Budgets B0–B4

| Budget | WP types | Typical sources | Allowed context classes | Skills | Governance share | Report | Review depth | Escalation |
|---|---|---|---|---|---|---|---|---|
| **B0 Micro** | typo, status line, 1-file correction | ≤ 2 | current state | 0–1 | reference only | Short Report (5–10 lines) | spot-check | any doubt → B1/B2 |
| **B1 Lean** *(preferred normal case)* | normal docs / small code WPs, continuations, fixes | ≤ 5 (≤ 3 fully read) | framework(ref) + current state + task (+ handoff) | 1–3 | reference + WP-specific special rules | Short Report + Compact Context Summary | targeted | scope unclear/critical → B2 |
| **B2 Standard** | medium features / reviews | ≤ 10 | + project context + evidence | 2–5 | reference + relevant invariants visible | standard report | normal | criticality → B3 |
| **B3 Extended** | architecture, release readiness, ADR-adjacent | as needed, justified | all, targeted | 4–8 | full relevant governance | full report | deep | governance conflict → B4/STOP |
| **B4 Exceptional** | release, scope lock, security special cases | justified per file | maximal needed | only with explicit justification | complete | complete | maximal | **not a standard**; recurring B4 need ⇒ split / re-scope the WP |

**Leitregeln:**

```text
B1 Lean ist der bevorzugte Normalfall.
B4 Exceptional darf kein Standard werden.
Regelmäßiger B4-Bedarf bedeutet: WP splitten oder Scope reduzieren.
```

No pseudo-precise token targets without measured data (baseline / target corridor / minimum improvement / abort criteria live in the WP-151 measurement model).

### 7.1 Terminology Namespacing for Consumer Projects

Innerhalb des NDF-Kerns behalten `B0`…`B4` und `Lean` ihre hier definierte Bedeutung — unpräfigiert. Kollidiert ein Consumer-Projekt bereits mit denselben Begriffen (eigenes `B1`, eigenes `Lean` o. Ä.), werden im Integrations-/Enablement-Kontext die namespaced Formen `NDF-B0`…`NDF-B4` / `NDF-Lean` verwendet, um die NDF-Bedeutung von der projekteigenen zu unterscheiden. Unpräfigierte projekt-lokale Begriffe behalten dabei ihre eigene, projekt-lokale Bedeutung. Dies ist eine reine Namensraum-Klärung, kein neues Budget-Modell — die native NDF-Terminologie `B0`–`B4`/`Lean` wird nicht umbenannt.

Within NDF core, `B0`–`B4` and `Lean` keep their meaning as defined here — unprefixed. Where a consumer project already has a naming collision with these same terms (its own `B1`, its own `Lean`, etc.), the namespaced forms `NDF-B0`…`NDF-B4` / `NDF-Lean` are used in the integration/enablement context to distinguish the NDF meaning from the project's own. Unprefixed project-local terms keep their own, project-local meaning. This is a pure namespacing clarification, not a new budget model — NDF's native `B0`–`B4`/`Lean` terminology is not renamed.

## 8. Prompt Profiles

The profiles are **additive refinements** of the existing [Prompt Modes](../agent-workflows/NDF_PROMPT_MODES.md) — Full/Standard/Short semantics are unchanged.

| Profile | Purpose | Mandatory info | Forbidden repetition | Budget | Suited WPs |
|---|---|---|---|---|---|
| **Lean** | preferred normal case | 8-element WP core | role model, standard hard limits, template full text | B1 | normal docs / small code WPs, fixes, continuations |
| **Handoff** | resume a session (not an implementation mode) | `SESSION_HANDOFF` block | old chat, full original prompt | B0–B1 | continuations |
| **Review-only** | Nova / maintainer review (starts no new implementation) | Evidence Pack + acceptance criteria | full WP text again | B1–B2 | reviews |
| **Fix** | one targeted correction (does not widen scope) | symptom, goal, affected file(s), invariant | the whole frame | B0–B1 | bug/correction |

**Leitentscheidung:** *Lean ist der bevorzugte Normalfall, sofern keine erhöhte Komplexität oder Kritikalität vorliegt. Full darf nicht allein deshalb verwendet werden, weil er mehr Sicherheit vermittelt.* Full stays mandatory for release, ADR, security policy, v1.x-compatibility, and complex reviews (section 16). Handoff is not an implementation mode. Review-only starts no new implementation. Fix must not widen scope.

## 9. Work-Package Prompt Core

Normal WP prompts reduce to **8 elements**:

```text
1. Ziel   2. Scope   3. relevante Quellen   4. verbindliche Invarianten (nur WP-spezifisch)
5. konkrete Aufgabe   6. Abnahmekriterien   7. Non-Goals   8. Rückmeldeformat (Referenz)
```

**Nur referenzieren (skill-/dokumentgetragen, nicht wiederholen):** Standard-Rollenmodell · Standard-Git-Grenzen · Standard-Secret-Grenzen · Standard-Public-Neutrality-Grenzen · Standard-Self-Check · Standard-Rückmeldeformat · Standard-Skills-first-Regeln.

**Immer sichtbar bleiben:** WP-ID · Ziel · Scope · Allowed/Forbidden Files · WP-spezifische Sonderregeln · Fail-Closed-Trigger · Human-Maintainer-Gate · erwartete Commit-Message.

Template: [`LEAN_WP_PROMPT_TEMPLATE.md`](../templates/LEAN_WP_PROMPT_TEMPLATE.md).

**Execution contract (NDF-WP-153):** every execution prompt also carries the execution header (`SESSION`, `SESSION REASON`, `STATUS`; `SUPERSEDES` for replacements) per the [Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md). A *Complete Execution Instruction* does not mean repeating stable boilerplate: the 8-element core plus the always-visible fields is complete. A full replacement after a correction reuses the compact current contract, not the entire historical conversation.

## 10. Session Handoff

A minimal resume format so a new chat/session does not need the whole old chat. Template: [`SESSION_HANDOFF_TEMPLATE.md`](../templates/SESSION_HANDOFF_TEMPLATE.md). Handoff types: implementation continuation, review, fix, human-maintainer decision, Nova handoff. It builds on the existing Compact Context Summary and adds the two missing fields *Do not reload* and *Forbidden work*. It is a template + the additive Handoff profile — **not** a new skill.

## 11. Current State

A ≤ 1-page status extract that replaces re-reading long context packs at session start. Template: [`CURRENT_STATE_TEMPLATE.md`](../templates/CURRENT_STATE_TEMPLATE.md). It does not duplicate completed history and never replaces a check of the current files, the public quality gate, or human review.

## 12. Evidence Pack

A compact review input that avoids raw logs while staying verifiable. The evidence obligations are normative only in the [Execution Contract, Rule 6 – Execution Evidence](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (NDF-WP-167); this section gives the format, and §12.1 illustrates how the tiers typically apply.

```markdown
## Evidence Pack

Evidence tier:        # E1 – Basis | E2 – Regulär | E3 – Erweitert — declared or derived, with reason
Relevant files:
Relevant diffs:
Checks run:           # command or method · actual result (exit status for process checks) · kind of check
Checks not run:       # check · reason
Scope / integrity:    # comparison basis · what it proves · what it does not
Acceptance criteria:  # met / not met
Known risks:
Open questions:
Evidence limits:      # source classes, unverified claims, local vs. CI
```

The six original fields stay. NDF-WP-167 adds `Evidence tier`, `Checks not run`, `Scope / integrity`, and `Evidence limits`; a field that does not apply may be marked `n/a` (typical at E1).

### 12.1 Evidence Tiers

The normative minimum assignment of E1/E2/E3 is defined only in [Rule 6 – Execution Evidence](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (*Evidence Tiers*). The table is illustrative: its examples show typical cases and the evidence a tier usually adds; it is no separate trigger source, and where an example and Rule 6 diverge, Rule 6 decides.

| Tier | Illustrative example (assignment: Rule 6) | Evidence, in addition to the lower tier where applicable | Not required |
|---|---|---|---|
| **E1 – Basis** | e.g. typo, link fix, small editorial change | evidence that fits the change (e.g. the diff and a direct check of the edited place) | general before/after hashes · environment details · full logs |
| **E2 – Regulär** | e.g. a regular docs work package or a bounded correction without an E3 risk factor | relevant repository revision · traceable scope check · the project-appropriate quality gates actually run, with reliable process results · short note on the relevant test environment · open evidence limits | a specific NDF script in consumer projects — project-appropriate gates are sufficient |
| **E3 – Erweitert** | e.g. a new or changed normative contract rule, a compatibility-relevant change, release preparation, a security-relevant change | targeted before/after integrity evidence · check of protected areas · differentiated kind and coverage of tests · explicit "not verified" statements · prefix proof for relevant append-only claims | a repository-wide full-hash duty · full logs |

The highest applicable risk factor decides; under-declaration, derivation of a missing tier, and proportionality follow Rule 6. An E3 result still stays compact: it adds the evidence the risk needs, not volume.

**Distinction.** Evidence Tiers are not context budgets: there is no mapping `B0 → E1`, `B2 → E2`, or `B4 → E3`; a small prompt can need E3, and a large one can stay E2. Tiers are equally independent of prompt modes and profiles, of the governance-tier candidate WP-164 (not activated), of the evidence-strength ratings used in reviews (e.g. "evidence level strong"), and of source classes: a tier fixes the *required* evidence scope in advance; a strength rating evaluates *existing* evidence afterwards.

## 13. Short Report Format

For B0/B1 WPs, replacing the 15–17-section report where it is not required:

```markdown
## Short Report

Result:
Changed files:
Evidence:        # Evidence tier + key results, or a reference to the Evidence Pack (§12)
Risks:
Open questions:
Next step:
Compact Context Summary:
```

Rule: B0/B1 do not automatically produce a 15–17-section report; the full report stays allowed and mandatory for B3/B4; review quality must not drop.

`Evidence:` states the Evidence Tier and the decisive results, or refers to the relevant Evidence Pack; a short report never duplicates a full evidence block that already exists (NDF-WP-167).

## 14. Skill selection rule

```text
NDF has 38 docs-only skills as a library.
Do not mentally activate all 38 skills by default.
Select only the skills required for the current task.
```

| Budget | Skills |
|---|---|
| B0 | 0–1 |
| B1 | 1–3 |
| B2 | 2–5 |
| B3 | 4–8 |
| B4 | only with explicit justification |

**Core candidate set** — the four core-MVP skills of the authoritative [Skills-first Operating Mode](../validation/foundation-0-9/SKILLS_FIRST_OPERATING_MODE.md): `ndf-work-package-runner`, `ndf-compact-context-summary-runner`, `ndf-public-neutrality-guard`, `ndf-context-pack-maintainer` — selected per task, **not forced blindly into every prompt**. `ndf-changelog-writer` is a **support skill**, selected only when the CHANGELOG is actually in scope. *(Reconciled in NDF-WP-153: the WP-151 real-use classification had listed `ndf-changelog-writer` instead of `ndf-context-pack-maintainer` among the four frequent candidates.)* The 38 skills stay unchanged; this is a usage rule, not a skill change.

## 15. Optional project-local tools

Optional, **project-local only — never NDF core**: Repomix, repo-map tools, local semantic code search, layered-memory approaches, token-optimizer plugins. Rules: no public-NDF requirement; no automatic installation; **no MCP/API/OAuth/network function as NDF core**; check privacy and public neutrality; never put secrets or private data into a tool context; document any tool use project-locally. The secret name `NDF_PUBLIC_NEUTRALITY_DENYLIST` may be named, its value never.

## 16. Fail-Closed Rules

Lean / B0 / B1 **must not** be used for: release gate · ADR change · security policy · v1.x-compatibility risk · breaking-change review · migration · privacy or permission change · contradictory sources · unclear scope · missing authoritative documents · public-neutrality uncertainty.

```text
Fehlender Kontext wird sichtbar gemacht, nicht geraten.
Bei Unsicherheit: Budget erhöhen, STOP melden oder Human-Maintainer-Gate auslösen.
```

This extends the existing forbidden-Short-prompt cases; Lean broadens the Short logic, it does not replace it.

## 17. Project-local Pilot

Pilot archetype: **operations-oriented consumer project** (neutral; no private project data). The pilot tests `CURRENT_STATE`, `SESSION_HANDOFF`, Lean prompt, Review-only prompt, Fix prompt, B0/B1/B2 budgets, Short Report, Evidence Pack. Success criteria: several connected work steps without full context; less repeated boilerplate; fewer loaded files; clear resume after interruption; no worse review quality; no lost governance boundaries. No pseudo-precise token goals without measured data. NDF-core adoption of any pilot result stays a later Human-Maintainer decision.

## 18. Decision

**GO WITH NOTES – token efficiency and context budget baseline implemented.** Additive and docs-only; no new skills; no skill removal/renaming; no tool requirement; no MCP/API/OAuth/network; Lean is the new preferred normal case but fail-closed; B4 is exceptional, not standard; project-local pilot recommended; v1.1 stays planning only (no scope lock, no release prep). Next: Human-Maintainer commit, then run the project-local pilot before any NDF-core hardening.

*Status update (NDF-WP-153):* WP-152 is committed (`c4c1c34`); real project-local pilot evidence informed the follow-up [Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (WP-153). Current sequence: [v1.1 plan](../roadmap/V1_1_PLAN.md).

*Status update (NDF-WP-167):* §12 (Evidence Pack fields, §12.1 Evidence Tiers) and §13 (`Evidence:` field) were extended for [Rule 6 – Execution Evidence](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md). The extension applies prospectively from the Human-Maintainer acceptance of NDF-WP-167; the WP-152 decision above and evidence packs authored earlier stay valid as written.
