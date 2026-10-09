# Projektkontext

<!-- Lebendes Dokument. Erster Einstieg für jede Arbeitssitzung – auch nach langen Pausen.
     Enthält: aktuellen Stand, Randbedingungen in operationalisierter (prüfbarer) Form,
     Stack (sobald entschieden) und Glossar.
     Pflege: bei jeder Statusänderung „Aktueller Stand" aktualisieren; neue Randbedingungen
     nur mit Verweis auf eine Entscheidung in decisions.md.
     Herkunft: initialisiert am 2026-10-09 aus VISION.md und haertung-vision.md. -->

## 1. Wiedereinstieg

Beim Wiedereinstieg in dieser Reihenfolge lesen:

1. **Aktueller Stand** (Abschnitt 2) – wo steht das Projekt, was ist der nächste Schritt?
2. `blockers.md` – was ist offen oder blockiert?
3. `fahrplan.md` – welche Phase läuft, was ist das nächste Ziel?
4. `decisions.md` – welche Entscheidungen gelten?
5. Bei Bedarf: `VISION.md` (ursprüngliche Absicht, eingefroren), `haertung-vision.md` (Härtung mit Quellen) und `recherche-basis.md` (Basiswahl mit Quellen).

## 2. Aktueller Stand

- **Datum:** 2026-10-09
- **Phase:** Modus 2 (Architektur) läuft. Basis und Mandanten-Trennung entschieden (ADR-006 bis ADR-008, unter PoC-Vorbehalt).
- **Nächster Schritt:** A-3 (Schlüsselverwaltung und Verschlüsselung im Ruhezustand) entscheiden; parallel Proof of Concept P-1 bis P-7 vorbereiten (`architecture.md` Abschnitt 8).
- **Code:** noch keiner.

## 3. Projekt in einem Satz

Selbst gehosteter KI-Workspace, in dem ein Betreiber mehrere Mandanten mit Chat, Agenten und Wissen versorgt; jeder Mandant verwaltet sich über einen technisch nicht versierten Admin selbst, der Betreiber sieht nur Metadaten, und Verbrauch wird in Euro abgerechnet.

## 4. Randbedingungen (operationalisiert)

Jede Randbedingung ist so formuliert, dass sie prüfbar ist. Spalte „Quelle" verweist auf Vision (V), Härtungsbericht (H) oder Entscheidung (ADR).

### 4.1 Inhaltsgrenze und Datenschutz

| ID | Randbedingung | Prüfung | Quelle |
|---|---|---|---|
| RB-01 | Inhalte (Chats, Dateien, Wissen) sind in Datenbank, Dateiablage und Backups mit mandantenspezifischen Schlüsseln verschlüsselt. Mit Server- oder Datenbankzugriff allein sind sie für den Betreiber nicht lesbar. | Datenbank-Dump und Backup ohne Mandantenschlüssel enthalten keinen lesbaren Inhalt. | V6, ADR-002 |
| RB-02 | Während der Verarbeitung gilt organisatorische Absicherung: jeder administrative Zugriff auf Server oder Daten wird protokolliert; Selbstverpflichtung und Zusage im Auftragsverarbeitungsvertrag. | Zugriffsprotokoll vorhanden und manipulationssicher abgelegt; AVV-Vorlage enthält die Zusage. | V6, ADR-002 |
| RB-03 | Bei zentralen API-Schlüsseln ist die Inhaltsprotokollierung in den Anbieter-Konten abgeschaltet; Zero-Data-Retention ist beantragt, wo der Anbieter sie anbietet. | Konto-Einstellungen je Anbieter dokumentiert. | V9, H3 |
| RB-04 | Löschung pro Nutzer und pro Mandant erstreckt sich auf Live-Daten und Backups und ist ohne Lesezugriff des Betreibers durchführbar. | Nach Löschung ist der Inhalt auch aus wiederhergestelltem Backup nicht lesbar. | V6, H2 (B4) |
| RB-05 | Auskunft (Art. 15 DSGVO) pro Nutzer ist durch den Mandanten-Admin exportierbar, ohne Betreiber-Beteiligung am Inhalt. | Export-Funktion im Mandanten-Admin vorhanden. | V6 |
| RB-06 | Einsichtsmodus pro Mandant: aus / nur bei Anlass (Begründung + Protokoll) / immer. Der aktuelle Modus ist für jeden Nutzer sichtbar. | Moduswechsel wirkt sofort; Anzeige im Nutzer-Interface; Anlass-Einsichten im Protokoll. | V3, ADR-004 |
| RB-07 | DSGVO gilt ab Stufe 1. Betreiber ist Auftragsverarbeiter je Mandant, für den eigenen Mandanten Verantwortlicher. Hoster, Modellanbieter und ab Stufe 2 Zahlungsdienstleister sind Unterauftragsverarbeiter. | AVV je Mandant, Liste der Unterauftragsverarbeiter gepflegt. | V6 |
| RB-08 | Keine Daten oder Inhalte über Mandantengrenzen hinweg sichtbar – weder für Nutzer noch für Mandanten-Admins. | Automatisierte Isolationstests je Release. | V3, V9 |

### 4.2 Abrechnung

| ID | Randbedingung | Prüfung | Quelle |
|---|---|---|---|
| RB-10 | Verbrauch wird in Euro getrennt nach Anbieterkosten und Betreiberpreis (Kosten plus Aufschlag) ausgewiesen. | Beide Werte je Mandant und Zeitraum sichtbar. | V3, ADR-003 |
| RB-11 | Ausgewiesene Anbieterkosten weichen pro Monat höchstens 2 % von der Anbieterrechnung ab, pro Modell und über Preisänderungen hinweg. | Monatlicher Abgleich gegen Anbieterrechnung; Abweichung protokolliert. | V4, ADR-003 |
| RB-12 | Umrechnung USD → EUR mit festem, dokumentiertem Wechselkurs-Stichtag. | Stichtag und Kurs je Abrechnungszeitraum gespeichert. | V4, ADR-003 |

### 4.3 Betrieb und Hosting

| ID | Randbedingung | Prüfung | Quelle |
|---|---|---|---|
| RB-20 | Betrieb auf gemietetem Server bei einem Hoster in der EU; kein fremder SaaS für den Workspace selbst. | Hoster-Vertrag mit EU-Standort und AVV. | V6, ADR-005 |
| RB-21 | Betrieb durch eine Person: Updates, Backups und Überwachung laufen weitgehend automatisch. | Konkrete Zielwerte in Modus 2 festlegen. | V7 |
| RB-22 | Lizenzmodell proprietär; nur der Betreiber betreibt das System. Wiederverwendete Komponenten dürfen das nicht verhindern (Branding-Klauseln, Mehrmandanten-Verbote, AGPL-Offenlegungspflichten prüfen). | Lizenzprüfung je Komponente in `decisions.md`. | V6, V8 |

### 4.4 Abgrenzung

| ID | Randbedingung | Quelle |
|---|---|---|
| RB-30 | Kein Zugang ohne Anmeldung, keine einbettbaren Widgets, keine öffentlichen Chatbots. | V5 |
| RB-31 | Kein Modelltraining, kein Fine-Tuning. | V5 |
| RB-32 | Zugelassen sind nur Anbieter und Modelle, die der Betreiber freigibt – auch bei eigenen API-Schlüsseln eines Mandanten. | V3 |
| RB-33 | Nutzung der Modell-APIs nur im Rahmen der Anbieterbedingungen: kein Weiterverkauf von Schlüsseln oder Konten, kein reiner API-Durchreich-Dienst. | V9, H3 |

## 5. Abnahmekriterien

- **Laientest (primär):** Eine Person ohne Technikwissen richtet einen vom Betreiber angelegten Mandanten ohne Hilfe vollständig ein: Nutzer einladen und Gruppen zuordnen, Rechte und Kontingente anpassen, eigene API-Schlüssel hinterlegen, Einsichtsmodus wählen, Name und Logo setzen. Testperson: noch nicht benannt (siehe `blockers.md`).
- **Abrechnungsgenauigkeit:** RB-11 über mindestens einen vollen Monat erfüllt.

## 6. Stack

Teilweise entschieden (unter PoC-Vorbehalt). Entscheidungen werden in `decisions.md` festgehalten und hier zusammengefasst.

| Bereich | Wahl | ADR |
|---|---|---|
| Chat-Frontend / Basis | LibreChat (MIT), eine Instanz je Mandant | ADR-006, ADR-008 |
| Gateway / Abrechnung | Bifrost OSS (Apache-2.0), Inhaltslogging aus | ADR-007 |
| Datenbank | MongoDB (durch LibreChat vorgegeben), eigene Datenbank je Mandant; dazu Meilisearch und Postgres/pgvector | ADR-006, ADR-008 |
| Verschlüsselung / Schlüsselverwaltung | offen | – |
| Hoster | offen (EU) | ADR-005 |

## 7. Glossar

| Begriff | Bedeutung |
|---|---|
| Betreiber | Person, die die Plattform betreibt, zentrale API-Schlüssel hält und strukturelle Grenzen setzt. Sieht nur Metadaten. |
| Mandant | Voneinander getrennte Organisation oder Gruppe auf der Plattform, mit eigenem Admin, eigenen Nutzern und eigenen Inhalten. |
| Mandanten-Admin | Verwaltet Nutzer, Gruppen, Rechte, Kontingente, Vorlagen und Einsichtsmodus eines Mandanten. Kein Technikwissen vorausgesetzt. |
| Endnutzer | Arbeitet im Chat-Workspace eines Mandanten. |
| Gruppe | Teilmenge der Nutzer eines Mandanten; Einheit für Rechte, Kontingente und Teilen. |
| Einsichtsmodus | Einstellung je Mandant, ob der Mandanten-Admin Chats seiner Nutzer sehen kann: aus / bei Anlass / immer. |
| Vorlage | Voreinstellung (Modelle, Agenten, Limits). Betreiber-Vorlagen gelten für neue Mandanten, Mandanten-Vorlagen für Gruppen. |
| Anbieterkosten | Vom Modellanbieter berechnete Kosten, in Euro umgerechnet. |
| Betreiberpreis | Anbieterkosten plus Aufschlag des Betreibers. |
| Stufe 1 / Stufe 2 | Ausbaustufen: Eigenbetrieb für eigene Gruppen / kommerzieller Dienst für zahlende Organisationen. |
| Modus 1 / Modus 2 | Projektphasen: Konzept (Vision) / Architektur. |
