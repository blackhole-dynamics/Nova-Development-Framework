# NDF-WP-167 – Execution Evidence Hardening (Notes)

> Status: **`AGENT_COMPLETE – READY_FOR_NOVA_REVIEW`** — keine Annahme, kein Commit, kein Push, kein Release. Nova-Review und Human-Maintainer-Entscheidung ausstehend. Validation: [EXECUTION_EVIDENCE_HARDENING.md](../docs/validation/context-economy/EXECUTION_EVIDENCE_HARDENING.md)

## 1. Ausgangslage

NDF v1.1.0 veröffentlicht; WP-169 und WP-170 `ACCEPTED WITH NOTES`, committed und gepusht; WP-167 bis dahin nur als P1-Kandidat geführt (`RESERVED CANDIDATE – NOT ACTIVATED`). Die in WP-169/170 erprobte Evidenzpraxis (Exit-Codes direkt erfassen, Hash-Baselines vor Schreibvorgängen, Präfixnachweise, Trennung dokumentarischer Prüfung und Verhaltenstest, lokal vs. CI) war nur in Einzel-Records dokumentiert, nicht im Execution Contract verankert.

## 2. Autorisierungsgrenze

Human-Maintainer-autorisierter Vertrag `NDF-WP-167 — Full Authorized Implementation Contract` (`STATUS: COMPLETE REPLACEMENT`, `SUPERSEDES` Approval Draft und nicht autorisierte Vorfassung, `SESSION: NEW_SESSION_REQUIRED` mit spezifischer Begründung: Wechsel von lesendem Assessment zu autorisiertem Schreibauftrag; Hinweis „Neue Session nötig? Ja – neue Session erforderlich.“). Profil Full, Budget B3 Extended, vorgesehenes Evidence Tier E3, Claude Opus / Effort High. Docs-only; exakte Sieben-Datei-Allowlist; Git-Schreibrechte NONE; Release-Autorität NONE. Ausgeführt in einer neuen Session am 2026-11-03. Andere Kandidaten (WP-162…166, WP-168) sind nicht aktiviert (N-167-04).

## 3. Entscheidungsmatrix D-1 bis D-12

| ID | Entscheidung (Human Maintainer) | Umsetzung |
|---|---|---|
| D-1 | Variante B: Rule 6 im bestehenden Contract, WP-152-Guide für das Format | Rule 6 in `BLOCK_EXECUTION_CONTRACT.md`; Guide §12/§12.1/§13 |
| D-2 | E1/E2/E3 (`Basis`/`Regulär`/`Erweitert`), risikoproportional, nach Kollisionsprüfung | Kollisionsprüfung ohne semantischen Treffer (Validierung §6); Tiers in Rule 6 und §12.1 |
| D-3 | `BLOCK_FEEDBACK_TO_NOVA.md` unverändert | unverändert (Hash vorher/nachher, Abschlussbericht) |
| D-4 | Prompt Index minimal | ein Zusatz im Execution-Contract-Eintrag |
| D-5 | WP-170-Statushistorie nicht korrigieren | nicht berührt |
| D-6 | keine Verdict-/Status-/Fehlercode-Vereinheitlichung | keine neuen Codes; `REWORK` als bestehendes Votum |
| D-7 | G-14 separat | keine Skript-/Workflow-Änderung |
| D-8 | `NDF_PROMPT_MODES.md`-Status außerhalb | nicht berührt |
| D-9 | Opus, High, Full, B3 | eingehalten |
| D-10 | dokumentarische Regel-Testmatrix | T01–T20 dokumentarisch; kein Verhaltenstest behauptet |
| D-11 | keine Skill-Anpassung | keine Skill-Datei verändert |
| D-12 | WP-167 vor WP-168 bevorzugt, ohne zwingende Abhängigkeit | WP-168 nicht aktiviert |

## 4. Korrigierte Vertragsbefunde

- **C-167-01:** D-1…D-12 vollständig im Vertrag; keine Rekonstruktion aus früheren Chats.
- **C-167-02:** `PASS`/`FAIL` der Testmatrix sind rein dokumentarische Ergebnisse; ein hypothetisches `REWORK` in einem Testfall ist kein Abschlussstatus von WP-167; keine neuen Statuswerte.
- **C-167-03:** docs-only-Implementierung autorisiert; das Ergebnis ist nicht automatisch angenommen.
- **N-167-04:** keine Selbstsperre für WP-167; Verbot nur der Aktivierung anderer Kandidaten.

## 5. Preflight

`main` @ `ebff8626665d517f2017f843dd2e323b143d85f4` = Remote-`refs/heads/main` (lesend über `git ls-remote`, kein Fetch). Index leer; keine getrackten Änderungen; keine laufende Git-Operation; genau 38 untracked `.agents/skills/*/SKILL.md`. Listen-Hash der 38 Dateien reproduziert den WP-170-CP01-Wert `cf59b237…f8ba`; die vier bekannten `.agents`/`.claude`-Abweichungen stimmen mit den acht Einzelhashes aus WP-170 §7 überein. Fünf bestehende Schreibziele vorhanden, zwei neue nicht vorhanden. Vorher-Hashes aller Schreibziele und geschützten Bereiche vor dem ersten Schreibvorgang erfasst (Validierung §9). Ergebnis: keine materielle Abweichung.

## 6. ADR-0031-Kompatibilitätsgate

Vor der ersten Änderung ausgeführt (Validierung §3). Einordnung: **additiv mit prospektivem Übergang**. Work-Package-Flow und Review-Werte (Stable Candidate) unverändert; Rules 1–5, Header, Modi, Profile und Budgets unverändert; keine Rückwirkung; kein neues Tooling für Consumer; keine Migrationsnotiz über „keine Consumer-Aktion erforderlich“ hinaus; kein zusätzlicher ADR-Pfad. Gate erfüllt.

## 7. Tatsächlicher Datei-Scope

| # | Datei | Modus | Ergebnis |
|---|---|---|---|
| 1 | `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md` | additive Rule 6, Metadatenzeile | geändert |
| 2 | `docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md` | §12/§12.1/§13, Statusnachtrag | geändert |
| 3 | `docs/templates/REVIEW_ONLY_PROMPT_TEMPLATE.md` | Evidence-Pack-Block, ein Hinweis | geändert |
| 4 | `framework/prompts/PROMPT_INDEX.md` | Rule-6-Verweis | geändert |
| 5 | `CHANGELOG.md` | ein Eintrag unter `[Unreleased]` | geändert |
| 6 | `docs/validation/context-economy/EXECUTION_EVIDENCE_HARDENING.md` | neu | erstellt |
| 7 | diese Notes | neu | erstellt |

Keine weitere Datei erstellt, geändert, gelöscht, umbenannt oder verschoben. Die Nachher-Prüfung (Arbeitsbaum-Listenhash, `git status`, geschützte Bereiche) steht im Abschlussbericht an Nova.

## 8. Rule-6-Implementierungsstand

Rule 6 – Execution Evidence (zwölf kompakte Punkte): belastbare Ergebnisse (Exit-Status direkt und unverfälscht; Erfolgstext allein kein Prozessnachweis), Trennung der Prüfarten, Quellenklassen, Integritätsaussagen mit Vergleichsbasis und Listen-Hash-Option, Evidence Tiers mit höchstem Risikofaktor und Ableitung fehlender Angaben, Proportionalität inkl. Präfixnachweis ohne automatisches E3, Selbstreferenz über externen Abschlussbericht, lokal vs. CI inkl. Post-Push-Erfassung ohne Pflicht-WP, Sicherheitsgrenze für Denylist und Logs, Hostneutralität, unveränderte Autorität, prospektiver Übergang. Format und Tier-Trigger stehen ausschließlich im Guide §12/§12.1; Template und Index verweisen. Keine zweite Normquelle, kein Header-Feld, keine neuen Status- oder Fehlercodes.

## 9. Testmatrix

T01–T20 dokumentarisch geprüft: 20/20 `RULE CHECK: PASS`, 0 FAIL. Verhaltenstest tatsächlich ausgeführt: nein (alle 20). Kein Agentenverhaltens-, Cross-Host- oder Consumer-Test; die tatsächliche Anwendung von Rule 6 durch Agenten ist nicht verifiziert. Einzelheiten: Validierung §7.

## 10. Quality Gates

Lauf 1 (2026-11-03, 10:24:05–10:24:06 UTC; Git Bash 5.3.15, Python 3.13.17; `$?` direkt nach jedem Befehl, Ausgabe in Datei außerhalb des Repositorys umgeleitet, keine Pipeline): `--self-test` Exit-Code `0`; `--strict` Exit-Code `0`, 0 Fehler, 0 Warnungen, 4 Notices. Denylist konfiguriert: nein (weder Prozess-, User- noch Machine-Variable, keine lokale Datei; Wert nie gelesen). `git diff --check` Exit-Code `0`. Ein Bestätigungslauf mit beiden neuen Dateien, die Link-/Markdown-Prüfung und die Nachher-Integritätsprüfung stehen im Abschlussbericht an Nova.

## 11. Risiken und Grenzen

- Nur dokumentarische Regelprüfung; reales Agentenverhalten nicht verifiziert.
- Abgrenzung E1/E3 bleibt im Grenzfall eine Einschätzung; Zweifel werden über den höchsten Risikofaktor aufgelöst.
- Lokale Gates ohne Denylist; der CI-Lauf nach einem etwaigen Push bleibt maßgeblich und wird nicht vorweggenommen.
- Skills nennen Rule 6 noch nicht (D-11); Angleichung erst nach geklärter WP-168-Parity-Strategie und eigener Freigabe.
- G-14 bleibt gesonderte Sicherheitsprüfung (D-7).
- Hash-Vergleiche belegen nur Inhaltsgleichheit zu den verglichenen Zeitpunkten dieser Session; über den reproduzierten WP-170-Listenhash hinaus keine historische Unverändertheitsaussage.

## 12. Nova-Übergabe

Abschlusswert: `AGENT_COMPLETE – READY_FOR_NOVA_REVIEW`. Nova (ChatGPT) – die ChatGPT-basierte Planungs-, Architektur- und Review-Rolle – prüft WP-167 unabhängig. Danach entscheidet ausschließlich der Human Maintainer über die Annahme sowie über Staging, Commit und Push; Rule 6 gilt erst ab dieser Annahme. Der endgültige SHA-256 dieser Notes steht im Abschlussbericht an Nova, nicht in dieser Datei.

## 13. Corrective Pass CP01 (Nachtrag, append-only)

> Abschnitte 1–12 dokumentieren die ursprüngliche WP-167-Ausführung und bleiben unverändert. Dieser Nachtrag ist CP01-Inhalt, keine ursprüngliche Evidenz.

### 13.1 Autorisierung

Nova-Votum zur ursprünglichen Ausführung: `REWORK_REQUIRED – TARGETED DOCUMENTATION CORRECTION`; die WP-167-Architektur (Variante B, D-1…D-12, C-167-01…C-167-03, N-167-04) bleibt angenommen. Gesonderte Human-Maintainer-Entscheidung: `NDF-WP-167 CP01 AUTHORIZED – DOCS ONLY`. Vertrag `NDF-WP-167 CP01 — Full Authorized Corrective Pass Contract` (`STATUS: COMPLETE REPLACEMENT`, `SUPERSEDES` den ursprünglichen WP-167-Implementierungsvertrag, `SESSION: NEW_SESSION_REQUIRED` wegen der auf fünf Dateien reduzierten Allowlist und der neuen Autoritätsgrenze; „Neue Session nötig? Ja – neue Session erforderlich.“). Full, B3 Extended, Evidence Tier E3, Claude Opus / High. Docs-only; Git-Schreibrechte NONE; Release NONE. Ausgeführt in einer neuen Session am 2026-11-03. Umfang: ausschließlich F-167-01 und F-167-02.

### 13.2 Befunde und Korrekturen

| Befund | Ursprünglicher Zustand | CP01-Korrektur |
|---|---|---|
| F-167-01 | Rule 6 verlangte den höchsten zutreffenden Tier und wertete Unterdeklaration als `REWORK`; die Risikozuordnung stand aber nur als `Typical trigger` im Guide §12.1 | Rule 6 *Evidence Tiers* enthält die normative Mindestzuordnung E1/E2/E3; Rule-6-Verweiszeile „Format and illustrative tier examples“; Guide §12/§12.1 kennzeichnen die Tabelle als illustrativ (Spalte `Illustrative example (assignment: Rule 6)`; bei Abweichung entscheidet Rule 6); Validierung §5/§6 als *CP01* markiert korrigiert |
| F-167-02 | CHANGELOG „No consumer action is required.“; Validierung §3 Zeile 8 entsprechend | CHANGELOG und Validierung §3 Zeile 8 trennen: keine verpflichtende Tool-/Runtime-Migration · prospektive Anwendung durch Consumer, die die aktualisierten NDF-Regeln übernehmen · Fortgeltung historischer Records nach ihrem Regelstand |

Betroffene Dateien (genau fünf): `framework/prompts/blocks/BLOCK_EXECUTION_CONTRACT.md`, `docs/guides/TOKEN_EFFICIENCY_AND_CONTEXT_BUDGET_BASELINE.md`, `docs/validation/context-economy/EXECUTION_EVIDENCE_HARDENING.md` (in-place *CP01*-Markierungen in §3/§5/§6/§7, neuer §13), `CHANGELOG.md` (nur die WP-167-Zeile), diese Notes (nur dieser Nachtrag). `REVIEW_ONLY_PROMPT_TEMPLATE.md` und `PROMPT_INDEX.md` nicht berührt.

### 13.3 Kompatibilität

ADR-0031 in CP01 erneut gelesen (dokumentarische Regelprüfung, Validierung §13.2): Work-Package-Flow, Review-Werte und Rollengrenzen unverändert; keine Rückwirkung; künftige Evidenzanforderungen werden für übernehmende Consumer strenger — offengelegt und prospektiv; die korrigierte CHANGELOG-Aussage ist die von ADR-0031 erwartete kurze Migrationsnotiz. Einordnung nach erneuter Prüfung: **additiv mit prospektivem Übergang**; kein Breaking Change, kein zusätzlicher ADR-Bedarf. Kein Consumer-Verhaltenstest; tatsächliche Consumer-Adoption nicht verifiziert.

### 13.4 Ergänzende dokumentarische Prüfungen

T03, T04, T13, T16, T17, T18 gegen den CP01-Text dokumentarisch nachgeprüft: 6/6 PASS; die übrigen 14 Fälle stützen sich auf bytegleich gebliebene Rule-6-Punkte, kein Widerspruch. Verhaltenstest ausgeführt: nein. Die ursprünglichen Matrixzeilen (Validierung §7) bleiben unverändert und gelten nicht als neu ausgeführte Tests (Validierung §13.3).

### 13.5 Quality Gates (CP01 Lauf 1)

2026-11-03, 11:30:33–11:30:34 UTC; Git Bash 5.3.15, Python 3.13.17; `$?` direkt nach jedem Befehl, Ausgabe in Datei außerhalb des Repositorys, keine Pipeline; nach den Korrekturen an Contract, Guide, CHANGELOG und Validierung §3/§5/§6/§7, vor Validierung §13 und diesem Nachtrag. `--self-test` Exit-Code `0`; `--strict` Exit-Code `0`, 0 Fehler, 0 Warnungen, 4 Notices; `git diff --check` Exit-Code `0`. Denylist konfiguriert: nein (Prozess-, User-, Machine-Ebene und lokale Datei auf Vorhandensein geprüft, kein Wert gelesen). Lokaler PASS ist kein vollständiger Neutralitätsnachweis und kein CI-Ergebnis. Bestätigungslauf nach diesem Nachtrag: Abschlussbericht an Nova.

### 13.6 Integrität

Vergleichsbasis: SHA-256 der fünf CP01-Ziele, in dieser Session vor dem ersten CP01-Schreibvorgang erfasst; sie reproduzieren die Nachher-Werte des ursprünglichen WP-167-Abschlussberichts. Contract: Rückwärtsanwendung der zwei CP01-Ersetzungen ergibt bytegenau den Vorher-Hash `bb26b455…1f4c`; Metadaten, Execution Header, Rules 1–5 und Authority-Abschnitt hashgleich. Guide: alles vor §12 und ab §13 hashgleich. CHANGELOG: alle Zeilen außer der WP-167-Zeile hashgleich. Diese Notes: Präfix der ersten 8184 Bytes = Vorher-Hash `a2f73e2e…8228` (Prüfung und Endhash im Abschlussbericht an Nova, nicht in dieser Datei). Zeilenenden aller fünf Ziele vorher und nachher LF; eine zwischenzeitliche CRLF-Umwandlung des Contracts durch einen Agentenfehler wurde in derselben Session vor jedem weiteren Schritt zurückgenommen und ist durch den Rekonstruktionsnachweis abgedeckt. Ausgeschlossene WP-167-Dateien, `.agents/` und Schutzbereiche: Vorher/Nachher-Vergleich im Abschlussbericht an Nova.

### 13.7 Verbleibende Risiken

- N-CP01-01: Die WP-167-CHANGELOG-Zeile beschreibt den Guide weiterhin als Träger von „format and tier triggers“; CP01 erlaubte im CHANGELOG nur die Korrektur der Migrationsaussage. Keine Normquelle; eine Angleichung braucht eine gesonderte Human-Maintainer-Entscheidung.
- „Relevant“ in der E1/E3-Zuordnung bleibt eine Einschätzung; Zweifel löst der höchste Risikofaktor.
- Nur dokumentarische Prüfung; keine Agentenverhaltens-, Cross-Host- oder Consumer-Tests.
- Lokale Gates ohne Denylist; CI wird nicht vorweggenommen. Skill-Angleichung (D-11) und G-14 (D-7) bleiben separat.

### 13.8 Abschlussstatus

F-167-01 und F-167-02: `CORRECTED – PENDING NOVA REVIEW`. CP01: **`READY_FOR_NOVA_REVIEW`**. Nova-Nachprüfung, Human-Maintainer-Annahme sowie Staging, Commit und Push stehen aus; kein anderes Work Package aktiviert.
