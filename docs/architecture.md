# Architektur

<!-- Lebendes Dokument. Beschreibt die Architektur des Systems: Bausteine, Schnittstellen,
     Datenflüsse, Mandanten-Trennung, Schlüssel- und Datenhaltung.
     Pflege: Architekturentscheidungen werden in decisions.md begründet und hier als Ergebnis
     beschrieben. Offene Fragen stehen in Abschnitt 2, bis sie per ADR entschieden sind.
     Herkunft: initialisiert am 2026-10-09 als Skelett. Inhalt entsteht in Modus 2. -->

## 1. Status

Noch keine Architektur entschieden. Modus 2 startet mit den offenen Fragen in Abschnitt 2.

## 2. Offene Architekturfragen

| ID | Frage | Optionen bisher | Abhängig von | Herkunft |
|---|---|---|---|---|
| A-1 | Welche Basis wird verwendet? | (a) Chat-Frontend + Gateway mit Budgets (Bifrost frei, LiteLLM Enterprise), Mandanten-Ebene selbst bauen; (b) LibreChat mit Mandantenisolation (ab v0.8.7/v0.8.8, noch unreif); (c) Eigenbau | RB-22 (Lizenzen) | H3, V8 |
| A-2 | Mandanten in einem gemeinsamen System oder in getrennten Instanzen? | gemeinsam / Instanz je Mandant | A-1, RB-08, RB-21 | V7, V9, H2 (B3) |
| A-3 | Wie werden Mandantenschlüssel verwaltet und wer hält sie? | offen | RB-01, RB-06 | ADR-002 |
| A-4 | Wie wird Löschung in Backups und beim Anbieter umgesetzt? | z. B. Vernichtung des Mandanten- bzw. Nutzerschlüssels (Kryptoshredding), Zero-Data-Retention | A-3, RB-04 | H2 (B4) |
| A-5 | Wie wird die Abrechnung erfasst und gegen Anbieterrechnungen abgeglichen? | Gateway-Preistabellen + eigener Abgleich | A-1, RB-10 bis RB-12 | ADR-003 |
| A-6 | Wie wird die Betreiber-Ebene (Vorlagen, Grenzen, Metadaten-Überblick) über alle Mandanten umgesetzt? | offen | A-2 | V3 |
| A-7 | Wie wird das manipulationssichere Zugriffsprotokoll (RB-02) umgesetzt? | offen | – | ADR-002 |

## 3. Systemüberblick

<!-- Nach Entscheidung von A-1 und A-2: Bausteine, Verantwortlichkeiten, Datenflüsse. -->

Offen.

## 4. Mandanten-Trennung

<!-- Nach Entscheidung von A-2 und A-3. Muss RB-08 nachweisbar erfüllen. -->

Offen.

## 5. Daten und Verschlüsselung

<!-- Nach Entscheidung von A-3 und A-4. Muss RB-01, RB-04 und RB-05 erfüllen. -->

Offen.

## 6. Abrechnung

<!-- Nach Entscheidung von A-5. Muss RB-10 bis RB-12 erfüllen. -->

Offen.

## 7. Betrieb

<!-- Updates, Backups, Überwachung, Zugriffsprotokoll. Muss RB-02, RB-20 und RB-21 erfüllen. -->

Offen.
