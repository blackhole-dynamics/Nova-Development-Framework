# Post-v1.1 Candidate Roadmap

> Work Package: `NDF-WP-170` — Post-v1.1 Status & Roadmap Reconciliation
> Stand: 2026-11-03 · Repository-Revision bei Erstellung: `main` @ `24760c4`
> Kennungen und Status: [NDF_WORK_PACKAGE_ID_REGISTER.md](NDF_WORK_PACKAGE_ID_REGISTER.md) · Abgeschlossener Zyklus: [V1_1_PLAN.md](V1_1_PLAN.md)

## DE – 1. Ziel und Status

**Status: laufende Kandidatenplanung — kein Scope Lock, kein aktivierter Entwicklungszyklus.** Dieses Dokument sammelt die nach `v1.1.0` vorgemerkten Kandidaten, ihre Prioritäten und Abhängigkeiten, damit der Human Maintainer das nächste Work Package bewusst auswählen kann. Es aktiviert kein Work Package und autorisiert keine Implementierung. Erstellt im Rahmen von WP-170; WP-170 ist nicht angenommen.

## DE – 2. Abgrenzung vom abgeschlossenen v1.1-Zyklus

- Der v1.1-Zyklus (WP-151…159) ist abgeschlossen; `v1.1.0` ist veröffentlicht (2026-09-23, Human-Maintainer-Entscheidung `GO_WITH_NOTES`). [V1_1_PLAN.md](V1_1_PLAN.md) bleibt das historische Dokument dieses Zyklus und wird nicht fortgeschrieben.
- Die acht v1.1.0-Known-Limitations gelten unverändert ([Release Notes](../release/V1_1_0_RELEASE_NOTES.md)); diese Roadmap löst keine davon auf.
- Seit `v1.1.0` wurde auf `main` u. a. WP-169 (Prompt Execution Contract Hardening) angenommen und committed (`24760c4`). Das ist kein Release.

## DE – 3. Kein v1.2-Scope-Lock

- Kein v1.2-Scope-Lock, keine v1.2-Release-Entscheidung, keine Release-Vorbereitung.
- Ob und wann Kandidaten in einen v1.2-Zyklus münden, entscheidet ausschließlich der Human Maintainer in einem eigenen Schritt.
- Alle Änderungen bleiben an [ADR-0031](../adr/ADR-0031-v1x-compatibility-policy.md) (v1.x-Kompatibilität) und [ADR-0032](../adr/ADR-0032-skill-security-policy.md) (Skill Security) gebunden.

## DE – 4. Angenommene Planungsentscheidungen

Vom Human Maintainer getroffen, hier nur aufgezeichnet:

| ID | Entscheidung |
|---|---|
| I-1 | WP-160 bleibt `RESERVED – HISTORICAL ALLOCATION UNRESOLVED`; keine rückwirkende Zuordnung zur README-Modernisierung |
| I-2 | WP-162…168 strategisch vorgemerkt, nicht aktiviert; Reihenfolge darf von der Nummerierung abweichen |
| I-3 | Nummerierungsregel (siehe [Register §7](NDF_WORK_PACKAGE_ID_REGISTER.md)) |
| I-4 | Laufende Post-v1.1-Kandidatenplanung; kein v1.2-Scope-Lock; keine Release-Entscheidung; keine automatische Zyklusaktivierung |
| I-5 | `.claude/skills/` bleibt der getrackte Skillbestand; `.agents/skills/` bleibt lokal und untracked; Multi-Host-/Parity-Strategie offen; vier bekannte Unterschiede als Risikohinweis |
| I-6 | Kandidatenzuschnitt (siehe §5) |
| I-7 | v1.1.0-Post-Release-Review als eigenständiges späteres Vorhaben, ohne automatische WP-ID |
| I-8 | ADR-0033 weiter aufgeschoben |
| I-9 | GitHub-Actions-Wartung als getrenntes Vorhaben; Node-20-Deprecation-Warnung nicht blockierend |
| I-10 | Annahmestatus zweier Governance-Guidances bleibt offen |

## DE – 5. Kandidatenübersicht

Alle Kandidaten haben den Status `RESERVED CANDIDATE – NOT ACTIVATED`. Jeder Kandidat braucht vor einer Ausführung einen eigenen, vollständigen, Human-Maintainer-autorisierten Ausführungsvertrag ([Execution Contract](../../framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md)).

### WP-162 – Machine-Readable Work Package Contract (verkleinert)

- Nur eine **optionale, abgeleitete Projektion** bestehender Regeln (z. B. eine maschinenlesbare Sicht auf Header-Felder und Allowlists).
- Markdown und der bestehende Execution Contract bleiben führend; die Projektion ist nie normative Quelle.
- Durch diese Planung **nicht** autorisiert: Validator, Parser, Schema-Pflicht, neue Runtime oder Tooling.

### WP-163 – Compliance Model (nicht eigenständig)

- Kein eigenständiges aktives WP. Mögliche Zusammenführung mit WP-164 im Sinne **projektinterner NDF-Konformität** (wie weit folgt ein Projekt den NDF-Regeln).
- Keine externe Zertifizierungs-, Audit- oder regulatorische Compliance-Behauptung.

### WP-164 – Adoption / Governance Tiers

- Kandidat für eine risikobasierte Anpassung des Governance-Umfangs an Projektgröße und Risiko.
- Keine Lockerung von Human-Maintainer-Gates, ADR-0031, ADR-0032, Security, Public Neutrality oder Fail-Closed. Tiers dürfen nur den Dokumentationsumfang staffeln, nie Kontrollrechte.

### WP-165 – Independent Validation Kit und späterer externer Lauf

Zwei getrennte Schritte:

- **WP-165 (Kit):** Vorbereitungskit für eine unabhängige Validierung (Anleitung, Fixture-Anforderungen, Erfassungsformat), aufbauend auf bestehenden Runbooks.
- **Späterer externer Lauf:** Durchführung durch eine tatsächlich unabhängige Partei. Agentengenerierte Evidenz ersetzt diesen Lauf nicht; nur er kann die G-13-Unabhängigkeitsfrage adressieren.

### WP-166 – Benchmark Specification (DEFERRED)

- Zurückgestellt (`DEFERRED`). Ein Benchmark-Vorhaben wird erst dann sinnvoll konkretisiert, wenn ausreichende reale, nachvollziehbare und reproduzierbare Mess- bzw. Validierungsevidenz vorliegt.
- Ein externer Lauf aus WP-165 kann relevante Evidenz beitragen, ist aber keine generell zwingende Voraussetzung für WP-166.
- Eine spätere Aktivierung von WP-166 erfordert einen gesonderten Human-Maintainer-autorisierten Ausführungsvertrag.

### WP-167 – Execution Evidence Hardening (P1)

- Bestehende Evidence-Pack-Strukturen verbessern (Validierungsdokumente, WP-Notes, Quality-Gate-Erfassung, Vorher-/Nachher-Nachweise).
- Keine zweite, parallele normative Contract-Quelle; der Execution Contract bleibt die einzige normative Quelle für Ausführungsregeln.
- Evidenzanforderungen nach Risiko und Prüfbarkeit staffeln (z. B. Exit-Codes direkt erfassen, Hash-Baselines vor Schreibvorgängen, klare Trennung dokumentarischer Prüfung und ausgeführter Verhaltenstests).

### WP-168 – Skills Parity & Integrity Reconciliation (P1)

- Zuerst die Unterschiede zwischen `.claude/skills/` und `.agents/skills/` klassifizieren, danach über Parity entscheiden.
- Keine automatische Gleichsetzung verschiedener Host-Artefakte; keine neue Host-Pflicht.
- Keine automatische Änderung der 38 untracked Dateien; jede Änderung braucht einen eigenen autorisierten Vertrag.

### Weitere Vorhaben ohne WP-ID

Nicht automatisch aktiviert; eine WP-ID wird erst bei Bedarf durch den Human Maintainer vergeben:

- **CI-Actions-Wartung:** `actions/checkout@v4`, `actions/setup-python@v5`, gegebenenfalls Runner-Pinning (`ubuntu-latest`). Zielversionen erst nach eigenständiger Prüfung und Freigabe.
- **v1.1.0-Post-Release-Review:** eigenständiges späteres Vorhaben.
- **ADR-0033:** weiter aufgeschoben (Skill-Nutzung in privaten Consumer-Projekten).
- **Klärung der zwei Governance-Guidance-Annahmestatus:** Human-Maintainer-Entscheidung.

## DE – 6. Prioritäten

| Priorität | Kandidat | Grundlage |
|---|---|---|
| P1 | WP-167 Execution Evidence Hardening | Human-Maintainer-Entscheidung I-6 |
| P1 | WP-168 Skills Parity & Integrity Reconciliation | Human-Maintainer-Entscheidung I-6 |
| offen (weiterplanen) | WP-164 Adoption / Governance Tiers (ggf. inkl. WP-163) | I-6; keine Priorität festgelegt |
| offen (weiterplanen) | WP-165 Kit; externer Lauf separat | I-6; keine Priorität festgelegt |
| offen (verkleinert) | WP-162 | I-6; keine Priorität festgelegt |
| DEFERRED | WP-166 | I-6 |
| nicht eigenständig | WP-163 | I-6 |

Nur P1 und DEFERRED sind entschieden. Alle übrigen Einstufungen sind Planungsstand, keine Priorisierung durch den Agenten.

## DE – 7. Abhängigkeitsmatrix

| Kandidat | Hängt ab von | Liefert an | Art |
|---|---|---|---|
| WP-167 | Execution Contract (WP-153/169) | WP-162, WP-164, WP-165 | empfohlen, nicht zwingend |
| WP-168 | Human-Maintainer-Entscheidung zur Multi-Host-Strategie (für den Parity-Teil); ADR-0032; [Provenance & Integrity Lock](../agent-workflows/NDF_SKILL_PROVENANCE_AND_INTEGRITY_LOCK.md) | — | Klassifikation ohne Vorbedingung möglich |
| WP-164 | WP-163 (Zusammenführung); profitiert von WP-167 | — | empfohlen |
| WP-165 Kit | profitiert von WP-167 (Erfassungsformat) | externer Lauf | empfohlen |
| Externer Lauf | WP-165 Kit; unabhängige Partei | ggf. Evidenz für WP-166 | Vorbedingungen zwingend; Evidenzbeitrag zu WP-166 optional |
| WP-166 | ausreichende reale, reproduzierbare Evidenz (ein externer WP-165-Lauf kann beitragen, ist aber nicht zwingend) | — | Evidenzanforderung zwingend |
| WP-162 | WP-167; stabiler Execution Contract | — | empfohlen |
| CI-Wartung | keine | — | unabhängig |
| Post-Release-Review | keine | ggf. Priorisierung | unabhängig |

## DE – 8. Risiken und offene Evidenz

- **Skill-Abweichungen:** Vier `SKILL.md` unter `.agents/skills/` weichen von `.claude/skills/` ab (`ndf-compact-context-summary-runner`, `ndf-context-pack-maintainer`, `ndf-skill-quality-reviewer`, `ndf-skill-trigger-quality-reviewer`). Keine historische Hash-Baseline vor WP-169; Consumer-Locks mit früheren Digests nicht ausgeschlossen.
- **G-13** bleibt `MATERIALLY_REDUCED`, nicht geschlossen; erst ein unabhängiger externer Lauf kann die Unabhängigkeit adressieren.
- **Single-Maintainer-Engpass** begrenzt Review- und Annahmekapazität.
- **Lokale Neutralitätsprüfung ohne Denylist:** lokal kein Nachweis; der CI-Lauf mit konfigurierter Denylist ist maßgeblich.
- **CI-Wartung:** Node-20-Deprecation-Warnung (nicht blockierend); Zielversionen ungeprüft.
- **Governance-Guidances:** fachlicher Annahmestatus offen (I-10).
- **Agentenverhalten:** Die WP-169-Regeln sind dokumentarisch geprüft, nicht durch ausgeführte Verhaltens- oder Cross-Host-Tests.
- **Scope-Drift:** Kandidaten dürfen nicht durch Erwähnung in Context Packs oder Handoffs als aktiviert gelten.

## DE – 9. Next-Phase-Empfehlung

1. Unabhängiges Nova-Review von WP-170.
2. Human-Maintainer-Entscheidung über WP-170 sowie Staging, Commit und Push.
3. Danach Auswahl des nächsten Work Packages durch den Human Maintainer. Empfehlung (nicht entschieden): einer der P1-Kandidaten WP-167 oder WP-168, jeweils mit eigenem vollständigem Vertrag; CI-Wartung als getrenntes Vorhaben.

Details: [NEXT_PHASE_POST_V1_1.md](../../project-brain/NEXT_PHASE_POST_V1_1.md).

## DE – 10. Nichtziele

- Keine Aktivierung von WP-162…168; keine Implementierung, kein Tooling, keine Runtime, keine Integration.
- Kein v1.2-Scope-Lock, keine Release-Vorbereitung, keine Release-Aussage.
- Keine Änderung an ADRs, Execution Contract, Templates, Skills, Workflows oder Scripts.
- Keine neue universelle NDF-Pflicht, keine neue Host-Pflicht.
- Keine Abhängigkeit von externen Projekt- oder Ecosystem-Produkten.
- Keine externe Zertifizierungs- oder Compliance-Behauptung.

## EN – Summary

**Status: running candidate planning — no scope lock, no activated development cycle, no v1.2 release decision.** The v1.1 cycle (WP-151…159) is closed and `v1.1.0` is published; [V1_1_PLAN.md](V1_1_PLAN.md) stays historical.

| Candidate | Planning state |
|---|---|
| WP-162 Machine-Readable Work Package Contract | reduced; optional derived projection only; Markdown and the Execution Contract stay authoritative; no validator, parser, or runtime authorised |
| WP-163 Compliance Model | not standalone; may merge into WP-164 as project-internal NDF conformance; no external certification claim |
| WP-164 Adoption / Governance Tiers | candidate; no weakening of Human-Maintainer gates, ADR-0031/0032, security, neutrality, or fail-closed |
| WP-165 Independent Validation Kit | kit and a later genuinely independent external run planned separately; agent evidence cannot replace the run |
| WP-166 Benchmark Specification | deferred until real, reproducible evidence exists |
| WP-167 Execution Evidence Hardening | P1; improve existing evidence structures; no second normative contract source |
| WP-168 Skills Parity & Integrity Reconciliation | P1; classify differences first, then decide on parity; no automatic change to `.agents/skills/` |

None of these is activated. Further items without an ID: CI actions maintenance, a v1.1.0 post-release review, ADR-0033 (deferred), and the open acceptance status of two governance guidances. Next step: Nova review of WP-170, then the Human Maintainer's decision.
