# NDF-WP-167 — Execution Evidence Hardening Validation

> Work Package: `NDF-WP-167` — Execution Evidence Hardening
> Type: docs-only governance hardening — no runtime, tooling, or enforcement machinery
> Normative block: [BLOCK_EXECUTION_CONTRACT.md](../../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (Rule 6) · Format: [Token Efficiency & Context Budget Baseline](../../guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) §12–§13 · WP notes: [WP_167 notes](../../../project-brain/WP_167_EXECUTION_EVIDENCE_HARDENING_NOTES.md)

**Kernaussage:** Ein Nachweis belegt genau die Behauptung, für die er erbracht wurde — risikogestaffelt, hostneutral und ohne neue Autorität; der Execution Contract bleibt die einzige normative Quelle.

## 1. Mandate and authorisation

- **Goal:** anchor the evidence practice proven in WP-169 and WP-170 (direct exit-code capture, hash baselines before writes, separation of documentary and executed checks, append-only prefix proofs, local vs. CI) consistently, risk-proportionally, and host-neutrally in the existing NDF architecture.
- **Authority:** Human-Maintainer-authorised execution contract `NDF-WP-167` (`STATUS: COMPLETE REPLACEMENT`, `SESSION: NEW_SESSION_REQUIRED`, Full, B3 Extended, intended Evidence Tier E3), executed in a new session on 2026-11-03. Docs-only; exact seven-file allowlist; no git writes; no release authority. Accepted architecture decisions D-1…D-12 and contract corrections C-167-01…C-167-03, N-167-04 (see WP notes).
- **Status:** `AGENT_COMPLETE – READY_FOR_NOVA_REVIEW`. This document declares no GO and no acceptance. `AGENT_COMPLETE != HUMAN_APPROVED` · `NOVA_REVIEW != HUMAN_ACCEPTANCE`.

## 2. Repository baseline

Source class: direct tool output (read-only git commands), 2026-11-03.

| Item | Result |
|---|---|
| Root / remote | repository root confirmed; `origin` = the expected public NDF repository (owner handle not recorded here, public neutrality) |
| Branch / HEAD | `main` @ `ebff8626665d517f2017f843dd2e323b143d85f4` |
| Remote HEAD | `refs/heads/main` = `ebff8626…` (`git ls-remote`, no fetch) |
| Index / tracked changes | empty / none |
| In-progress git operation | none (no merge, rebase, cherry-pick, revert, or bisect state) |
| Untracked files | exactly 38 `.agents/skills/*/SKILL.md` |
| `.agents/skills/` integrity | list hash (`sha256sum` per file, sorted by path, SHA-256 of the list) `cf59b237cab107dffb68f781d7822753a5df456c29e03ece6dfb57100e79f8ba` — reproduces the value recorded in WP-170 CP01.9 |
| `.agents` vs `.claude` | exactly the four known differences (`ndf-compact-context-summary-runner`, `ndf-context-pack-maintainer`, `ndf-skill-quality-reviewer`, `ndf-skill-trigger-quality-reviewer`); all eight per-file hashes match WP-170 §7 |
| Allowlist | five existing targets present; both new targets absent |
| Planning status | WP-167 `RESERVED CANDIDATE – NOT ACTIVATED` (P1) in the WP-ID register; activated only by this contract (N-167-04) |

## 3. ADR-0031 compatibility gate

Executed before the first write, against [ADR-0031](../../adr/ADR-0031-v1x-compatibility-policy.md), [ADR-0032](../../adr/ADR-0032-skill-security-policy.md), the [v1.1 readiness review](../v1-1/V1_1_READINESS_REVIEW.md) R2, the Execution Contract, and the WP-169 transition model.

| # | Question | Finding |
|---|---|---|
| 1 | Affected public interfaces | Execution Contract (new Rule 6), Evidence Pack and Short Report format (guide §12/§13), Review-only template, prompt index entry |
| 2 | Work-Package flow (Stable Candidate) | not changed: roles, flow, and the review values GO / GO WITH NOTES / REWORK / STOP keep their meaning; `REWORK` is reused as an existing verdict |
| 3 | Execution rights / contract semantics | unchanged: no right is granted or removed; `EVIDENCE != AUTHORITY` stays; Rules 1–5 byte-identical (§9) |
| 4 | Retroactive invalidation | none: prospective transition, earlier work judged by authoring-time rules (T13) |
| 5 | Additive and prospective | yes: one new rule, four new Evidence Pack fields; the six original fields stay |
| 6 | Header, modes, profiles, budgets | unchanged; tiers explicitly independent of B0–B4, modes, profiles; no header field |
| 7 | Consumers without new tooling | yes: no script, schema, parser, or tool duty; project-appropriate gates suffice (T18) |
| 8 | Migration note | *CP01 correction (F-167-02):* no mandatory tooling or runtime migration; consumers adopting the updated NDF rules apply the new evidence requirements prospectively to newly authored execution instructions and results; historical records stay valid under the rules applicable when authored. This is the short migration note ADR-0031 expects where users are affected, carried in the CHANGELOG entry. Original wording and re-check: §13 |
| 9 | Additional ADR / governance path | not required: no change to ADR-governed policy, Public Quality Gate expectations (Governed), or skill security |

**Result:** gate satisfied — additive with a prospective transition (ADR-0031). Remaining limit: Rule 6 tightens how *future* results must be evidenced; a consumer that adopts NDF updates will see stricter review expectations for new work, which is the intended prospective effect. *CP01:* the original migration finding (row 8) was too broad (F-167-02) and is corrected; the classification was re-checked against ADR-0031 in CP01 (§13.2).

## 4. Changes made

| File | Change | Workstream |
|---|---|---|
| `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md` | new `## Rule 6 – Execution Evidence` (12 bullets) inserted after Rule 5; metadata line names NDF-WP-167 | A |
| `docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md` | §12 Evidence Pack: Rule-6 pointer, four added fields with annotations; new §12.1 Evidence Tiers (trigger table, distinction); §13 `Evidence:` annotation and one rule line; prospective status update after §18 | B |
| `docs/templates/REVIEW_ONLY_PROMPT_TEMPLATE.md` | Evidence Pack block aligned to §12; one note referencing guide §12 and Rule 6 | C |
| `framework/prompts/PROMPT_INDEX.md` | execution-contract entry names NDF-WP-167 / Rule 6 | D |
| `CHANGELOG.md` | one entry under `[Unreleased]` → `### Changed` | G |
| this document, WP-167 notes | new | E, F |

Not changed: Rules 1–5, the execution header, the authority section, `BLOCK_FEEDBACK_TO_NOVA.md` (D-3), `NDF_PROMPT_MODES.md` (D-8), all skills (D-11), ADRs, scripts, workflows, roadmap, register, context pack, next phase, historical WP records, released CHANGELOG sections.

## 5. Source-of-truth check

| Check | Result |
|---|---|
| Normative evidence obligations live only in Rule 6 | *CP01 correction (F-167-01):* PASS after correction — the normative minimum E1/E2/E3 assignment now stands in Rule 6; guide §12 gives the format and §12.1 illustrative examples, marked as no trigger source. The original PASS overlooked that the assignment stood only as `Typical trigger` in the guide (§13) |
| Guide does not restate Rule 6 | PASS — §12.1 points to Rule 6 for under-declaration, derivation, proportionality |
| Template and index reference, do not redefine | PASS |
| No second Evidence Standard file | PASS — no new normative document; this file is validation evidence |
| No contradiction with Rules 1–5 | PASS — Rule 6 reuses `REWORK` and `EVIDENCE != AUTHORITY`; host-neutrality clause mirrors Rule 1's decision-aid clause |

## 6. Evidence Tiers

- **Labels:** `E1 – Basis` · `E2 – Regulär` · `E3 – Erweitert` (D-2). *CP01 correction (F-167-01):* the normative minimum assignment stands in Rule 6; guide §12.1 gives illustrative examples and the typical evidence per tier (§13).
- **Selection:** highest applicable risk factor; missing tier derived and named; under-declaration waives nothing (`REWORK`).
- **Name-collision check (before implementation):** repository-wide `git grep` for `Evidence Tier`, `Evidence Level`, `evidence class`, word-bounded `E1`/`E2`/`E3`, and tier terms, plus the untracked `.agents/skills/`. `E1`/`E2`/`E3` occur only as byte matches in three binary files (two PNG, one PDF) — no textual meaning. "Evidence-Level strong" (WP-089), the strength scale of `ndf-validation-evidence-reviewer` (strong … insufficient), and the evidence-source classes of the v1.1 release evidence index rate or classify *existing* evidence; WP-164 "Governance Tiers" is an undefined, not-activated candidate. **No semantic collision**; the distinction is stated in guide §12.1.
- **This WP:** E3 (normative contract change, compatibility relevance).

## 7. Documentary test matrix

**Method.** Each case is a controlled sample situation checked by hand against the new rule text: does the text yield the expected rule outcome without extra interpretation? This is a **documentary rule check, not an executed agent-behaviour or cross-host test** (D-10). `PASS` / `FAIL` here are documentary results only; `REWORK` is the existing Nova review verdict, not a new status (C-167-02).

Columns: *Expected* = expected rule outcome · *Rule check* = does the documented rule meet the case · *Behaviour test* = was actual agent behaviour tested.

| ID | Situation | Expected | Rule-6 statement (and guide) | Documentary finding | Rule check | Behaviour test | Residual uncertainty |
|---|---|---|---|---|---|---|---|
| T01 | Process reports `passed`, exit status not captured | no reliable PASS from the message alone | *Reliable results:* "success text alone is no reliable process evidence" | yields expected | PASS | no | — |
| T02 | Exit code masked by a pipeline | no verified process PASS | *Reliable results:* exit status "captured directly and unaltered (e.g. not masked by a pipeline)" | yields expected | PASS | no | — |
| T03 | E1 typo fix without hash and environment | allowed | guide §12.1 E1 "Not required: general before/after hashes · environment details" | yields expected | PASS | no | — |
| T04 | Normative contract change declared E1 | contract defect; `REWORK` | *Evidence Tiers:* highest risk factor; under-declaration "→ `REWORK`"; §12.1 E3 trigger "normative" | yields expected | PASS | no | boundary between "minor" and "normative" stays a judgement call |
| T05 | "Unchanged" without a comparison basis | disclose evidence limit | *Integrity:* "Without a basis, the claim is reported as an evidence limit, not as fact" | yields expected | PASS | no | — |
| T06 | Required append-only prefix proof missing | claim not established; `REWORK` | *Proportionality:* prefix proof needed; "claim asserted as established without the evidence its tier requires → `REWORK`" | yields expected | PASS | no | — |
| T07 | Final hash of the notes in an external closing report | allowed | *Self-reference:* "no file has to contain its own final hash" | yields expected | PASS | no | — |
| T08 | CI success claimed before the run | not allowed | *Local checks and CI:* "a future CI result is never anticipated" | yields expected | PASS | no | — |
| T09 | Local strict PASS without denylist presented as full neutrality proof | rule defect; `REWORK` | *Local checks and CI:* "no complete neutrality evidence"; *Proportionality:* unsupported established claim → `REWORK` | yields expected via two bullets | PASS | no | outcome relies on combining two bullets |
| T10 | Documentary test declared as executed behaviour test | rule defect; `REWORK` | *Kinds of check:* "never reported as an executed or behaviour test → otherwise `REWORK`" | yields expected | PASS | no | — |
| T11 | Nova verdict taken from a Human-Maintainer message, source class stated | allowed | *Sources:* relayed statement "valid as what it is — never as independent verification" | yields expected | PASS | no | — |
| T12 | Universal `$LASTEXITCODE` duty | host-neutrality defect; `REWORK` | *Host neutrality:* no universal "exit-code variable" duty; one host method as universal obligation "→ `REWORK`" | yields expected | PASS | no | — |
| T13 | Historical WP without an Evidence Tier | judged by the norm of its time | *Prospective transition:* "earlier work is judged by the rules in force when it was authored" | yields expected | PASS | no | — |
| T14 | Reproducible list hash for a large protected area | allowed | *Integrity:* "A reproducible list hash (method stated) may cover a large protected area" | yields expected | PASS | no | — |
| T15 | Confidential denylist term in public evidence | not allowed | *Security:* "no confidential denylist terms or sensitive log content in public evidence" | yields expected | PASS | no | — |
| T16 | Tier missing, risk clearly E2 | derive E2 and name it | *Evidence Tiers:* "A missing tier is derived and named with its reason" | yields expected | PASS | no | — |
| T17 | Small append-only addendum with prefix proof | no automatic full E3 | *Proportionality:* "does not by itself trigger E3" | yields expected | PASS | no | — |
| T18 | Consumer without the NDF gate script | project-appropriate evidence allowed | *Proportionality:* no particular tool; §12.1 E2 "project-appropriate gates are sufficient" | yields expected | PASS | no | — |
| T19 | Post-push CI checked by the Human Maintainer, no follow-up WP | allowed | *Local checks and CI:* recorded "in the Human-Maintainer closure … no automatic extra work package" | yields expected | PASS | no | — |
| T20 | Evidence Tier used to replace a Human-Maintainer gate | not allowed | *Authority unchanged:* "an Evidence Tier never replaces a Human-Maintainer gate" | yields expected | PASS | no | — |

**Summary:** 20/20 documentary rule checks PASS, 0 FAIL. Behaviour test executed: no, for all 20 cases. No agent-behaviour, cross-host, or consumer test was run; whether agents apply Rule 6 in practice is **not verified**. The rule check was done by the implementing agent; Nova's review is the first independent check.

*CP01 note:* the rows above record the original documentary check against the pre-CP01 text and are not re-labelled; the CP01 documentary re-check against the corrected text is in §13.3.

## 8. Quality gates

Source class: direct tool output. Script read beforehand: file lists via `git ls-files` (read-only), writes only into a `TemporaryDirectory` during the self-test, no network.

**Run 1** — after the five edits, before the two new files: 2026-11-03, 10:24:05–10:24:06 UTC; Git Bash 5.3.15, Python 3.13.17; each exit status read via `$?` directly after the command, output redirected to a file outside the repository (no pipeline).

| Gate | Exit code | Output | Errors / warnings / notices |
|---|---|---|---|
| `python scripts/check_public_quality.py --self-test` | `0` | `self-test passed` | – |
| `python scripts/check_public_quality.py --strict` | `0` | `Public quality gate passed.` | 0 / 0 / 4 |

Notices: scan mode tracked + new/untracked; 38 new text files in scan (the `.agents/skills/` files); no custom denylist configured; only structure/root/README rules apply to new files. **Denylist configured: no** — `NDF_PUBLIC_NEUTRALITY_DENYLIST` absent at process, user, and machine level (presence checked, value never read) and no `.ndf/public-neutrality-terms.local.txt`. A local PASS is therefore no complete neutrality evidence and no GitHub CI result.

Further checks in run 1: `git diff --check` exit `0`; index empty; HEAD unchanged. A confirmation run with both new files present, relative-link and Markdown checks of all seven files, and the final integrity comparison are recorded in the closing report to Nova (this document cannot contain its own final state).

## 9. Scope and integrity evidence

Comparison basis: SHA-256 taken before the first write in this session; copies of the five targets kept outside the repository. These hashes prove equal or changed content at the two compared points in time only.

| File | SHA-256 before | SHA-256 after |
|---|---|---|
| `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md` | `0aa6897189f2d3abca8b3ecd4478202915ed7807350683e6f27096ad81a4983b` | `bb26b455ad59ce91d35fbdacdb8d1142742fffd6fda3bcec54935497cad91f4c` |
| `docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md` | `a6a98597250cb7449c7fde1007cab1b310e07be2a602728cf12cf00691c2f7ef` | `24c8a036caad474bb3390ced7fe2109fe68ca73a90c320eb500b637f0a747b16` |
| `docs/templates/REVIEW_ONLY_PROMPT_TEMPLATE.md` | `ceb78a44f9d31e37913e1bc62e0c22e03590b33d57b867cb6791d313b83e258b` | `0e9cb692d398c7e919fdbc7f708ae542c76ca85184f329df33905f3b277b4fbe` |
| `framework/prompts/PROMPT_INDEX.md` | `e8937707feed94d25e18f40578e4b187ed435bbfb6a446e320a9856d9937dbf6` | `3006d2e594691a5de4d3b9b43cf4d450c12a89a94f32aa71801902de44983513` |
| `CHANGELOG.md` | `15c4eda665f4f72610c23355c89090a9a5875f5ec3a25407832c165a47279b8b` | `cd96231b41c25a0426fe9a78ba8894c77ec457d76676cc6a0bcf1a4eb7a8a5c3` |

- **Rules 1–5 unchanged:** the section from `## Execution header` through the last Rule-5 bullet and the `## Authority and fail-closed` section have identical SHA-256 before and after; `git diff -U0` shows only the metadata line 3 and the inserted Rule-6 block.
- **CHANGELOG:** one inserted line under `[Unreleased]`; everything from `## [1.1.0]` onwards is identical before and after.
- **Protected areas (before values):** list hashes (method as in §2) of `scripts/` (5 tracked files) `0cc05567…5940`, `.github/` (6) `2de166ae…246d`, `docs/adr/` (14) `f5a85b5b…ad0f`, `.claude/` (39 files) `bfeaea2a…4f1a`; per-file hashes of ADR-0031 `030d0e96…86e0`, ADR-0032 `6542b81c…df2b`, `BLOCK_FEEDBACK_TO_NOVA.md` `a57a24f2…6046`, `NDF_PROMPT_MODES.md` `a1952638…786d`, WP-169 notes `31972f6b…8608`, WP-169 validation `f1cf366e…6e16`, WP-170 notes `f0bb95de…50f8`, register `711e4889…af85`, roadmap `50a97db5…699f`, context pack `6001b92d…1930`, next phase `78db6ce2…7d2c`, `README.md` `ada4730b…2a23`; whole working tree (987 files excluding `.git`) list hash `ecfc97be…fe76`. The after-comparison is in the closing report to Nova.
- **No historical claim:** these values do not prove anything about the state before this session beyond what the reproduced WP-170 list hash (§2) covers.

## 10. Security and compatibility boundaries

- No denylist content was read or output; only the presence of the variable and the local file was checked.
- No script, workflow, skill, ADR, or `.agents/**` / `.claude/**` file changed; G-14 (possible disclosure of private denylist terms via gate error messages) stays a separate security review (D-7) — Rule 6's security bullet covers only how evidence is reported.
- Host neutrality: the rule text names no mandatory host method; the commands used in this WP are recorded as what was used, not as a requirement.
- Compatibility: §3.

## 11. Open risks

- Rule 6 is verified only documentarily; real agent adherence is not verified (§7).
- "Minor" vs. "normative" (E1 vs. E3) remains a judgement call; Rule 6 resolves doubt by the highest risk factor, which may over-tier borderline cases.
- Local gates run without a denylist; the CI run with the configured secret stays authoritative and is future evidence (not anticipated).
- Skill alignment with Rule 6 (`ndf-work-package-runner`, `ndf-compact-context-summary-runner`, `ndf-validation-evidence-reviewer`) is deferred (D-11) until the WP-168 parity strategy is clarified; until then skills reference the contract without naming Rule 6.
- Historical WP-170 status wording stays as recorded (D-5); verdict, status, and error-code vocabulary is not unified (D-6); stale status wording in `NDF_PROMPT_MODES.md` stays (D-8).

## 12. Handover to Nova

Nova (ChatGPT) – the ChatGPT-based planning, architecture and review role – reviews scope, normative consistency, the documentary test matrix, integrity evidence, security, and compatibility, and issues a verdict. The Human Maintainer alone accepts NDF-WP-167 and performs staging, commit, and push. Rule 6 takes effect only with that acceptance. No other work package (WP-162…166, WP-168) is activated by this WP.

## 13. Corrective Pass CP01

> Authority: Human-Maintainer decision `NDF-WP-167 CP01 AUTHORIZED – DOCS ONLY` (`NDF-WP-167 CP01 — Full Authorized Corrective Pass Contract`, `STATUS: COMPLETE REPLACEMENT`, `SESSION: NEW_SESSION_REQUIRED`, Full, B3 Extended, Evidence Tier E3), following Nova's verdict `REWORK_REQUIRED – TARGETED DOCUMENTATION CORRECTION`. Executed in a new session on 2026-11-03. Docs-only; five-file write allowlist; no git writes. Sections 1–12 record the original execution; CP01 corrections in them are marked *CP01* and are no original evidence.

### 13.1 Findings and corrections

| Finding | Original state | CP01 correction | Files |
|---|---|---|---|
| F-167-01 | Rule 6 required the highest applicable tier and rated under-declaration `REWORK`, but the risk assignment stood only as `Typical trigger` in guide §12.1; §5 and §6 above described the guide as carrying "format and triggers" | Rule 6 *Evidence Tiers* carries the normative minimum assignment E1/E2/E3; the Rule-6 pointer line reads "Format and illustrative tier examples"; guide §12/§12.1 mark the table as illustrative (column `Illustrative example (assignment: Rule 6)`, Rule 6 decides on divergence) | contract, guide, this document §5/§6 |
| F-167-02 | CHANGELOG: "No consumer action is required."; §3 row 8: "none required beyond the CHANGELOG statement 'no consumer action is required'" | CHANGELOG and §3 row 8 separate (1) no mandatory tooling or runtime migration, (2) prospective application of the new evidence requirements by consumers adopting the updated rules, (3) historical records valid under the rules applicable when authored | CHANGELOG, this document §3 |

### 13.2 ADR-0031 re-check

Documentary rule check against [ADR-0031](../../adr/ADR-0031-v1x-compatibility-policy.md), re-read in CP01:

- Stable Candidate *Work-Package-Flow und Review-Entscheidungswert*: unchanged; `REWORK` is reused with its existing meaning. Role boundaries and Human-Maintainer release control: unchanged.
- Retroactive effect: none; historical records stay valid under their authoring-time rules.
- Future evidence requirements become stricter for consumers adopting the updated rules — disclosed, prospective, and invalidating no existing artefact.
- *Migration Notes:* where a change affects users, ADR-0031 expects a short migration note in the changelog or release notes. The corrected CHANGELOG statement is that note; the original "no consumer action" wording omitted the prospective obligation.
- No ADR-governed policy, Public Quality Gate expectation, or skill-security rule changes; no additional ADR or governance path is needed.

**Result:** `ADDITIVE WITH PROSPECTIVE TRANSITION` holds after the re-check; no breaking change and no additional ADR need found. Limits: no consumer behaviour test was run; actual consumer adoption is not verified; this is the implementing agent's documentary check — Nova's review is the independent one.

### 13.3 Documentary re-check of the test matrix

Method as in §7: documentary rule check against the CP01 text; no behaviour test.

| ID | CP01 re-check | Rule check | Behaviour test |
|---|---|---|---|
| T03 | Rule 6 assigns E1 to a "minor, non-normative change without relevant … risk"; §12.1 E1 example (typo, link fix) and its "Not required" column are unchanged | PASS | no |
| T04 | Rule 6 assigns "relevant normative … effect" to E3 directly; under-declaration → `REWORK` unchanged | PASS — residual uncertainty reduced; "relevant" stays a judgement | no |
| T13 | *Prospective transition* bullet byte-unchanged; CHANGELOG states that historical records remain valid | PASS | no |
| T16 | Rule 6 assigns E2 to a "normal work package or bounded correction" without E3 factor; derivation rule unchanged | PASS | no |
| T17 | *Proportionality* byte-unchanged; the E3 assignment names "elevated integrity effect", not append-only as such; the §12.1 E3 example lists no append-only case | PASS | no |
| T18 | *Proportionality* and the §12.1 E2 "Not required" column unchanged; CHANGELOG: no mandatory tooling migration | PASS | no |

T01, T02, T05–T12, T14, T15, T19, T20: their Rule-6 bullets are byte-unchanged by CP01 (§13.5); no contradiction introduced. Summary: 6/6 re-checked PASS, 14 unaffected; behaviour test executed: no.

### 13.4 Quality gates (CP01 run 1)

Source class: direct tool output. 2026-11-03, 11:30:33–11:30:34 UTC; Git Bash 5.3.15, Python 3.13.17; each exit status read via `$?` directly after the command; output redirected to a file outside the repository; no pipeline. Run after the CP01 edits to the contract, the guide, the CHANGELOG, and §3/§5/§6/§7 of this document; before this §13 and the notes addendum.

| Gate | Exit code | Output | Errors / warnings / notices |
|---|---|---|---|
| `python scripts/check_public_quality.py --self-test` | `0` | `self-test passed` | – |
| `python scripts/check_public_quality.py --strict` | `0` | `Public quality gate passed.` | 0 / 0 / 4 |
| `git diff --check` | `0` | – | – |

Notices: scan mode tracked + new/untracked; 40 new text files in scan (38 `.agents/skills/` files and the two new WP-167 files); no custom denylist configured. **Denylist configured: no** (presence checked at process, user, and machine level and for the local file; no value read). A local PASS is no complete neutrality evidence and no CI result. The confirmation run after this §13 and the notes addendum is in the closing report to Nova.

### 13.5 Scope and integrity

Comparison basis: SHA-256 of the five CP01 targets, taken in this session before the first CP01 write; they reproduce the after-values of the original WP-167 closing report.

| File | SHA-256 before CP01 | SHA-256 after CP01 |
|---|---|---|
| `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md` | `bb26b455ad59ce91d35fbdacdb8d1142742fffd6fda3bcec54935497cad91f4c` | `ee3443279d3f1776cfb7bea72b86366d033f2061b07cb3c294e1d8b700738331` |
| `docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md` | `24c8a036caad474bb3390ced7fe2109fe68ca73a90c320eb500b637f0a747b16` | `b5800c362cab98801ef7eac2e2f278f474edd6a8555f81f0efa3b8d5254b80b2` |
| `CHANGELOG.md` | `cd96231b41c25a0426fe9a78ba8894c77ec457d76676cc6a0bcf1a4eb7a8a5c3` | `fbdf4f12be55456715080991bfcadbbae8f23e32a9319cbf9b05891b2591ee34` |
| this document, WP-167 notes | `9ac0955e…a8ea`, `a2f73e2e…8228` | closing report to Nova (self-reference) |

- **Contract:** reversing the two CP01 replacements reproduces the before-hash byte-exactly. The part from the start up to `## Rule 6` (metadata, execution header, Rules 1–5) and the `## Authority and fail-closed` section hash identically before and after.
- **Guide:** everything before `## 12.` and from `## 13.` hashes identically before and after.
- **CHANGELOG:** all lines except the WP-167 line hash identically; that hash also equals the pre-WP-167 value in §9.
- **Line endings:** all five targets are LF-only before and after. One interim CRLF conversion of the contract during CP01 (an agent error) was reverted in the same session before any further edit; the reconstruction proof above covers the final bytes.
- Excluded WP-167 files, `.agents/`, and protected areas: compared in the closing report to Nova.

### 13.6 Open notes

- **N-CP01-01:** the WP-167 CHANGELOG line still says the guide §12 "carries the format and tier triggers". CP01 authorised only the migration-statement correction in the CHANGELOG, so this descriptive wording stays; it is no normative source. A wording alignment needs a separate Human-Maintainer decision.
- "Relevant" in the E1/E3 assignment stays a judgement; doubt is resolved by the highest risk factor.
- No agent-behaviour, cross-host, or consumer test; skill alignment (D-11) and G-14 (D-7) stay separate.

### 13.7 Status

F-167-01 and F-167-02: `CORRECTED – PENDING NOVA REVIEW`. CP01: `READY_FOR_NOVA_REVIEW`. Nova review, Human-Maintainer acceptance, commit, and push are pending; this document declares no GO and no acceptance.
