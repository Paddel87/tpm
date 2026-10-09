# Architektur

<!-- Lebendes Dokument. Beschreibt die Architektur des Systems: Bausteine, Schnittstellen,
     Datenflüsse, Mandanten-Trennung, Schlüssel- und Datenhaltung.
     Pflege: Architekturentscheidungen werden in decisions.md begründet und hier als Ergebnis
     beschrieben. Offene Fragen stehen in Abschnitt 2, bis sie per ADR entschieden sind.
     Herkunft: initialisiert am 2026-10-09 als Skelett. Inhalt entsteht in Modus 2. -->

## 1. Status

Modus 2 läuft. Entschieden (unter PoC-Vorbehalt): Basis (A-1 → ADR-006, ADR-007) und Mandanten-Trennung (A-2 → ADR-008). Offen: A-3 bis A-7.

## 2. Offene Architekturfragen

| ID | Frage | Optionen bisher | Abhängig von | Herkunft |
|---|---|---|---|---|
| A-3 | Wie werden Mandantenschlüssel verwaltet und wer hält sie? Wie werden MongoDB (Community: nur explizite Feldverschlüsselung), Meilisearch und Vektor-DB im Ruhezustand geschützt? | z. B. App-seitige Verschlüsselung mit Mandantenschlüssel aus einem KMS; Verschlüsselung der Datenträger je Mandant; Meilisearch abschalten | RB-01, RB-06, ADR-008 | ADR-002, ADR-006 |
| A-4 | Wie wird Löschung in Backups und beim Anbieter umgesetzt? | z. B. Vernichtung des Mandanten- bzw. Nutzerschlüssels (Kryptoshredding), Zero-Data-Retention | A-3, RB-04 | H2 (B4) |
| A-5 | Wie wird die Abrechnung erfasst und gegen Anbieterrechnungen abgeglichen? | Rahmen gesetzt (ADR-007): Bifrost-Echtzeitkosten, ein Anbieter-Projekt je Mandant, täglicher Abgleich gegen Kosten-APIs, Monatsrechnung maßgeblich. Offen: Umsetzung, Kursquelle | RB-10 bis RB-12 | ADR-003, ADR-007 |
| A-6 | Wie wird die Betreiber-Ebene (Instanzen anlegen, Vorlagen, Grenzen, Metadaten-Überblick) über alle Mandanten-Instanzen umgesetzt? | offen | ADR-008 | V3 |
| A-7 | Wie wird das manipulationssichere Zugriffsprotokoll (RB-02) umgesetzt? | offen | – | ADR-002 |

## 3. Systemüberblick

```
Browser ──► Reverse-Proxy (TLS, Subdomain je Mandant)
              │
              ├──► LibreChat-Instanz Mandant A ──┐
              ├──► LibreChat-Instanz Mandant B ──┤
              │                                  ├──► Bifrost (Gateway) ──► Modellanbieter
              │                                  │     Customer = Mandant      (Projekt/Workspace
              │                                  │     Team = Gruppe            je Mandant oder
              │                                  │     Virtual Key je Nutzer    eigener Schlüssel)
              │                                  │
              ├──► Mandanten-Admin-Oberfläche ───┤  (Eigenbau, laientauglich)
              └──► Betreiber-Ebene ──────────────┘  (Eigenbau: Instanzen, Vorlagen, Grenzen, Metadaten)

DB-Server (gemeinsam): je Mandant eigene Datenbank und eigener Zugang
Abrechnungsdienst (Eigenbau): Abgleich Bifrost ↔ Anbieter-Kosten-APIs, EUR-Umrechnung
```

| Baustein | Herkunft | Verantwortung |
|---|---|---|
| Reverse-Proxy | Standardkomponente (offen) | TLS, Zuordnung Subdomain → Mandanten-Instanz |
| LibreChat je Mandant | LibreChat (ADR-006) | Chat, Agenten, Wissen, MCP, Teilen in Gruppen |
| Bifrost | Bifrost OSS (ADR-007) | Budgets, Modell-Freigaben, Kostenerfassung; kein Inhaltslogging |
| Mandanten-Admin-Oberfläche | Eigenbau | Nutzer, Gruppen, Rechte, Kontingente, Vorlagen, eigene Schlüssel, Einsichtsmodus, Branding |
| Betreiber-Ebene | Eigenbau | Mandanten anlegen und sperren, Vorlagen, erlaubte Anbieter und Modelle, Preise, Metadaten-Überblick |
| Abrechnungsdienst | Eigenbau | täglicher Abgleich, Monatsabschluss, EUR-Umrechnung |

## 4. Mandanten-Trennung

Entschieden in ADR-008: eigene LibreChat-Instanz, eigene Datenbank und eigener Datenbank-Zugang je Mandant; gemeinsam sind DB-Server, Gateway und Reverse-Proxy. Im Gateway ist jeder Mandant ein eigener Customer mit eigenen Virtual Keys.

Offen: Trennung von Meilisearch und Vektor-Datenbank je Mandant (eigener Index bzw. eigene Datenbank) – mit A-3 klären.

## 5. Daten und Verschlüsselung

<!-- Nach Entscheidung von A-3 und A-4. Muss RB-01, RB-04 und RB-05 erfüllen. -->

Offen.

## 6. Abrechnung

<!-- Nach Entscheidung von A-5. Muss RB-10 bis RB-12 erfüllen. -->

Offen.

## 7. Betrieb

<!-- Updates, Backups, Überwachung, Zugriffsprotokoll. Muss RB-02, RB-20 und RB-21 erfüllen. -->

Offen.

## 8. Proof of Concept (Vorbehalt für ADR-006 bis ADR-008)

Alle Kriterien müssen bestehen; scheitert eines, wird die betroffene Entscheidung per neuem ADR ersetzt.

| ID | Prüfkriterium | betrifft |
|---|---|---|
| P-1 | Zwei LibreChat-Instanzen mit getrennten Datenbanken auf einem Server; keine Daten der einen Instanz in der anderen sichtbar. | ADR-008 |
| P-2 | Ressourcenbedarf je Instanz gemessen; Hochrechnung für 10 Mandanten passt auf einen bezahlbaren Server. | ADR-008 |
| P-3 | Bifrost OSS: Budgets auf Customer-, Team- und Virtual-Key-Ebene greifen und sperren bei Überschreitung. | ADR-007 |
| P-4 | Bifrost: mit `disable_content_logging: true` landen keine Prompts oder Antworten in der Datenbank. | ADR-007, RB-03 |
| P-5 | Bifrost: Kosten für Anfragen mit Cache und Reasoning (Anthropic, OpenAI, Gemini) weichen höchstens 2 % von den Anbieter-Kosten-APIs ab. | ADR-007, RB-11 |
| P-6 | LibreChat übergibt Nutzer- bzw. Virtual-Key-Zuordnung zuverlässig an Bifrost, sodass jede Anfrage dem richtigen Nutzer, der Gruppe und dem Mandanten zugeordnet ist. | ADR-006, ADR-007 |
| P-7 | Branding (Name, Logo) je LibreChat-Instanz ohne Codeänderung setzbar, oder Aufwand der Änderung abgeschätzt. | ADR-006 |
