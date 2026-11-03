# NDF-WP-170 – Post-v1.1 Status & Roadmap Reconciliation (Notes)

> Status: **`AGENT_COMPLETE – READY_FOR_NOVA_REVIEW`** — keine Annahme, kein Commit, kein Release. Nova-Review und Human-Maintainer-Entscheidung ausstehend.

## 1. Autorisierung

Human-Maintainer-autorisierter Ausführungsvertrag `NDF-WP-170` (`STATUS: COMPLETE`, `SUPERSEDES: N/A`, `SESSION: NEW_SESSION_REQUIRED` mit spezifischer Begründung: Wechsel von einer lesenden Roadmap-Prüfung zu einem begrenzten Schreibvertrag; Hinweis „Neue Session nötig? Ja – neue Session erforderlich.“). Profil Full, Budget B3. Docs-only; Git-Schreibaktionen verboten; keine Release-Autorität. Ausgeführt in einer neuen Session am 2026-11-03.

## 2. Baseline

`main` @ `24760c4315a02e26d61b17cc43eece56e52579d9` = lokales `origin/main` = Remote-`refs/heads/main` (lesend über `git ls-remote`, kein Fetch). Index leer; keine getrackten Änderungen; keine laufende Git-Operation; 38 untracked `SKILL.md` unter `.agents/skills/` (bekannt, außerhalb des Scopes). Die Ausgangsangaben des Vertrags wurden vollständig bestätigt.

## 3. Exakte Allowlist

| # | Pfad | Modus | Vorher |
|---|---|---|---|
| 1 | `docs/roadmap/POST_V1_1_CANDIDATE_ROADMAP.md` | neu | nicht vorhanden |
| 2 | `docs/roadmap/NDF_WORK_PACKAGE_ID_REGISTER.md` | neu | nicht vorhanden |
| 3 | `project-brain/CONTEXT_PACK_POST_V1_1.md` | neu | nicht vorhanden |
| 4 | `project-brain/NEXT_PHASE_POST_V1_1.md` | neu | nicht vorhanden |
| 5 | `project-brain/WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md` | neu | nicht vorhanden |
| 6 | `project-brain/WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md` | append-only | vorhanden |
| 7 | `docs/validation/context-economy/PROMPT_EXECUTION_CONTRACT_HARDENING.md` | append-only | vorhanden |

## 4. Bestätigte Human-Maintainer-Entscheidungen

| ID | Entscheidung | Abbildung |
|---|---|---|
| I-1 | WP-160 `RESERVED – HISTORICAL ALLOCATION UNRESOLVED`; keine rückwirkende Zuordnung zur README-Modernisierung | Register §3, §5, §8 |
| I-2 | WP-162…168 vorgemerkt, nicht aktiviert; Reihenfolge darf abweichen | Register §3, §5; Roadmap §4, §5 |
| I-3 | Nummerierungsregel (keine Wiederverwendung, keine stille Umnummerierung, Historie behalten, neue Nummer nur per Human-Maintainer-Entscheidung, keine Agenten-Vergabe) | Register §7 |
| I-4 | Laufende Kandidatenplanung; kein v1.2-Scope-Lock; keine Release-Entscheidung | Roadmap §1, §3 |
| I-5 | `.claude/skills/` getrackt, `.agents/skills/` lokal/untracked; Strategie offen; vier Unterschiede als Risiko | Roadmap §4, §8; Context Pack |
| I-6 | Kandidatenzuschnitt WP-162…168 | Roadmap §5, §6 |
| I-7 | Post-Release-Review ohne WP-ID, nicht in WP-170 | Roadmap §5; Next Phase |
| I-8 | ADR-0033 aufgeschoben | Roadmap §5; Context Pack |
| I-9 | CI-Wartung getrennt; keine Zielversion | Roadmap §5; Next Phase |
| I-10 | Annahmestatus zweier Governance-Guidances offen | Register §8; Context Pack |

## 5. Neu erstellte Dokumente

- [NDF_WORK_PACKAGE_ID_REGISTER.md](../docs/roadmap/NDF_WORK_PACKAGE_ID_REGISTER.md) — Status WP-160…170, Quellenlage, Nummerierungsregel, Evidenzgrenzen (DE + EN-Zusammenfassung).
- [POST_V1_1_CANDIDATE_ROADMAP.md](../docs/roadmap/POST_V1_1_CANDIDATE_ROADMAP.md) — Kandidaten, Prioritäten, Abhängigkeiten, Risiken, Nichtziele (DE + EN-Zusammenfassung).
- [CONTEXT_PACK_POST_V1_1.md](CONTEXT_PACK_POST_V1_1.md) — kompakter Snapshot mit Rule-5-Freshness-Hinweis.
- [NEXT_PHASE_POST_V1_1.md](NEXT_PHASE_POST_V1_1.md) — Handoff, Reihenfolge, Voraussetzungen WP-167/168, Freshness-Prüfung.
- diese Notes.

## 6. Append-only-Änderungen an WP-169

| Datei | Neuer Abschnitt | Vorher SHA-256 | Vorher Bytes |
|---|---|---|---|
| [WP-169-Notes](WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md) | `## Post-Acceptance Reconciliation – NDF-WP-170` | `16493167b9be188a1994980af53f3075689f3078c481abe1af4292c0aabf645a` | 5777 |
| [WP-169-Validierung](../docs/validation/context-economy/PROMPT_EXECUTION_CONTRACT_HARDENING.md) | `## 14. Post-Acceptance Evidence – NDF-WP-170 Reconciliation` | `426e2dc0c204bc335127618f3517e12777a13aa1be569ecbb72a304b42eef02f` | 20734 |

Präfixprüfung: Der vollständige Vorher-Inhalt (Kopie außerhalb des Repositorys) ist bytegenau Präfix des Endzustands. Nachher-Werte und angehängte Zeilenzahl stehen im Abschlussbericht an Nova, weil diese Notes selbst nicht Teil der Append-Dateien sind.

## 7. Quellen und Evidenz

| Aussage | Quelle | Prüfung |
|---|---|---|
| `v1.1.0` veröffentlicht | Tag `v1.1.0` → `948c91d`; GitHub-Release „Latest“ 2026-09-23 | `git rev-parse`, `gh release list` (lesend) |
| WP-169 angenommen | Commit-Body `24760c4`; Human-Maintainer-Angabe im WP-170-Vertrag | `git show -s` (lesend) |
| WP-169 gepusht | Remote `refs/heads/main` = `24760c4` | `git ls-remote` (lesend) |
| CI `success` für `24760c4` | Workflow „Public Quality Gate“, `push`, `success` | `gh run list --commit` (lesend) |
| Nova-Votum `GO_WITH_NOTES` | nur Human-Maintainer-Angabe im WP-170-Vertrag | kein Repository-Dokument; nicht unabhängig geprüft |
| „kein WP-160“ zum v1.1-Abschluss | `V1_1_PLAN.md`, Release Evidence Index, Context Pack 0.9 | Repository-Suche |
| WP-161-Bezug | `branding/assets/png/README.md`, Commit `b7bebb8` | Repository-Suche, `git show --stat` |
| Guidance-Status offen | Statusfeld `Implemented, pending Nova review`; Commit `ebf716c` | Repository-Suche |
| Vier Skill-Unterschiede | SHA-256-Vergleich `.agents/skills/` vs. `.claude/skills/` | siehe unten |

Skill-Unterschiede (SHA-256, 2026-11-03; `.claude/skills/` = HEAD-Blob):

| Skill | `.agents/skills/` | `.claude/skills/` |
|---|---|---|
| `ndf-compact-context-summary-runner` | `7fae60937332fa42da41ba5de40b41c383a83bba65e8519665c2d760906e9c44` | `001da3e7528b9fbb06b6d8028df540440ee9cd7a5f26d170d28a6756568d9f24` |
| `ndf-context-pack-maintainer` | `e072ef15c4f22efa8d3d02d81a98289a935e2eceb33aa47c8535965ca5ac90dc` | `3241e1050c25a1b909c2df7b1d643d52c0de2ea95fe9257d885b740b17b22563` |
| `ndf-skill-quality-reviewer` | `a936ef397dd9d1fe497e4995083cb21d564844c530ff00cd7ad7dbfd48220bf9` | `eaa8819266765c71cbe40ad852d96858feee7dc24480b61c5797128bc14927e0` |
| `ndf-skill-trigger-quality-reviewer` | `072726175e0244bd177cfa46eab070fea9d6aaa0e06f9a14f5435c2640f89f05` | `2843aba42405f8d249c94b14439a8e4a93080a59a927c04b3945991f34890294` |

## 8. Dokumentations- und Konsistenzprüfungen

Relative Links aller sieben Dateien aufgelöst; WP-IDs und Statusbegriffe zwischen Register, Roadmap, Context Pack und Next Phase abgeglichen; Planung, Implementierung, Review, Annahme und Release getrennt; Kandidaten durchgehend als nicht aktiviert gekennzeichnet; keine neue universelle Pflicht; keine externen Projekt- oder Produktabhängigkeiten; Public-Neutrality-Selbstprüfung (keine privaten Namen, Domains, Kontokennungen oder Secrets); ADR-0031/0032 unverändert. Einzelergebnisse: Abschlussbericht an Nova.

## 9. Quality-Gate-Ergebnisse

Lauf 2026-11-03, 06:17:43–06:17:44 UTC, `main` @ `24760c4` mit den WP-170-Dokumenten außer diesen Notes; PowerShell 7.6.9, Python 3.13.17; je Befehl `$LASTEXITCODE` direkt danach, keine Pipeline. Skript vorab gelesen: liest Dateilisten über `git ls-files`, schreibt nur im Self-Test in ein temporäres Verzeichnis, kein Netzwerk.

| Gate | Python-Exit-Code | Ausgabe | Fehler / Warnungen / Notices |
|---|---|---|---|
| `--self-test` | `0` | `self-test passed` | – |
| `--strict` | `0` | `Public quality gate passed.` | 0 / 0 / 4 |

Notices: Scan-Modus tracked + new/untracked; 42 neue Textdateien im Scan (38 `.agents/skills/` + 4 WP-170-Dokumente); keine eigene Denylist konfiguriert; daher nur Struktur-/Root-/README-Regeln für neue Dateien. **Denylist:** weder `NDF_PUBLIC_NEUTRALITY_DENYLIST` (Prozess, User, Machine) noch `.ndf/public-neutrality-terms.local.txt` vorhanden. Ein lokaler PASS ersetzt keinen späteren CI-Lauf mit konfigurierter Denylist. Ein Bestätigungslauf nach Erstellung dieser Notes steht im Abschlussbericht.

## 10. Offene Risiken

- WP-161: gesonderte Annahme nicht belegt. WP-160: externe Vergabe nicht ausschließbar.
- Nova-Votum `GO_WITH_NOTES` zu WP-169 nur als Human-Maintainer-Angabe vorhanden.
- `.agents/skills/`: Unverändertheit während WP-170 per Vorher-/Nachher-Hash nachgewiesen; historische Unverändertheit vor WP-170 nicht nachweisbar.
- Lokale Gates ohne Denylist; CI maßgeblich.
- Kandidaten könnten durch Erwähnung als aktiviert missverstanden werden; alle Dokumente markieren sie ausdrücklich als nicht aktiviert.

## 11. Abschließender Implementierungsstatus

`AGENT_COMPLETE – READY_FOR_NOVA_REVIEW`. Kein `ACCEPTED`, kein Staging, kein Commit, kein Push, kein Tag, kein Release. Keine Aktivierung von WP-162…168; keine neue WP-ID vergeben.

## 12. Übergabe an Nova

Nova (ChatGPT) – die ChatGPT-basierte Planungs-, Architektur- und Review-Rolle – prüft WP-170 unabhängig. Danach entscheidet ausschließlich der Human Maintainer über `ACCEPTED`, `ACCEPTED WITH NOTES`, `REWORK_REQUIRED` oder `STOP` sowie über Staging, Commit und Push.

## Corrective Pass CP01 – F-170-01 / F-170-02

> Status nach CP01: **`AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING`**. Die Statusangaben in der Kopfzeile und in §11 dieser Notes beschreiben den Stand vor dem ersten Nova-Review und bleiben als Historie unverändert.

### CP01.1 Anlass

Das unabhängige Nova-Review von WP-170 ergab `REWORK_REQUIRED – TARGETED DOCUMENTATION CORRECTION` mit zwei Befunden: F-170-01 (nicht autorisierte zwingende Abhängigkeit von WP-166 zu einem externen WP-165-Lauf) und F-170-02 (mehrdeutige WP-170-Statusbezeichnung im WP-ID-Register). Quelle des Review-Ergebnisses: Angabe im CP01-Ausführungsvertrag; kein Repository-Dokument.

### CP01.2 Autorisierung

Gesonderter Human-Maintainer-autorisierter Vertrag `NDF-WP-170 / CP01` (`STATUS: COMPLETE REPLACEMENT`, `SESSION: NEW_SESSION_REQUIRED`, Profil Full, Budget B2, `EXECUTION: DOCS_ONLY_CORRECTIVE_PASS`, `GIT_WRITES: FORBIDDEN`, `RELEASE_AUTHORITY: NONE`). Die Sieben-Datei-Allowlist des ursprünglichen Vertrags wurde nicht übernommen. Ausgeführt in einer neuen Session am 2026-11-03.

### CP01.3 Exakte Drei-Datei-Allowlist

| # | Pfad | Modus | SHA-256 vorher | SHA-256 nachher |
|---|---|---|---|---|
| 1 | `docs/roadmap/POST_V1_1_CANDIDATE_ROADMAP.md` | punktuelle Korrektur (F-170-01) | `c5c2a24ec03626fbd795b335f87f958694bebd1f64e6141d1bfd79fd936a1258` | `50a97db5f63f13ffd03d5805be3b36b4a79f59c81eec134c128a80e5b479699f` |
| 2 | `docs/roadmap/NDF_WORK_PACKAGE_ID_REGISTER.md` | punktuelle Korrektur (F-170-02) | `48e15705751888dfad2c60910d07d8d7ddab70077999df5c8ab7562d486627e4` | `711e48890ca81780123d4ee89e3cea30cbfe3a801285c505c0c7a9d68bf4af85` |
| 3 | `project-brain/WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md` | append-only (dieser Abschnitt) | `33a433284088696b8201b8db1acf7f31bb42ae31ae80e0a9b1cb026cceda16bc` (9096 Bytes) | im Abschlussbericht an Nova |

### CP01.4 F-170-01 – korrigierte Aussagen (Roadmap §5, §7)

- §5 WP-166: bleibt `DEFERRED`; ein Benchmark-Vorhaben wird erst konkretisiert, wenn ausreichende reale, nachvollziehbare und reproduzierbare Mess- bzw. Validierungsevidenz vorliegt; ein externer WP-165-Lauf kann Evidenz beitragen, ist aber keine generell zwingende Voraussetzung; eine spätere Aktivierung erfordert einen gesonderten Human-Maintainer-autorisierten Vertrag. Entfernt: „frühestens nach einem externen Lauf aus WP-165“.
- §7 Abhängigkeitsmatrix: Die Darstellung „Externer Lauf → WP-166: zwingend“ ist durch eine optionale Evidenzbeziehung ersetzt („ggf. Evidenz für WP-166“; „Vorbedingungen zwingend; Evidenzbeitrag zu WP-166 optional“). Die Vorbedingungen des externen Laufs (WP-165 Kit, unabhängige Partei) bleiben unverändert. WP-166 behält als zwingende Voraussetzung ausschließlich die Evidenzanforderung.
- EN-Zusammenfassung („deferred until real, reproducible evidence exists“) widerspricht dem korrigierten Stand nicht und blieb unverändert.

### CP01.5 F-170-02 – korrigierte Statusklassifikation (Register)

- §4: Statusklasse `HUMAN-MAINTAINER-AUTHORIZED – IMPLEMENTATION PENDING NOVA REVIEW` ersetzt durch `AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING` (Implementierung inkl. CP01 agentenseitig abgeschlossen; erstes Nova-Review `REWORK_REQUIRED`; Re-Review und Annahme ausstehend).
- §5 Zeile WP-170: neuer Status; Ausführungsautorität getrennt als `HUMAN_MAINTAINER_AUTHORIZED`; Hinweis auf das erste Review-Ergebnis.
- EN-Zusammenfassung und Kopfzeile (direkt widersprechende Formulierung „Nova-Review … ausstehend“) entsprechend angepasst.
- Unverändert: WP-160, WP-161 (`COMMITTED – ACCEPTANCE RECORD OPEN`), WP-162…168 (`RESERVED CANDIDATE – NOT ACTIVATED`), WP-169 (`ACCEPTED WITH NOTES – COMMITTED – PUSHED`).

### CP01.6 Unveränderte Planungsentscheidungen

I-1…I-10 unverändert. WP-165 bleibt in Kit und späteren unabhängigen Lauf getrennt; G-13-Unabhängigkeitsanforderung unverändert; WP-167/168 bleiben P1; WP-162 verkleinert; WP-163 nicht eigenständig; WP-164 Kandidat. Keine neue Priorität, keine neue Abhängigkeit, keine neue WP-ID, keine Aktivierung.

### CP01.7 Quality Gates und Grenzen

Skript vorab lesend geprüft: Dateilisten über `git ls-files` (lesend), Schreibzugriffe nur im Self-Test in ein `TemporaryDirectory`, kein Netzwerk. Lauf 1 nach den Korrekturen an Datei 1 und 2, vor diesem Anhang: 2026-11-03, 06:47:55–06:47:56 UTC; PowerShell 7.6.9, Python 3.13.17; `$LASTEXITCODE` je Befehl direkt danach, keine Pipeline.

| Gate | Python-Exit-Code | Ausgabe | Fehler / Warnungen / Notices |
|---|---|---|---|
| `--self-test` | `0` | `self-test passed` | – |
| `--strict` | `0` | `Public quality gate passed.` | 0 / 0 / 4 |

Notices: Scan-Modus tracked + new/untracked; 43 neue Textdateien im Scan (38 `.agents/skills/` + 5 WP-170-Dokumente); keine Denylist konfiguriert; daher nur Struktur-/Root-/README-Regeln für neue Dateien. **Denylist:** weder `NDF_PUBLIC_NEUTRALITY_DENYLIST` (Prozess, User, Machine) noch `.ndf/public-neutrality-terms.local.txt` vorhanden. Ein lokaler PASS ist kein GitHub-CI-Lauf. Ein Bestätigungslauf nach diesem Anhang steht im Abschlussbericht an Nova.

### CP01.8 Append-only-Präfixprüfung

Vorher-Inhalt dieser Notes vor dem ersten Schreibvorgang außerhalb des Repositorys gesichert (9096 Bytes, SHA-256 siehe CP01.3, LF-Zeilenenden, abschließender Zeilenumbruch). Der Anhang erfolgte ausschließlich durch Anfügen am Dateiende. Die bytegenaue Präfixprüfung (Vorher-Inhalt = erste 9096 Bytes des Endzustands) und der Nachher-Hash stehen im Abschlussbericht an Nova, weil diese Notes ihren eigenen Endzustand nicht enthalten können.

### CP01.9 Ausgeschlossene Dateien

SHA-256 vor CP01 und vor diesem Anhang identisch:

| Datei | SHA-256 |
|---|---|
| `project-brain/CONTEXT_PACK_POST_V1_1.md` | `6001b92d56953e7eee32a4c85876c448c68ec51a7df4e365ba1eaa6e7f3f1930` |
| `project-brain/NEXT_PHASE_POST_V1_1.md` | `78db6ce241809cb3eb96ef4daa939f57d7cfa350428f357b8ec9174b1ad57d2c` |
| `project-brain/WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md` | `31972f6ba066715a0803b46a6fd3e6526b63b9915f9959db62d9e74807228608` |
| `docs/validation/context-economy/PROMPT_EXECUTION_CONTRACT_HARDENING.md` | `f1cf366e12acb892bf754a58829b47276aa390de57690c720a8142fc5e766e16` |

Alle 38 `.agents/skills/*/SKILL.md` per sortierter Hash-Liste identisch (SHA-256 der Hash-Liste: `cf59b237cab107dffb68f781d7822753a5df456c29e03ece6dfb57100e79f8ba`); Git-Index leer; `git status --short --untracked-files=all` unverändert. Die Nachprüfung nach diesem Anhang steht im Abschlussbericht an Nova. Historische Unverändertheit vor CP01 ist durch diese Prüfung nicht nachweisbar.

### CP01.10 Bekannte, nicht korrigierte Folgehinweise

Außerhalb des CP01-Auftrags und daher unverändert (lesend festgestellt):

- Roadmap §9 (Punkt 1) und EN-Zusammenfassung nennen das Nova-Review von WP-170 noch als nächsten Schritt.
- `CONTEXT_PACK_POST_V1_1.md` (WP-170-Statuszeile, Next Step 1) und `NEXT_PHASE_POST_V1_1.md` (Reihenfolge Punkt 1) beschreiben den Stand vor dem ersten Nova-Review. Beide Dateien enthalten keine WP-165→WP-166-Abhängigkeit (nur „WP-166 DEFERRED“).

Diese Formulierungen geben den Stand vor dem ersten Nova-Review wieder und bilden das Review-Ergebnis `REWORK_REQUIRED` nicht ab. Über eine Nachführung entscheiden Nova und der Human Maintainer.

### CP01.11 Abschlussstatus und offene Entscheidung

`AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING`. Kein `ACCEPTED`, kein Staging, kein Commit, kein Push, kein Tag, kein Release. Nova (ChatGPT) – die ChatGPT-basierte Planungs-, Architektur- und Review-Rolle – prüft CP01 erneut. Danach entscheidet ausschließlich der Human Maintainer über die Annahme von WP-170 sowie über Staging, Commit und Push.
