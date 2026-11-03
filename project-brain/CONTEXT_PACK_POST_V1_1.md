# Context Pack – Post-v1.1

> Kompakter Snapshot nach NDF-WP-169 (erstellt in NDF-WP-170). Ersetzt keine Prüfung der aktuellen Dateien, keinen Public Quality Gate und keine Human-Maintainer-Entscheidung. Historische Context Packs (z. B. [Foundation 0.9](CONTEXT_PACK_FOUNDATION_0_9.md)) bleiben unverändert.

## Status

Datum: 2026-11-03 · Revision: `main` @ `24760c4315a02e26d61b17cc43eece56e52579d9` (= `origin/main`) zuzüglich der nicht committeten WP-170-Dokumente · Phase: Post-v1.1-Kandidatenplanung, **kein Scope Lock, kein aktiver Zyklus**.

## Baseline

- **NDF v1.1.0** veröffentlicht (Tag `v1.1.0` → `948c91d`, GitHub-Release „Latest“, 2026-09-23, `GO_WITH_NOTES`). v1.x-Zusage aktiv (ADR-0031). Acht Known Limitations unverändert ([Release Notes](../docs/release/V1_1_0_RELEASE_NOTES.md)).
- **WP-151…159** abgeschlossen.
- **WP-169** `ACCEPTED WITH NOTES` (CP01 `ACCEPTED`), committed und gepusht als `24760c4`; GitHub „Public Quality Gate“ `success`; kein Release. Die WP-169-Regeln gelten prospektiv ab der Human-Maintainer-Annahme.
- **WP-170** Human-Maintainer-autorisiert (docs-only, Sieben-Pfad-Allowlist); **nicht angenommen** bis zur Human-Maintainer-Entscheidung nach dem Nova-Review.

## Governance-Grundlagen

- [Execution Contract](../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (WP-153, gehärtet durch WP-169; Rules 1–5).
- [Token Efficiency & Context Budget Baseline](../docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) (WP-152).
- [ADR-0031](../docs/adr/ADR-0031-v1x-compatibility-policy.md) v1.x-Kompatibilität · [ADR-0032](../docs/adr/ADR-0032-skill-security-policy.md) Skill Security. Nächste freie ADR-Nummer: ADR-0033 (weiter aufgeschoben).
- Human-Maintainer-Autorität · Standalone-First · Hostneutralität · öffentliche, projektneutrale Dokumentation.

## Planung

- WP-ID-Status: [NDF_WORK_PACKAGE_ID_REGISTER.md](../docs/roadmap/NDF_WORK_PACKAGE_ID_REGISTER.md) (WP-160 reserviert/ungeklärt; WP-162…168 vorgemerkt, nicht aktiviert; keine automatische ID-Vergabe).
- Kandidaten, Prioritäten, Abhängigkeiten: [POST_V1_1_CANDIDATE_ROADMAP.md](../docs/roadmap/POST_V1_1_CANDIDATE_ROADMAP.md).
- Priorisiert (P1, nicht aktiviert): WP-167 Execution Evidence Hardening · WP-168 Skills Parity & Integrity Reconciliation. WP-166 DEFERRED; WP-163 nicht eigenständig.
- Ohne WP-ID: CI-Actions-Wartung · v1.1.0-Post-Release-Review · ADR-0033 · Annahmestatus zweier Governance-Guidances.

## Offene Human-Maintainer-Entscheidungen

1. Annahme von WP-170 (nach Nova-Review) sowie Staging, Commit und Push.
2. Auswahl und Autorisierung des nächsten Work Packages.
3. Multi-Host-/Parity-Strategie für `.claude/skills/` und `.agents/skills/`.
4. Fachlicher Annahmestatus von `NDF_DECISION_AND_STATUS_MODELING_GUIDANCE.md` und `NDF_EXTERNAL_FRAMEWORK_TAILORING_GUIDANCE.md` (Statusfeld `Implemented, pending Nova review`; Commit `ebf716c` belegt nur die Aufnahme).
5. Zeitpunkt der CI-Wartung und des v1.1.0-Post-Release-Reviews.

## Integritäts- und Evidenzgrenzen

- 38 untracked `SKILL.md` unter `.agents/skills/`; vier weichen von `.claude/skills/` ab (`ndf-compact-context-summary-runner`, `ndf-context-pack-maintainer`, `ndf-skill-quality-reviewer`, `ndf-skill-trigger-quality-reviewer`). Keine historische Hash-Baseline vor WP-169.
- Consumer-Locks mit früherem Summary-Runner-Digest nicht ausgeschlossen (WP-169-Note).
- WP-169-Tests: 17/17 dokumentarisch PASS, Agentenverhalten 17/17 `NOT_VERIFIABLE`.
- Lokale Quality Gates laufen ohne Neutralitäts-Denylist; maßgeblich ist der CI-Lauf.
- G-13 `MATERIALLY_REDUCED`, nicht geschlossen; Single-Maintainer-Engpass.

## Handoff Freshness (Rule 5)

Vor jeder Wiederaufnahme auf Basis dieses Context Packs:

1. `git rev-parse HEAD` und `git rev-parse origin/main` mit der oben genannten Revision vergleichen; bei Abweichung prüfen, was sich geändert hat und ob es Dateien, Quellen oder Annahmen des aktiven Vertrags berührt.
2. Prüfen, ob der referenzierte Vertrag noch aktuell ist (nicht ersetzt, zurückgezogen oder widersprochen).
3. Prüfen, ob WP-170 inzwischen angenommen, nachgebessert oder gestoppt wurde, und den tatsächlichen Stand aus Git und den WP-170-Notes übernehmen.
4. Materielle Abweichung → `BLOCKED` mit Bericht; sonst fortfahren und die Prüfung festhalten.

## What Must Not Be Claimed

Keine Annahme von WP-170 · keine Aktivierung von WP-162…168 · kein v1.2-Scope-Lock · keine Release-Aussage · keine Annahme der zwei Governance-Guidances · keine Parity zwischen `.claude/skills/` und `.agents/skills/`.

## Quellen

[WP-169-Notes](WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md) · [WP-169-Validierung](../docs/validation/context-economy/PROMPT_EXECUTION_CONTRACT_HARDENING.md) · [WP-170-Notes](WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md) · [Next Phase](NEXT_PHASE_POST_V1_1.md) · [V1_1_PLAN.md](../docs/roadmap/V1_1_PLAN.md) (historisch).
