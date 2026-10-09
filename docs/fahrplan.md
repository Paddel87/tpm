# Fahrplan

<!-- Lebendes Dokument. Phasen und Meilensteine des Projekts mit Status.
     Kein Termin: Das Projekt läuft nachrangig neben anderen Vorhaben (VISION.md, Abschnitt 6).
     Reihenfolge und Abhängigkeiten zählen, nicht Daten.
     Pflege: Status bei jedem abgeschlossenen Schritt aktualisieren; neue Meilensteine mit
     Begründung, größere Umplanungen per ADR in decisions.md.
     Status: [ ] offen · [~] in Arbeit · [x] erledigt
     Herkunft: initialisiert am 2026-10-09. -->

## Phase 0 – Konzept (Modus 1)

- [x] Vision erfasst (`VISION.md`)
- [x] Härtung abgeschlossen (`haertung-vision.md`)
- [x] Vorlagen-Set initialisiert, ADR-001 angelegt

## Phase 1 – Architektur (Modus 2)

Ziel: alle offenen Fragen aus `architecture.md` Abschnitt 2 per ADR entschieden, Stack festgelegt.

- [x] A-1 Basiswahl – LibreChat + Bifrost OSS (ADR-006, ADR-007)
- [x] A-2 Mandanten-Trennung – App-Instanz je Mandant (ADR-008)
- [ ] Proof of Concept P-1 bis P-7 (`architecture.md` Abschnitt 8)
- [ ] A-3 Schlüsselverwaltung
- [ ] A-4 Löschkonzept (Backups, Anbieterdaten)
- [ ] A-5 Abrechnungserfassung und Abgleich
- [ ] A-6 Betreiber-Ebene
- [ ] A-7 Zugriffsprotokoll
- [ ] Muss/Kann-Liste für Stufe 1 festlegen (Abschnitt „Umfang Stufe 1" unten füllen)
- [ ] Rechtsgrundlage der Drittlandübermittlung je Modellanbieter klären (B-04)
- [ ] Stack in `project-context.md` Abschnitt 6 eintragen

## Phase 2 – Stufe 1: Eigenbetrieb

Ziel: Betreiber und eigene Gruppen arbeiten produktiv; Laientest bestanden.

- [ ] Hoster gewählt, Server eingerichtet (RB-20)
- [ ] Mandanten-Isolation inkl. automatisierter Tests (RB-08)
- [ ] Verschlüsselung im Ruhezustand und Zugriffsprotokoll (RB-01, RB-02)
- [ ] Anbieter-Konten konfiguriert: Logging aus, Zero-Data-Retention beantragt (RB-03)
- [ ] Zwei Verwaltungsebenen mit Vorlagen und Einsichtsmodus (RB-06)
- [ ] Verbrauchsausweis in Euro und monatlicher Abgleich (RB-10 bis RB-12)
- [ ] DSGVO-Unterlagen: AVV-Vorlage, Liste der Unterauftragsverarbeiter, Datenschutzhinweise (RB-07)
- [ ] Testperson benannt und Laientest bestanden

### Umfang Stufe 1

<!-- In Modus 2 füllen. Rahmen laut Vision: Kern-Chat-Workspace plus die vier
     Unterscheidungsmerkmale; TypingMind-Funktionsgleichstand ist Richtung, nicht Pflicht. -->

| Funktion | Muss / Kann | Bemerkung |
|---|---|---|
| Mehrere Mandanten, zwei Verwaltungsebenen | Muss | Vision |
| Inhaltsgrenze gegenüber dem Betreiber | Muss | Vision, ADR-002 |
| Verbrauchsausweis in Euro | Muss | Vision, ADR-003 |
| Mandanten-Admin ohne Technikwissen (Laientest) | Muss | Vision |
| Teilen innerhalb von Gruppen | offen | in Vision vorgesehen (C3), Stufe offen |
| weitere Funktionen | offen | Modus 2 |

## Phase 3 – Stufe 2: Kommerzieller Dienst

Ziel: fremde, zahlende Organisationen als Mandanten.

- [ ] Rechtsrahmen: Gewerbe, Umsatzsteuer, AGB, Haftung
- [ ] Anbieterbedingungen erneut prüfen, unbestätigte Punkte klären (B-06)
- [ ] Abrechnungsmodell für Mandanten mit eigenen API-Schlüsseln (B-05)
- [ ] Zahlungsabwicklung und Prepaid-Guthaben
- [ ] Vertrauensfeste Mandanten-Trennung nachgewiesen
