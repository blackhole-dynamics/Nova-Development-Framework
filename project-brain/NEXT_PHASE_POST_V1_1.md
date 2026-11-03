# Next Phase – Post-v1.1

> Handoff nach NDF-WP-170. Stand: 2026-11-03 · Revision: `main` @ `24760c4` (= `origin/main`) zuzüglich der nicht committeten WP-170-Dokumente. Historische Next-Phase-Dokumente bleiben unverändert.

## Current status

- `v1.1.0` veröffentlicht (2026-09-23, `GO_WITH_NOTES`); v1.x-Zusage aktiv (ADR-0031).
- WP-169 `ACCEPTED WITH NOTES`, committed `24760c4`, gepusht, CI „Public Quality Gate“ `success`; kein Release.
- WP-170 durch den Agenten ausgeführt; Ergebnis **nicht angenommen**. Agentenstand und Evidenz: [WP-170-Notes](WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md).
- Kein aktiver Entwicklungszyklus, kein v1.2-Scope-Lock.

## Governance baseline

[Execution Contract](../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md) (WP-153 + WP-169, Rules 1–5) · [Token Efficiency & Context Budget Baseline](../docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md) (WP-152) · [ADR-0031](../docs/adr/ADR-0031-v1x-compatibility-policy.md) · [ADR-0032](../docs/adr/ADR-0032-skill-security-policy.md) · Human-Maintainer-Autorität · Standalone-First · Hostneutralität · Public Neutrality.

## Open review and decision for WP-170

1. **Nova (ChatGPT) – die ChatGPT-basierte Planungs-, Architektur- und Review-Rolle** prüft WP-170 unabhängig und gibt ein Votum ab.
2. Erst danach entscheidet der **Human Maintainer**: `ACCEPTED` · `ACCEPTED WITH NOTES` · `REWORK_REQUIRED` · `STOP` sowie über Staging, Commit und Push.

Bis dahin gelten die WP-170-Dokumente als Implementierung ohne Annahme.

## Sequence of follow-up work

1. Nova-Review WP-170.
2. Human-Maintainer-Entscheidung zu WP-170 und Git-Aktionen.
3. Human-Maintainer-Auswahl des nächsten Work Packages. Empfehlung (nicht entschieden): WP-167 oder WP-168 (beide P1), jeweils mit eigenem vollständigem Vertrag.
4. Getrennt und unabhängig davon: CI-Actions-Wartung, v1.1.0-Post-Release-Review, Klärung der Governance-Guidance-Status — jeweils nur nach eigener Human-Maintainer-Freigabe.

## Explicitly not activated

WP-162 · WP-163 · WP-164 · WP-165 (Kit und externer Lauf) · WP-166 (DEFERRED) · WP-167 · WP-168 · ADR-0033 · CI-Wartung · Post-Release-Review. Eine Erwähnung in diesem Dokument ist keine Aktivierung. WP-160 bleibt reserviert und darf nicht vergeben werden.

## Prerequisites for a later WP-167 / WP-168 execution

Gemeinsam:

- eigener, vollständiger, Human-Maintainer-autorisierter Vertrag mit Execution Header (`SESSION`, spezifischer `SESSION REASON`, deutscher Session-Hinweis), exakter Schreib-Allowlist, STOP-Bedingungen und Abnahmekriterien;
- angenommener (oder ausdrücklich anders entschiedener) Stand von WP-170;
- Rule-5-Freshness-Prüfung vor Beginn (siehe unten);
- Vorher-Hashes aller Schreibziele und relevanter ausgeschlossener Dateien vor dem ersten Schreibvorgang.

WP-167 zusätzlich: Festlegung, welche bestehenden Evidence-Strukturen im Scope sind; keine zweite normative Contract-Quelle; keine neuen Tools oder Runtime ohne gesonderte Freigabe.

WP-168 zusätzlich: lesende Klassifikation der Unterschiede vor jeder Änderung; ausdrückliche Entscheidung, ob `.agents/**` überhaupt Schreibziel sein darf; Bezug auf ADR-0032 und den [Provenance & Integrity Lock](../docs/agent-workflows/NDF_SKILL_PROVENANCE_AND_INTEGRITY_LOCK.md); keine neue Host-Pflicht.

## CI maintenance (separate)

Betroffen: `actions/checkout@v4`, `actions/setup-python@v5`, gegebenenfalls Runner-Pinning (`runs-on: ubuntu-latest`) in `.github/workflows/public-quality-gate.yml`. Die Node-20-Deprecation-Warnung ist nicht blockierend. Zielversionen werden erst nach eigenständiger Prüfung und Freigabe festgelegt; dieses Dokument nennt keine.

## No release authority

Weder WP-170 noch dieses Dokument begründen einen Release, eine Release-Vorbereitung oder einen Tag. Release-Entscheidungen trifft ausschließlich der Human Maintainer.

## Rule 5 freshness check before resumption

Vor jeder Wiederaufnahme auf Basis dieses Handoffs, lesend:

1. **Revision:** `git rev-parse HEAD` und `git rev-parse origin/main` gegen `24760c4315a02e26d61b17cc43eece56e52579d9` prüfen. Eine neue Revision ist nicht automatisch `BLOCKED`: festhalten, was sich geändert hat (`git log --oneline 24760c4..HEAD`), und prüfen, ob die Änderung Dateien, Quellen oder Annahmen des aktiven Vertrags berührt.
2. **Arbeitsbaum:** `git status --short --untracked-files=all`, `git diff --cached --name-only` (leer erwartet); bekannte 38 untracked `.agents/skills/`-Dateien gesondert ausweisen.
3. **Vertrag:** Ist der aktive Vertrag noch aktuell (nicht ersetzt, zurückgezogen oder widersprochen)? Ersetzt → nur den aktuellen `COMPLETE REPLACEMENT` ausführen.
4. **WP-170-Stand:** angenommen, nachgebessert oder gestoppt? Den tatsächlichen Stand aus Git und den WP-170-Notes übernehmen, nicht aus diesem Dokument ableiten.
5. **Ergebnis:** materielle Abweichung → STOP / `BLOCKED` mit Bericht; sonst fortfahren und die Prüfung im Ergebnis festhalten.

## Session classification for the next step

`SESSION: NEW_SESSION_REQUIRED` · `SESSION REASON:` Das nächste Work Package erhält einen eigenen Human-Maintainer-Vertrag mit neuer Allowlist; Schreibrechte aus WP-170 werden nicht übernommen. · Neue Session nötig? Ja – neue Session erforderlich.
