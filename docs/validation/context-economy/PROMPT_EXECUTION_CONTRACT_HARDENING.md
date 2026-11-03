# NDF-WP-169 — Prompt Execution Contract Hardening Validation

> Work Package: `NDF-WP-169` — Prompt Execution Contract Hardening
> Type: docs-only governance hardening — no runtime, tooling, or enforcement machinery
> Normative block: [BLOCK_EXECUTION_CONTRACT.md](../../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) · WP notes: [WP_169 notes](../../../project-brain/WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md)

**Kernaussage:** Jede neu erzeugte Session-Angabe ist begründet und menschenlesbar; ein Ersatzvertrag prüft die Session neu und erweitert keine Rechte stillschweigend; ein Handoff wird vor der Wiederaufnahme auf Aktualität geprüft.

## 1. Status

Implementation complete. After Nova's verdict `REWORK_REQUIRED – DOCUMENTATION & EVIDENCE ONLY`, Corrective Pass CP01 corrected evidence statements in this document, the WP-169 notes, and `CHANGELOG.md` only (§13); the normative changes are untouched. Pending Nova re-review and Human-Maintainer acceptance. This document declares no GO and no acceptance. `AGENT_COMPLETE != HUMAN_APPROVED` · `NOVA_REVIEW != HUMAN_ACCEPTANCE`.

## 2. Goal and normative basis

- **Goal:** close the gaps left by the WP-153 baseline — optional reason for `SAME_SESSION_ALLOWED`, no human-readable session statement, no session re-assessment or scope guard on `COMPLETE REPLACEMENT`, no freshness rule for handoffs.
- **Basis:** NDF v1.1.0; [ADR-0031](../../adr/ADR-0031-v1x-compatibility-policy.md) (v1.x compatibility); [ADR-0032](../../adr/ADR-0032-skill-security-policy.md) (skill security); NDF-WP-152 ([Token Efficiency & Context Budget Baseline](../../guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md)); NDF-WP-153 ([Execution Contract](../../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md), [validation](../v1-1/PROMPT_EXECUTION_CONTRACT_BASELINE.md)); NDF-WP-154 ([Skills Pack P0 Hardening](../v1-1/SKILLS_PACK_P0_HARDENING.md)).
- **Authority:** Human-Maintainer-authorised execution contract `NDF-WP-169` (`STATUS: COMPLETE REPLACEMENT`, 2026-11-02): docs-only, explicit eleven-file allowlist, no git writes, no release. Accepted decisions: Option C (header unchanged, separate German notice), O-1…O-6. CP01 ran under a separate Human-Maintainer-authorised contract (`STATUS: COMPLETE REPLACEMENT`, 2026-11-02): docs-only, three-file allowlist (this document, the WP-169 notes, `CHANGELOG.md`), no git writes; the eleven-file allowlist did not apply to CP01.
- **Baseline:** `main` at `4dab503bd49c53191d46e56c6b77bffbe9320135`, empty index, no tracked changes, 38 untracked `SKILL.md` files under `.agents/skills/` (three differ from `.claude/skills/`: `ndf-context-pack-maintainer`, `ndf-skill-quality-reviewer`, `ndf-skill-trigger-quality-reviewer`) — matching the earlier read-only preflight in file count and in these three known differences; no per-file hash baseline was recorded (§9.2). No fetch, no network.

## 3. Changes made

| File | Change | Requirement |
|---|---|---|
| `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md` | Rule 1: reason for every value, generic-reason ban, German notice table, decision aids with host-neutrality, prospective transition. Rule 3: session re-assessment, missing `SUPERSEDES` → REWORK, no silent scope expansion, existing rules kept. New Rule 5 – Handoff Freshness. Header fields unchanged; only the `SESSION REASON` annotation updated. | A1–A4, B1–B3, C |
| `docs/templates/LEAN_WP_PROMPT_TEMPLATE.md` | Reason annotation for every value; separate notice line; notes updated | D |
| `docs/templates/FIX_PROMPT_TEMPLATE.md` | Same; explicit session re-assessment for corrections | D |
| `docs/templates/REVIEW_ONLY_PROMPT_TEMPLATE.md` | Same; no implicit implementation authority | D |
| `docs/templates/SESSION_HANDOFF_TEMPLATE.md` | Fields `Active contract`, `Open Human-Maintainer decisions`, `Session notice`; revision annotation; freshness-check note | D, C |
| `docs/agent-workflows/NDF_PROMPT_MODES.md` | DE/EN execution-header sections only: reason for all values, `SAME_SESSION_ALLOWED` exception lifted for new prompts, notice, prospective transition | D |
| `framework/prompts/PROMPT_INDEX.md` | Execution-contract entry names the WP-169 hardening | D |
| `.claude/skills/ndf-compact-context-summary-runner/SKILL.md` | Next-step essentials: active-contract reference (Rule 5); reason for every value plus notice (Rule 1) | E |
| `CHANGELOG.md` | `[Unreleased]` → `### Changed` entry | F3 |
| this document, WP-169 notes | new | F1, F2 |

Not changed: header field set and order; Rules 2 and 4; the WP-153 cut-over and legacy fallback; mode and profile semantics; any other skill, ADR, script, roadmap, or release file.

## 4. Compatibility assessment

- **Class:** additive with a prospective transition (ADR-0031). The new obligations bind instructions authored after the Human-Maintainer acceptance of WP-169; earlier instructions keep the rules in force when they were authored. No commit hash or date is invented.
- **WP-153 legacy fallback** (`NEW_SESSION_RECOMMENDED` + `SESSION_DECLARATION_MISSING_LEGACY`) unchanged.
- **No new error code** (O-2), **no new handoff status code** (O-3), **no script-comment obligation** (O-4), **no roadmap change** (O-5).
- **Header:** the five header fields are structurally unchanged (Option C); a prompt valid under WP-153 keeps the same parse.
- **Modes and profiles:** Full / Standard / Short and Lean / Handoff / Review-only / Fix keep their meaning.
- **Host neutrality:** no host-specific mechanism is mandated; making one universal is itself a REWORK case.
- **Single normative source:** the rules live only in `BLOCK_EXECUTION_CONTRACT.md`; templates, modes, index, and skill reference it.

## 5. Test method

Each case is a controlled sample situation checked by hand against the changed rule text: does the text yield the expected outcome without needing extra interpretation? This is a **documentary rule-conformance analysis, not an executed agent-behaviour test.** No external system, no write workflow, and no second model or host was used. Whether an agent actually applies the rules is therefore `NOT_VERIFIABLE` for every case; the one real instance available (the WP-169 contract executed in this session) is noted under T11 as self-reported, not independent evidence.

## 6. Test matrix and results

Columns: *Rule check* = documentary result; *Agent behaviour* = executed-behaviour result.

| ID | Input situation | Expected | Applied rule | Observed (rule text) | Rule check | Agent behaviour |
|---|---|---|---|---|---|---|
| T01 | New prompt (post-acceptance) without `SESSION` | REWORK | Rule 1 "missing declaration … prompt defect" | REWORK + `COMPLETE REPLACEMENT` | PASS | NOT_VERIFIABLE |
| T02 | `SESSION: NEW_SESSION_REQUIRED` with notice "Neue Session nötig? Nein – Fortsetzung zulässig." | REWORK | Rule 1 session notice: contradiction → REWORK; table maps REQUIRED to "Ja" | REWORK | PASS | NOT_VERIFIABLE |
| T03 | New prompt with `SESSION: SAME_SESSION_ALLOWED`, no `SESSION REASON` | REWORK | Rule 1 session reason: required for every value; missing → REWORK | REWORK | PASS | NOT_VERIFIABLE |
| T04 | `STATUS: COMPLETE REPLACEMENT` without `SUPERSEDES` | REWORK | Header (SUPERSEDES for replacements); Rule 3 re-assessment bullet: missing `SUPERSEDES` → REWORK | REWORK | PASS | NOT_VERIFIABLE |
| T05 | Replacement switches read-only → write-authorised but copies `SAME_SESSION_RECOMMENDED` from its predecessor | REWORK | Rule 3 session re-assessment: unsupported carried-over value → REWORK; decision aids point to REQUIRED for an authority change | REWORK | PASS | NOT_VERIFIABLE |
| T06 | Replacement silently adds `scripts/**` to the write allowlist and allows `git add` without authorisation | STOP | Rule 3 no silent scope expansion → STOP / `BLOCKED` | STOP / `BLOCKED` | PASS | NOT_VERIFIABLE |
| T07 | Correction: "use the previous PowerShell block, replace command 4" | BLOCKED | Rule 3 delta-only executable corrections invalid; fail-closed: incomplete instruction state → STOP / `BLOCKED` | `BLOCKED`, complete replacement requested | PASS | NOT_VERIFIABLE |
| T08 | Correction: "run the Bash script above, only change line 2" | BLOCKED | as T07 (Rule 3 applies to Bash/sh per scope line) | `BLOCKED` | PASS | NOT_VERIFIABLE |
| T09 | Prompt authored before WP-169 acceptance, with `SESSION` + reason, no German notice | Legacy fallback | Rule 1 prospective transition: judged by authoring-time rules | valid; no REWORK for the missing notice | PASS | NOT_VERIFIABLE |
| T10 | Handoff references contract revision 2; revision 3 has since replaced it | Re-assessment, BLOCKED if needed | Rule 5: check contract currency; superseded contract never executed silently | STOP / `BLOCKED`, current contract requested | PASS | NOT_VERIFIABLE |
| T11 | Valid replacement: all header fields, `SUPERSEDES`, specific reason, matching notice, no widening | PASS | Rules 1, 3 | executable | PASS | NOT_VERIFIABLE ¹ |
| T12 | Compact Lean (B1) prompt: 8-element core, header with specific reason, one notice line, stable rules referenced | PASS | Rule 2 (`COMPLETE != VERBOSE`), Rule 1 | executable; the notice adds one line, no budget escalation | PASS | NOT_VERIFIABLE |
| T13 | Prompt makes a specific host's session-fork feature a universal NDF obligation | REWORK | Rule 1 decision aids: host-specific mechanism as universal obligation → REWORK | REWORK | PASS | NOT_VERIFIABLE |
| T14 | WP-153-era prompt with `SAME_SESSION_ALLOWED`, no reason | Legacy-compatible | Rule 1 prospective transition (explicit example) | valid | PASS | NOT_VERIFIABLE |
| T15 | New prompt: `SESSION REASON: Sicherheitshalber.` | REWORK | Rule 1 session reason: generic reason → REWORK | REWORK | PASS | NOT_VERIFIABLE |
| T16 | Handoff with a still-current contract; HEAD moved by an unrelated docs commit | Re-verify, not auto-BLOCKED | Rule 5: freshness and scope check; only a material deviation blocks | continue after a recorded check | PASS | NOT_VERIFIABLE |
| T17 | Human Maintainer picks option B of fully defined options A/B; nothing else changes | No replacement needed | Rule 3 option-selection exception (unchanged) | no replacement | PASS | NOT_VERIFIABLE |

¹ One real instance: the WP-169 contract itself (`NEW_SESSION_REQUIRED`, specific reason, `COMPLETE REPLACEMENT`, `SUPERSEDES`, notice "Ja") was executed by the implementing agent in a new session. It predates WP-169 acceptance (so it is judged by WP-153 rules), its notice wording differs slightly from the table ("neue Claude-Session erforderlich"), and the observation is self-reported, so it is not independent behaviour evidence.

**Summary:** 17/17 PASS for the documentary rule check, 17/17 `NOT_VERIFIABLE` for agent behaviour, 0 FAIL, 0 NOT_RUN. The PASS values state only that the examined rule text yields the expected outcome; they are not results of executed agent-behaviour or cross-host tests (§5).

## 7. Limitations

- No executed agent-behaviour or cross-host test; no claim of host compatibility beyond the text being host-neutral.
- The rule check was done by the implementing agent; Nova's independent review is the first external check.
- The local Public Quality Gate runs without a neutrality denylist (none configured locally); a local strict PASS is therefore no evidence for a later CI run with a differently configured `NDF_PUBLIC_NEUTRALITY_DENYLIST`, which is authoritative for neutrality.
- Unchanged state of the 38 untracked `.agents/skills/` files during WP-169 is consistent with the observations but not proven, because no per-file hash baseline was recorded before WP-169 (§9.2).
- The notice wording is fixed in German only (O-1); English remains optional and unstandardised.

## 8. Skill quality check — `ndf-compact-context-summary-runner`

| Check | Result |
|---|---|
| Frontmatter (`name`, `description`) | unchanged |
| Triggers / USE WHEN / DO NOT USE | unchanged |
| 13 required ADR-0032 sections | all present, unchanged except "Next-step and handoff essentials" |
| New permissions, scripts, network, runtime | none |
| Skill chaining | none added; references only the Execution Contract and the handoff template |
| Execution contract weakened | no — the skill now carries the stricter Rule 1 / Rule 5 essentials |
| Output precedence, Human-Maintainer authority, docs-only | unchanged |
| ADR-0032 compliance | maintained |
| Integrity | content changed; pre-change SHA-256 (HEAD `4dab503`) `7fae60937332fa42da41ba5de40b41c383a83bba65e8519665c2d760906e9c44`; the working-tree digest now differs from it (re-checked in CP01). A consumer hash or lock record that pins the earlier content would report `modified` on re-verification ([Provenance & Integrity Lock](../../agent-workflows/NDF_SKILL_PROVENANCE_AND_INTEGRITY_LOCK.md) §13, §15). Whether such consumer records exist was not established: no file in this repository references the pre-change digest except this document (CP01 search), and consumers outside the repository cannot be checked from here. If such consumers exist, they need a controlled re-verification. As in WP-154, no post-change digest is recorded as a reference: if the Human Maintainer accepts and commits WP-169, that commit is the authoritative accepted revision. No automatic lock refresh. |
| `.agents/skills/` | not modified by CP01 (before/after SHA-256, §9.2); unchanged state during WP-169 is not proven (§9.2). Its untracked copy of this skill is byte-identical to the HEAD `4dab503` version (SHA-256 `7fae…9c44`) and therefore now differs from the changed `.claude/skills/` file (fourth known difference) |

Recommendation (advisory): GO for Nova review.

## 9. Quality gates

| Gate | Result (original WP-169 run) |
|---|---|
| Scope: working tree vs. eleven-file allowlist (tracked + untracked) | PASS — 9 modified, 2 new, all on the allowlist; 38 `.agents/skills/` files still present (count unchanged); unchanged content not proven (§9.2) |
| `git diff --check` | PASS — no whitespace errors |
| `git diff --cached --name-only` | PASS — index empty |
| New untracked documents checked directly (trailing whitespace, links) | PASS |
| Relative links in all eleven files | PASS — all resolve |
| `python scripts/check_public_quality.py --self-test` | reported "self-test passed"; the Python exit code was not reliably captured (shell pipeline) — superseded as evidence by the CP01 re-run (§9.1) |
| `python scripts/check_public_quality.py --strict` | reported 0 errors, 0 warnings (no local denylist); exit code not reliably captured and notices not fully documented — superseded as evidence by the CP01 re-run (§9.1) |
| ADR-0031 / ADR-0032 unchanged | PASS |
| No second normative execution contract | PASS |

The script was checked before running: it reads the file list via `git ls-files` and writes only into a temporary directory during the self-test. No install, no repair, no change to `scripts/**`.

### 9.1 CP01 re-run of the local Public Quality Gates

Run 2026-11-02, 13:50:40–13:50:41 UTC, on `main` at `4dab503bd49c53191d46e56c6b77bffbe9320135` (working tree with the WP-169 changes and the CP01 corrections written up to that point, i.e. without this subsection); PowerShell 7.6, Python 3.13. Invocation: the PowerShell 7 block of the CP01 contract, unchanged — `& python scripts/check_public_quality.py --self-test` and `& python scripts/check_public_quality.py --strict`, each followed directly by `$LASTEXITCODE`; no pipeline and no output filter. The script was re-read before the run (same behaviour as above; no network).

| Gate | Python exit code | Output | Errors / warnings / notices | Result |
|---|---|---|---|---|
| `--self-test` | `0` | `self-test passed` | – | PASS |
| `--strict` | `0` | `Public quality gate passed.` | 0 / 0 / 4 | PASS |

Strict notices, verbatim:

```text
[INFO] scan mode: tracked + new/untracked files (new-file neutrality check active)
[INFO] new-file neutrality check: 40 new text file(s) included in scan
[INFO] No custom neutrality denylist configured.
[INFO] new-file neutrality check: no denylist configured - only structure/root/README rules apply to new files
```

**Denylist:** neither `NDF_PUBLIC_NEUTRALITY_DENYLIST` (process, user, or machine environment) nor the local file `.ndf/public-neutrality-terms.local.txt` is configured; the neutrality term scan therefore ran without terms. A local strict PASS is no evidence for a later CI run with a differently configured denylist. A confirmation run after this subsection was written is recorded in the CP01 report to Nova.

### 9.2 Evidence limits — `.agents/skills/`

`.agents/**` is outside the authorised scope of WP-169 and of CP01. CP01 demonstrably changed no file there; for the WP-169 execution see *Historical* below.

- **Present:** 38 untracked `SKILL.md` files under `.agents/skills/` (count re-checked in CP01).
- **Observed properties:** all 38 modification times lie on 2026-09-23 between 12:40:45.12 and 12:40:45.46 UTC, before the WP-169 execution on 2026-11-02. 35 files are byte-identical to the corresponding `.claude/skills/` file at HEAD `4dab503`, including the summary-runner copy (SHA-256 `7fae…9c44`); 3 differ from it (`ndf-context-pack-maintainer`, `ndf-skill-quality-reviewer`, `ndf-skill-trigger-quality-reviewer`), as already recorded in the baseline.
- **Verifiable in CP01:** the SHA-256 of all 38 files was taken before the first CP01 write and again after the last; both sets are identical, so CP01 changed none of them.
- **Historical (WP-169 execution):** no per-file hash baseline was recorded before WP-169. Unchanged content during WP-169 is consistent with the observations above but not proven; for the three files that differ from HEAD there is no reference content at all.
- **Method limits:** modification times can be altered and say nothing about content; identity with a HEAD blob shows equal content, not an absence of intermediate writes; the before/after comparison covers only the CP01 run; untracked files have no git history.

## 10. Open risks and deviations

- **Consumer integrity drift** (medium, conditional): a consumer lock or stored digest that references the pre-change summary-runner content would report a mismatch after this change. Whether such consumers exist was not established; no concrete integrity violation is known. If they exist, the mitigation is a controlled re-verification of the affected consumers against the Human-Maintainer commit.
- **`ndf-work-package-runner` not aligned** (low): it reads the header but does not mention the session notice or Rule 5; it was explicitly out of scope. Its rules reference the Execution Contract, so no contradiction arises; a follow-up alignment is a Human-Maintainer decision.
- **`.agents/skills/` drift** (low): untracked copies now differ in four skills; synchronisation was excluded from this WP.
- **Historical records** (none): the WP-153 validation, notes, and CHANGELOG entry still describe the `SAME_SESSION_ALLOWED` exception; they record the WP-153 state and stay correct as history.
- **No deviation** from the authorised contract.

## 11. Nova and Human-Maintainer gate

Nova (ChatGPT) – the ChatGPT-based planning, architecture and review role – reviews scope, normative consistency, test evidence, security, and compatibility, and issues a verdict. The Human Maintainer alone accepts NDF-WP-169 and performs staging, commit, and push. The WP-169 obligations take effect only with that acceptance.

## 12. No anticipated acceptance

Nothing in this document is an acceptance, a commit record, or a release statement. `EXECUTED != ACCEPTED` · `READY != RELEASED`.

## 13. Corrective Pass CP01

Trigger: Nova verdict `REWORK_REQUIRED – DOCUMENTATION & EVIDENCE ONLY`; the normative part needed no change. Authority: Human-Maintainer-authorised CP01 contract (§2).

| Finding | Correction | Where |
|---|---|---|
| F-169-01 | "38 `.agents/skills/` files unchanged" narrowed to present files, observed properties, CP01-verifiable state, and the limits of historical proof | §2, §7, §8, §9, §9.2 |
| F-169-02 | Consumer-integrity statements made conditional; the existence of consumer locks is stated as not established | §8, §10; `CHANGELOG.md`; WP-169 notes |
| F-169-03 | Local Public Quality Gates re-run with directly captured exit codes and complete notices; the original run is marked as not reliable evidence | §9, §9.1 |
| F-169-04 | Documentary PASS vs. `NOT_VERIFIABLE` agent behaviour kept; summary clarified; no new behaviour tests, no cross-host claim | §6 |

CP01 changed no normative rule, template, skill, ADR, script, or `.agents/**` file. It is neither a Nova verdict nor an acceptance.

## 14. Post-Acceptance Evidence – NDF-WP-170 Reconciliation

> Appended additively by NDF-WP-170 (2026-11-03). Sections 1–13 stay unchanged as the historical record; their "pending" statements describe the state before acceptance.

| Item | Evidence | Verification |
|---|---|---|
| Human-Maintainer acceptance | WP-169 `ACCEPTED WITH NOTES`; CP01 `ACCEPTED`; final Nova verdict `GO_WITH_NOTES` | acceptance: Human-Maintainer statement in the WP-170 contract and commit body of `24760c4`; Nova verdict: Human-Maintainer statement only (no verdict document in the repository) |
| Commit | `24760c4315a02e26d61b17cc43eece56e52579d9` — "docs(governance): harden prompt execution contract (WP-169)", 2026-11-02 | `git log` (read-only) |
| Push | `origin/main` = `24760c4` | `git ls-remote origin refs/heads/main` (read-only), 2026-11-03 |
| GitHub CI | Workflow "Public Quality Gate", event `push`, head SHA `24760c4…`, conclusion `success` | `gh run list --commit` (read-only), 2026-11-03 |
| Release | none — WP-169 authorises no release, tag, or release preparation | — |

Unchanged by this reconciliation:

- **Test limits:** the 17 cases of §6 remain a documentary rule-conformance analysis — 17/17 PASS for the rule check, 17/17 `NOT_VERIFIABLE` for agent behaviour. They are not re-assessed retroactively, and no agent-behaviour or cross-host test is added or claimed.
- **Normative rules:** no WP-169 rule, template, skill, or ADR is changed; the Execution Contract stays the single normative source.
- **Limitations (§7, §9.2, §10):** they remain in force as accepted notes; the CI run used the repository's configured denylist setting, which this document does not inspect.
- **Effect:** the WP-169 obligations apply prospectively to instructions authored after the Human-Maintainer acceptance.

The acceptance basis is the Human-Maintainer decision together with the verified commit; a commit body alone is not a general substitute for any future Human-Maintainer approval.
