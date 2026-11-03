# NDF Work Package ID Register — Post-v1.1

> Work Package: `NDF-WP-170` — Post-v1.1 Status & Roadmap Reconciliation
> Stand: 2026-11-03 · Repository-Revision bei Erstellung: `main` @ `24760c4` (WP-169-Annahme-Commit)
> Status dieses Dokuments: im Rahmen von WP-170 erstellt; WP-170 ist **nicht angenommen** (erstes Nova-Review: `REWORK_REQUIRED`; erneutes Nova-Review nach CP01 und Human-Maintainer-Entscheidung ausstehend).
> Kandidatenplanung: [POST_V1_1_CANDIDATE_ROADMAP.md](POST_V1_1_CANDIDATE_ROADMAP.md)

## DE – 1. Zweck und Geltungsbereich

Dieses Register macht die Vergabe und den Status der NDF-Work-Package-Kennungen **WP-160 bis WP-170** nachvollziehbar. Es gilt nur für dieses Repository und nur für die hier gelisteten Kennungen.

Es rekonstruiert **nicht** sämtliche jemals vergebenen NDF-WP-Nummern. Ältere Kennungen sind über die jeweiligen Plan-, Scope-Lock- und Notes-Dokumente nachvollziehbar (z. B. [V1_1_PLAN.md](V1_1_PLAN.md) für WP-150…159). Das Register ist eine Status- und Nummerierungsübersicht, keine Aktivierung und keine Implementierungsfreigabe.

## DE – 2. Historische Ausgangslage

- Der v1.1-Zyklus umfasste WP-151…159 (nach zwei dokumentierten Einschüben, siehe [V1_1_PLAN.md](V1_1_PLAN.md)). Zum Abschluss des Zyklus vermerkten mehrere Dokumente ausdrücklich „kein WP-160“ bzw. „no WP-160 exists“ ([V1_1_PLAN.md](V1_1_PLAN.md), [V1_1_0_RELEASE_EVIDENCE_INDEX.md](../release/V1_1_0_RELEASE_EVIDENCE_INDEX.md), [CONTEXT_PACK_FOUNDATION_0_9.md](../../project-brain/CONTEXT_PACK_FOUNDATION_0_9.md)). Diese Aussagen beschreiben den damaligen Stand und bleiben als Historie korrekt.
- `v1.1.0` ist getaggt (Tag → `948c91d`) und als GitHub-Release veröffentlicht (2026-09-23).
- Nach dem Tag folgten vier Commits auf `main`: `948b06a` (README-Modernisierung, ohne WP-ID in der Commit-Nachricht), `b7bebb8` (Branding-Assets; die enthaltene Asset-README nennt NDF-WP-161), `4dab503` (Neutralitäts-Fix, ohne WP-ID in der Commit-Nachricht), `24760c4` (WP-169).
- Die Kennungen WP-162…168 wurden in der Post-v1.1-Planung vorgeschlagen. Im Repository war vor WP-170 nur WP-162 erwähnt (als verbotene vorzeitige Aktion in den WP-169-Notes).

## DE – 3. Human-Maintainer-Entscheidung zur Vergabe

Die folgenden Planungsentscheidungen hat der Human Maintainer getroffen; WP-170 zeichnet sie auf, trifft sie aber nicht:

- **WP-160** bleibt ungeklärt und gegen Wiederverwendung reserviert. Eine rückwirkende Zuordnung zur README-Modernisierung ist nicht autorisiert.
- **WP-162…168** bleiben mit Kennung und Arbeitstitel strategisch vorgemerkt. Sie sind keine aktivierten Implementierungsaufträge; die Bearbeitungsreihenfolge darf von der Nummerierung abweichen.
- **Nummerierungsregel** (§7) gilt als angenommene Planungsregel für dieses Repository.
- Für den eigenständigen v1.1.0-Post-Release-Review, die CI-Actions-Wartung, ADR-0033 und die Klärung zweier Governance-Guidance-Status wird **keine** WP-ID vergeben.

## DE – 4. Statusklassifikation

| Status | Bedeutung |
|---|---|
| `RESERVED – HISTORICAL ALLOCATION UNRESOLVED` | Kennung gesperrt; ursprüngliche Zuordnung nicht belegbar; nicht frei |
| `COMMITTED – ACCEPTANCE RECORD OPEN` | Ergebnis liegt in einem Commit vor; eine gesonderte Human-Maintainer-Annahme ist nicht separat belegt |
| `RESERVED CANDIDATE – NOT ACTIVATED` | Kennung und Arbeitstitel vorgemerkt; keine Ausführungsautorität, kein Vertrag |
| `ACCEPTED WITH NOTES – COMMITTED – PUSHED` | Human-Maintainer-Annahme belegt; Commit auf `origin/main` |
| `AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING` | Implementierung einschließlich Corrective Pass CP01 durch den Agenten abgeschlossen; erstes Nova-Review mit `REWORK_REQUIRED` durchgeführt; erneutes Nova-Review nach CP01 und Human-Maintainer-Annahme ausstehend. Die Ausführungsautorität (`HUMAN_MAINTAINER_AUTHORIZED`) wird getrennt in der Spalte „Ausführungsautorität“ geführt |

Planung, Implementierung, Review, Annahme und Release sind getrennte Zustände. Kein Status in diesem Register ist eine Release-Aussage.

## DE – 5. Register WP-160 bis WP-170

| WP-ID | Arbeitstitel | Status | Ausführungsautorität | Hinweis |
|---|---|---|---|---|
| WP-160 | — (ungeklärt) | `RESERVED – HISTORICAL ALLOCATION UNRESOLVED` | keine | nicht wiederverwenden; keine rückwirkende Zuordnung |
| WP-161 | Branding-Asset-Integration (historische Referenz; Titel aus der Commit-Nachricht abgeleitet) | `COMMITTED – ACCEPTANCE RECORD OPEN` | historisch | Commit `b7bebb8`; Annahmenachweis nicht separat belegt |
| WP-162 | Machine-Readable Work Package Contract | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | verkleinern; nur optionale abgeleitete Projektion |
| WP-163 | Compliance Model | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | nicht eigenständig aktivieren; mögliche Integration in WP-164 |
| WP-164 | Adoption / Governance Tiers | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | als Kandidat weiterplanen |
| WP-165 | Independent Validation Kit / späterer externer Lauf | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | Kit und externen Lauf getrennt planen |
| WP-166 | Benchmark Specification | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | zurückgestellt (DEFERRED) |
| WP-167 | Execution Evidence Hardening | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | Planungspriorität P1 |
| WP-168 | Skills Parity & Integrity Reconciliation | `RESERVED CANDIDATE – NOT ACTIVATED` | keine | Planungspriorität P1 |
| WP-169 | Prompt Execution Contract Hardening | `ACCEPTED WITH NOTES – COMMITTED – PUSHED` | abgeschlossen | Commit `24760c4`; CP01 `ACCEPTED`; kein Release |
| WP-170 | Post-v1.1 Status & Roadmap Reconciliation | `AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING` | `HUMAN_MAINTAINER_AUTHORIZED` (Docs-only-Vertrag, Sieben-Pfad-Allowlist; CP01 als gesonderter Drei-Pfad-Vertrag) | erstes Nova-Review: `REWORK_REQUIRED` (F-170-01, F-170-02); CP01-Re-Review und Annahme ausstehend; Agentenstand: [WP-170-Notes](../../project-brain/WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md) |

## DE – 6. Quellenlage je Kennung

| WP-ID | Quellen | Belegstärke |
|---|---|---|
| WP-160 | v1.1-Abschlussdokumente: „kein WP-160“ ([V1_1_PLAN.md](V1_1_PLAN.md), [Release Evidence Index](../release/V1_1_0_RELEASE_EVIDENCE_INDEX.md)); keine spätere Zuordnung im Repository; Human-Maintainer-Entscheidung I-1 (WP-170-Vertrag) | Reservierung belegt; Zuordnung ungeklärt |
| WP-161 | [branding/assets/png/README.md](../../branding/assets/png/README.md) („Human-Maintainer-approved handoff for NDF-WP-161“), eingeführt mit Commit `b7bebb8`; die Commit-Nachricht selbst nennt keine WP-ID | Commit belegt; Zuordnung über Dateiinhalt; gesonderte Annahme nicht separat belegt |
| WP-162 | Erwähnung in den [WP-169-Notes](../../project-brain/WP_169_PROMPT_EXECUTION_CONTRACT_HARDENING_NOTES.md) (verbotene vorzeitige Aktion); Human-Maintainer-Entscheidungen I-2, I-6 | Vormerkung belegt; kein Vertrag |
| WP-163…168 | Human-Maintainer-Entscheidungen I-2, I-6 (WP-170-Vertrag); vor WP-170 keine Repository-Erwähnung | Vormerkung belegt; kein Vertrag |
| WP-169 | Commit `24760c4` (Commit-Body: „Human Maintainer decision: ACCEPTED WITH NOTES; CP01: ACCEPTED.“); `origin/main` = `24760c4`; GitHub-Workflow „Public Quality Gate“ für diesen Commit `success`; Human-Maintainer-Angabe im WP-170-Vertrag | Annahme, Commit, Push und CI belegt |
| WP-170 | Human-Maintainer-autorisierter WP-170-Vertrag; [WP-170-Notes](../../project-brain/WP_170_STATUS_AND_NUMBERING_RECONCILIATION_NOTES.md) | Autorisierung belegt; Annahme offen |

Quellenpriorität: Die Human-Maintainer-Entscheidung und der verifizierte Commit bilden die Annahmegrundlage. Ein Commit-Body allein ersetzt keine zukünftige Human-Maintainer-Freigabe.

## DE – 7. Regeln zur Wiederverwendung und Umnummerierung

Angenommene Planungsregel für dieses Repository (Human-Maintainer-Entscheidung I-3):

1. Vergebene oder bereits referenzierte WP-IDs werden nicht wiederverwendet.
2. Nach externer Referenzierung wird nicht still umnummeriert.
3. Zurückgestellte oder zusammengelegte Kennungen bleiben mit ihrer Historie im Register.
4. Eine neue Nummer erfordert eine nachvollziehbare Human-Maintainer-Entscheidung.
5. Agenten vergeben keine WP-IDs automatisch.

Diese Regel ändert keine allgemeinen NDF-Templates, keinen normativen Execution Contract und keine Regeln in anderen Repositories. Die früheren dokumentierten Umnummerierungen im v1.1-Zyklus (siehe [V1_1_PLAN.md](V1_1_PLAN.md)) bleiben als historische Vorgänge erhalten.

## DE – 8. Offene Evidenzgrenzen

- **WP-160:** Ob die Kennung außerhalb des Repositorys (z. B. in Planungsunterhaltungen) bereits vergeben wurde, ist nicht nachweisbar → reserviert, nicht frei.
- **WP-161:** Eine gesonderte Human-Maintainer-Annahme ist nicht separat belegt; der Commit `b7bebb8` belegt die Aufnahme der Assets, nicht die Form der Annahme.
- **README-Modernisierung (`948b06a`):** ohne WP-ID; keine rückwirkende Zuordnung.
- **Neutralitäts-Fix (`4dab503`):** ohne WP-ID in der Commit-Nachricht; keine rückwirkende Zuordnung durch dieses Register.
- **Governance-Guidances:** Der fachliche Annahmestatus von [NDF_DECISION_AND_STATUS_MODELING_GUIDANCE.md](../governance/NDF_DECISION_AND_STATUS_MODELING_GUIDANCE.md) und [NDF_EXTERNAL_FRAMEWORK_TAILORING_GUIDANCE.md](../governance/NDF_EXTERNAL_FRAMEWORK_TAILORING_GUIDANCE.md) bleibt offen: Commit `ebf716c` belegt die Aufnahme, die Statusfelder melden weiterhin `Implemented, pending Nova review`. Keine WP-ID, keine rückwirkende Annahme.

## DE – 9. Verweis

Inhalt, Prioritäten und Abhängigkeiten der vorgemerkten Kandidaten: [POST_V1_1_CANDIDATE_ROADMAP.md](POST_V1_1_CANDIDATE_ROADMAP.md).

## EN – Summary

This register records the status of NDF work-package IDs **WP-160 to WP-170** for this repository. It does not reconstruct every NDF WP number ever issued.

- **WP-160:** `RESERVED – HISTORICAL ALLOCATION UNRESOLVED` — never reuse; no retroactive assignment to the README modernisation (`948b06a`).
- **WP-161:** historical branding reference, committed in `b7bebb8`; a separate Human-Maintainer acceptance record is not evidenced.
- **WP-162…168:** `RESERVED CANDIDATE – NOT ACTIVATED` — titles reserved, no execution authority, order may differ from numbering.
- **WP-169:** `ACCEPTED WITH NOTES – COMMITTED – PUSHED` (`24760c4`; CP01 accepted; Public Quality Gate CI `success`; no release).
- **WP-170:** `AGENT_COMPLETE – CP01_NOVA_REVIEW_PENDING – HUMAN_ACCEPTANCE_PENDING` — implementation including corrective pass CP01 is agent-complete; the first Nova review returned `REWORK_REQUIRED`; the CP01 re-review and the Human-Maintainer acceptance are pending; execution authority `HUMAN_MAINTAINER_AUTHORIZED`; not accepted.
- **Numbering rule (Human-Maintainer planning decision):** no reuse of issued or referenced IDs; no silent renumbering after external reference; deferred or merged IDs keep their history; a new number needs a traceable Human-Maintainer decision; agents never assign IDs automatically. It changes no general NDF template.

Candidate planning: [POST_V1_1_CANDIDATE_ROADMAP.md](POST_V1_1_CANDIDATE_ROADMAP.md).
