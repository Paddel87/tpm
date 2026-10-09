# Blocker und offene Punkte

<!-- Lebendes Dokument. Alles, was eine Entscheidung oder einen Fortschritt aufhält oder
     vor einer bestimmten Phase geklärt sein muss.
     Pflege: neue Punkte mit nächster freier ID anlegen; erledigte Punkte nicht löschen,
     sondern nach „Erledigt" verschieben, mit Datum und Verweis auf die Lösung.
     Schwere: Blocker (hält die aktuelle Phase auf) · Offen (muss vor der genannten Phase geklärt sein)
     Herkunft: initialisiert am 2026-10-09 aus haertung-vision.md. -->

## Aktiv

| ID | Punkt | Schwere | Fällig vor | Herkunft |
|---|---|---|---|---|
| B-03 | Löschkonzept für Backups und beim Anbieter gespeicherte Inhalte. | Offen | Phase 2 | H2 (B4), A-4 |
| B-04 | Rechtsgrundlage der Drittlandübermittlung je Modellanbieter (EU-US Data Privacy Framework, Standardvertragsklauseln). | Offen | Phase 2 | H2 (C6) |
| B-05 | Abrechnungsmodell für Mandanten mit eigenen API-Schlüsseln (z. B. Plattformgebühr). | Offen | Phase 3 | H2 (C7) |
| B-06 | Unbestätigte Anbieterangaben prüfen: Anthropic-Aufbewahrung angeblich auf 7 Tage verkürzt; Mistral soll die Zusage „kein Training auf Daten bezahlter API-Nutzer" gestrichen haben. | Offen | Phase 3 | H3 |
| B-07 | Testperson für den Laientest nicht benannt; der Betreiber selbst ist zu nah dran. | Offen | Ende Phase 2 | V9 |
| B-09 | LibreChat erscheint als Pre-release in schnellem Takt unter neuem Eigentümer (ClickHouse); Schnittstellen ändern sich häufig, eine Umstellung der Datenbank (FerretDB/Postgres) ist angedacht. | Offen | laufend | ADR-006 |
| B-10 | Proof of Concept für ADR-006 bis ADR-008 steht aus (Prüfkriterien in `architecture.md` Abschnitt 8). | Blocker | Phase 2 | ADR-006 bis ADR-008 |
| B-11 | Obergrenzen für Projekte bzw. Workspaces pro Organisation bei OpenAI, Anthropic, Google und Mistral ungeprüft (ein Projekt je Mandant). | Offen | Phase 2 | ADR-007 |

## Erledigt

| ID | Punkt | Erledigt am | Lösung |
|---|---|---|---|
| B-01 | Keine fertige Basis | 2026-10-09 | ADR-006, ADR-007 (PoC-Vorbehalt, B-10) |
| B-02 | Mandanten-Trennung offen | 2026-10-09 | ADR-008 (PoC-Vorbehalt, B-10) |
| B-08 | Open-WebUI-Lizenzschwelle | 2026-10-09 | gegenstandslos: Open WebUI verworfen (ADR-006) |
| – | Bedrohungsmodell der Inhaltsgrenze (Härtung A1) | 2026-10-09 | ADR-002 |
| – | Kosten oder Preis im Verbrauchsausweis, Genauigkeit (Härtung B1, B2) | 2026-10-09 | ADR-003 |
| – | Einsicht des Mandanten-Admins in Chats (Härtung C4) | 2026-10-09 | ADR-004 |
| – | Bedeutung von Self-Hosting (Härtung C5) | 2026-10-09 | ADR-005 |
