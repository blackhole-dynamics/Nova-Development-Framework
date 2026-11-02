# NDF-WP-169 – Prompt Execution Contract Hardening (Notes)

> Status: **Implementierung abgeschlossen; Corrective Pass CP01 (nur Dokumentation und Evidenz) ausgeführt; Nova-Re-Review und Human-Maintainer-Annahme ausstehend.** Validation: [PROMPT_EXECUTION_CONTRACT_HARDENING.md](../docs/validation/context-economy/PROMPT_EXECUTION_CONTRACT_HARDENING.md)

## WP / Baseline

`NDF-WP-169 – Prompt Execution Contract Hardening` (docs-only, Full, B3). Start-Revision `4dab503` auf `main`; Index leer; keine getrackten Änderungen; 38 untracked `SKILL.md` unter `.agents/skills/` als bekannte, nicht normative Ausgangslage. Basis: NDF v1.1.0, ADR-0031, ADR-0032, WP-152/153/154.

## Autorisierung

Human-Maintainer-autorisierter Ausführungsvertrag (`STATUS: COMPLETE REPLACEMENT`, 2026-11-02) mit fester Elf-Datei-Allowlist; Git-Schreibaktionen und Release ausgeschlossen.

- **Option C:** Execution Header strukturell unverändert; deutscher Session-Hinweis als separate Zeile; `SESSION REASON` bleibt eigenes Feld.
- **O-1:** deutscher Hinweis verpflichtend, englisch optional. **O-2:** keine neuen Fehlercodes. **O-3:** keine neuen Handoff-Statuscodes. **O-4:** keine Skript-Kommentarpflicht. **O-5:** keine Roadmap-Änderung. **O-6:** Validierung unter `docs/validation/context-economy/`.

## Ausgeführte Änderungen

- `BLOCK_EXECUTION_CONTRACT.md`: Begründung für alle vier Session-Werte (pauschal → REWORK), Hinweistabelle, Entscheidungshilfen ohne Host-Annahmen, prospektiver Übergang; Rule 3 mit Session-Neubewertung, fehlendem `SUPERSEDES` → REWORK und Schutz vor stiller Scope-Erweiterung; neue Rule 5 – Handoff Freshness.
- Templates LEAN_WP / FIX / REVIEW_ONLY / SESSION_HANDOFF, Execution-Header-Abschnitte in `NDF_PROMPT_MODES.md` (DE/EN), Eintrag in `PROMPT_INDEX.md`.
- `ndf-compact-context-summary-runner`: nur die Next-step-/Handoff-Regel (aktiver Vertrag, Begründung + Hinweis).
- `CHANGELOG.md` `[Unreleased]`, Validierungsdokument, diese Notes.

## Evidenz

Testmatrix T01–T17: dokumentarische Regelprüfung 17/17 PASS, Agentenverhalten 17/17 `NOT_VERIFIABLE` (kein ausgeführter Verhaltens- oder Cross-Host-Test). Public Quality Gate self-test + strict im ursprünglichen Lauf als bestanden gemeldet; die Python-Exit-Codes wurden dabei wegen einer Shell-Pipeline nicht zuverlässig erfasst und die Strict-Notices nicht vollständig dokumentiert (in CP01 neu ausgeführt, siehe unten); `git diff --check` sauber; Index leer; Links aufgelöst; ADR-0031/0032 unverändert.

## Offene Einschränkungen

- Skill-Integrität (bedingt): Der Inhalt des Summary-Runners wurde geändert; sein Arbeitsbaum-Digest weicht vom Digest vor WP-169 ab. Ein Consumer-Lock oder gespeicherter Digest, der den früheren Inhalt referenziert, würde bei erneuter Prüfung eine Abweichung melden. Ob solche Consumer existieren, ist nicht nachgewiesen; eine konkrete Integritätsverletzung ist nicht bekannt. Falls vorhanden: kontrollierte Neuverifikation gegen den Human-Maintainer-Commit. Keine automatische Lock-Aktualisierung.
- `ndf-work-package-runner` nennt Hinweis und Rule 5 nicht (außerhalb des Scopes; kein Widerspruch, da Verweis auf den Contract).
- `.agents/skills/` (außerhalb des WP-169-Scopes): untracked Kopie des Summary-Runners ist bytegleich mit der HEAD-Fassung und weicht damit jetzt von `.claude/skills/` ab (vierte bekannte Abweichung). Durch CP01 nachweislich nicht verändert (Vorher-/Nachher-SHA-256); die Unverändertheit während der ursprünglichen WP-169-Ausführung ist mangels Vorher-Hashes nicht bewiesen, nur mit den Beobachtungen vereinbar.
- Historische WP-153-Dokumente beschreiben die frühere `SAME_SESSION_ALLOWED`-Ausnahme korrekt als damaligen Stand.

## Abschlussstatus

Ursprünglicher Durchlauf: `AGENT_COMPLETE` — kein `HUMAN_APPROVED`, kein Commit, kein Release. Die WP-169-Pflichten gelten erst ab formeller Human-Maintainer-Annahme. Damaliges Votum an Nova: `READY_FOR_NOVA_REVIEW`; Nova-Votum darauf: `REWORK_REQUIRED – DOCUMENTATION & EVIDENCE ONLY` (normativer Teil ohne Änderungsbedarf).

## Corrective Pass CP01 (2026-11-02)

- **Anlass:** Nova-Votum `REWORK_REQUIRED – DOCUMENTATION & EVIDENCE ONLY` nach Prüfung des Evidence Packs.
- **Autorisierung:** gesonderter Human-Maintainer-autorisierter CP01-Vertrag (`STATUS: COMPLETE REPLACEMENT`, neue Session), nur Dokumentation; Schreib-Allowlist ausschließlich `CHANGELOG.md`, das Validierungsdokument und diese Notes; keine Git-Schreibaktionen. Die frühere Elf-Datei-Allowlist galt für CP01 nicht.
- **Bearbeitete Befunde:** F-169-01 (`.agents/skills/`-Aussage auf belegbare Beobachtungen und Beweisgrenzen präzisiert), F-169-02 (Consumer-Integrität bedingt formuliert), F-169-03 (Quality Gates neu ausgeführt), F-169-04 (Trennung dokumentarisches PASS / Agentenverhalten `NOT_VERIFIABLE` beibehalten und klargestellt). Einzelheiten: Validierungsdokument §9.1, §9.2, §13.
- **Quality Gates (CP01, HEAD `4dab503`):** `--self-test` Python-Exit-Code `0`; `--strict` Python-Exit-Code `0`, 0 Fehler, 0 Warnungen, 4 Notices; keine lokale Denylist konfiguriert → kein Nachweis für einen CI-Lauf mit anders konfigurierter Denylist.
- **Verbliebene Einschränkungen:** keine historische Hash-Baseline für `.agents/skills/`; Existenz von Consumer-Locks unbekannt; keine ausgeführten Agenten-Verhaltens- oder Cross-Host-Tests; lokale Gates ohne Denylist.
- **Status:** CP01 ist weder ein Nova-Votum noch eine Annahme. Annahme von WP-169 und CP01 bleibt ausschließlich dem Human Maintainer vorbehalten.

## Verbotene vorzeitige Aktionen

Staging/Commit/Push/Tag/Release durch einen Agenten; Lock- oder Digest-Aktualisierung; Änderung an `.agents/**`, ADRs, Scripts, Roadmap oder `ndf-work-package-runner`; Start von WP-162 oder einem anderen WP.
