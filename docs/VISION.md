Am 9.10.26 erstellt

# Vision

<!-- Eingangs-Dokument eines Projekts. Wird VOR der Erstellung der anderen Dokumente
     ausgefüllt und bleibt danach als historisches Artefakt im Repo erhalten.
     Zweck: rohe Idee strukturiert erfassen, bevor sie in Konzept und Architektur überführt wird.
     Diese Datei wird nach Initialisierung der anderen Dokumente NICHT mehr verändert –
     spätere Erkenntnisse landen in project-context.md, decisions.md, fahrplan.md.
     Die Vision bleibt als Referenz: „so haben wir es ursprünglich gewollt". -->

<!-- Arbeitstitel: Team-KI-Workspace (Vorbild: TypingMind Teams)
     Erarbeitet in Modus 1 (Konzeptphase) am 2026-10-09.
     Kennzeichnung „(abgeleitet)": Aussage folgt aus Antworten des Vision-Holders,
     wurde aber nicht einzeln bestätigt – in der Härtung prüfen. -->

## 1. Kernidee

Ein selbst gehosteter KI-Workspace, in dem ein Betreiber mehrere voneinander getrennte Gruppen (Mandanten) mit Chat, Agenten und Wissen versorgt. Jeder Mandant verwaltet sich über einen eigenen, technisch nicht versierten Admin selbst – innerhalb der Grenzen, die der Betreiber setzt. Chat und Governance bilden ein zusammenhängendes Produkt; der Verbrauch wird über gezählte Tokens in Geld umgerechnet und abgerechnet.

## 2. Problem und Anlass

- **Welches Problem löst das System?** Bestehende Team-KI-Workspaces bieten keine tragfähige Governance für mehrere Gruppen: Es fehlt eine zweite Verwaltungsebene, auf der Gruppen sich selbst verwalten, eine Inhaltsgrenze gegenüber dem Betreiber und eine Abrechnung in Geld statt bloßer Mengenlimits.
- **Wer hat dieses Problem heute?** Ein einzelner Betreiber, der mehreren Gruppen KI-Zugang bereitstellen will – zunächst für eigene Gruppen, später für fremde, zahlende Organisationen.
- **Wie wird das Problem heute gelöst (oder nicht)?** TypingMind Teams: eine Admin-Ebene pro Instanz, Limits nur über Nachrichten, Zeichen und Tokens, nicht über Geld; Mehrkunden-Betrieb über getrennte Instanzen (Reseller-Modell). Selbst hostbare Alternativen (LibreChat, Open WebUI, LobeChat) bieten Rollen und Gruppen, aber keine Mandanten als eigene Ebene.
- **Warum reicht das nicht?** Die Governance fehlt oder ist zu schwach – insbesondere die **Delegation** an Mandanten-Admins, die ohne Betreiber-Eingriff selbst verwalten.

## 3. Zielbild

Der Betreiber legt einen neuen Mandanten an. Der Mandanten-Admin erhält Zugang, lädt seine Nutzer ein und sortiert sie in Gruppen – danach ist der Mandant arbeitsfähig. Modelle, Agenten, Limits und weitere Einstellungen kommen aus sinnvollen Voreinstellungen, die der Betreiber als Vorgabe für neue Mandanten pflegt (abgeleitet). Die Nutzer arbeiten in einem vollwertigen Chat-Workspace. Der Mandanten-Admin verfeinert Rechte und Kontingente nach Bedarf selbst; der Betreiber sieht dabei nur Metadaten, nie Inhalte. Der Verbrauch jedes Mandanten ist in Euro sichtbar.

**Rollenmodell:**

| Rolle | Verantwortung | Sicht |
|---|---|---|
| Betreiber | Plattform, zentrale API-Schlüssel, strukturelle Grenzen (erlaubte Anbieter/Modelle), Voreinstellungen, Preise | Nur Metadaten (Nutzerzahlen, Verbrauch, Limits, Konfiguration) – technisch erzwungen keine Inhalte |
| Mandanten-Admin | Nutzer, Gruppen, Rechte, Kontingente innerhalb der Betreiber-Grenzen; bei eigenen API-Schlüsseln: Mengen und Budgets allein | Metadaten und Inhalte des eigenen Mandanten |
| Endnutzer | Arbeit im Chat im Rahmen der Freigaben beider Ebenen | Eigene Chats |

**Modellzugänge:** Zentrale API-Schlüssel des Betreibers als Standard; ein Mandant kann sie durch eigene ersetzen. Bei eigenen Schlüsseln gelten nur noch die strukturellen Vorgaben des Betreibers.

**Ausbaustufen:**

- **Stufe 1 – Eigenbetrieb:** Der Betreiber ist selbst erster Mandant und betreibt eigene Gruppen. Umfang: mehrere Mandanten, zwei Verwaltungsebenen, Inhaltsgrenze gegenüber dem Betreiber, Verbrauchsnachweis in Euro auf Token-Basis.
- **Stufe 2 – Kommerzieller Dienst:** Fremde, zahlende Organisationen als Mandanten. Zusätzlich: vollständige Abrechnung mit angebundener Zahlungsabwicklung, AGB und Rechtsrahmen.

**Beispielszenarien:**

- Ein Mandanten-Admin ohne Technikwissen bekommt Zugang, lädt seine Nutzer ein und ordnet sie Gruppen zu. Nach wenigen Minuten arbeiten alle im Workspace – ohne dass er Modelle, Limits oder Agenten selbst einrichten musste.
- Ein Mandant hinterlegt eigene API-Schlüssel. Der Betreiber gibt weiterhin vor, welche Anbieter erlaubt sind; über Mengen und Budgets entscheidet der Mandanten-Admin allein.
- Der Betreiber prüft im Überblick, welcher Mandant wie viel verbraucht hat und was das in Euro kostet – ohne einen einzigen Chatinhalt zu sehen.

## 4. Erfolgskriterien

- **Primär – Laientest:** Eine Person ohne Technikwissen richtet einen Mandanten vollständig und ohne Hilfe ein. Dient als Abnahmekriterium; prüft, dass die Delegation sich selbst trägt.
- **Abrechnungsgenauigkeit (abgeleitet):** Der in Euro ausgewiesene Verbrauch entspricht den tatsächlich vom Modellanbieter berechneten Kosten, pro Modell und über Preisänderungen hinweg.

## 5. Bewusste Abgrenzung

**Was das System ausdrücklich NICHT tun soll:**

- **Keine öffentlichen Chatbots:** keine einbettbaren Widgets, kein Zugang ohne Anmeldung. Der Workspace ist nur für Mitglieder.
- **Kein Modelltraining und kein Fine-Tuning:** Das System nutzt Modelle, macht sie aber nicht.

**Ausdrücklich nicht ausgeschlossen (Entscheidung beim Umfang der Ausbaustufen):**

- Eigene Erweiterungen (Plugins, MCP-Server) durch Mandanten
- Native Apps neben der Web-Oberfläche

## 6. Harte Randbedingungen

- **Technologie:** offen.
- **Hosting:** Self-Hosting.
- **Datenschutz/Compliance:**
  - DSGVO verbindlich. Mandanten sind Verantwortliche, der Betreiber ist Auftragsverarbeiter (Auftragsverarbeitungsvertrag pro Mandant). Modellanbieter und – ab Stufe 2 – Zahlungsdienstleister sind Unterauftragsverarbeiter.
  - Löschung und Auskunft pro Mandant und pro Nutzer, auch ohne dass der Betreiber Inhalte lesen kann.
  - Inhaltsgrenze gegenüber dem Betreiber ist **technisch erzwungen**: Auch mit Server- und Datenbankzugriff sind Inhalte für den Betreiber nicht lesbar; für den Mandanten-Admin schon.
  - Transparenz: Nutzer müssen erkennen können, dass ihr Mandanten-Admin Chats einsehen kann.
- **Lizenzmodell:** proprietär. Nur der Betreiber betreibt das System.
- **Zeitrahmen:** kein harter Termin. Das Projekt läuft nachrangig neben anderen Vorhaben; die Dokumentation muss Wiedereinstiege nach längeren Pausen tragen.
- **Budget für externe Dienste:** Kosten zentraler API-Schlüssel werden über die Token-basierte Abrechnung auf die Mandanten umgelegt; in Stufe 1 trägt der Betreiber sie als erster Mandant selbst.

## 7. Weiche Präferenzen

- Bewährtes vor Neuem – etablierte Bausteine, kein Experimentieren.
- Wiederverwendung vor Eigenbau – bestehende Lösungen ernsthaft als Basis prüfen, nicht nur als Inspiration.
- Wenig Betriebsaufwand – Updates, Backups und Überwachung mit minimalem Eingreifen, da ein einzelner Betreiber.
- Einfachheit der Umsetzung – motiviert die Überlegung, Mandanten in getrennten Instanzen statt in einem gemeinsamen System zu betreiben. Betrifft die Art der Umsetzung, nicht den Funktionsumfang.

## 8. Inspirationen und Vorbilder

- **TypingMind Teams:** Vorbild für den Funktionsumfang – Chat-Workspace mit Projekten, Agenten, Prompt-Bibliothek, Plugins und MCP, Wissensbasis, Branding, SSO, Limit-Gruppen (global, pro Modell, Agent, Plugin, Nutzer), Sichtbarkeitssteuerung, Analytics. Bewusst anders: zweite Verwaltungsebene, Betreiber ohne Inhaltseinsicht, Abrechnung in Geld, Mandanten-Admin ohne Technikwissen. Mehrkunden-Betrieb dort über eine Instanz je Kunde.
- **LibreChat (MIT):** Guthabensystem mit Umrechnung von Tokens in Geld, Startguthaben und automatischer Aufladung; Delegation einzelner Admin-Rechte ohne Voll-Admin. Grenze: Guthaben-Einstellungen global, keine Mandanten-Ebene.
- **Open WebUI:** Verbreitung und Reife. Bewusst nicht ohne Weiteres übernehmbar: Branding-Klausel verbietet das Ersetzen des Open-WebUI-Brandings ohne Enterprise-Lizenz – kritisch für einen Dienst unter eigenem Namen. Nutzerlimits und Abrechnung nur über Erweiterungen bzw. Zusatzprojekte.
- **LobeChat / LobeHub:** Agenten als zentrale Arbeitseinheit, großer Skill-Marktplatz. Eigene Community-Lizenz mit Einschränkungen für veränderte Fassungen; Lizenzgeberin kann Bedingungen ändern. LDAP und SCIM fehlen.
- **Gateway-Muster (z. B. LiteLLM):** Governance als eigene Schicht vor den Modellen – Schlüssel pro Mandant mit Limits, Kostenzuordnung je Mandant. Vorbild dafür, dass Chat und Governance getrennt sein können. Lizenz und Eignung nicht geprüft.

## 9. Bekannte Risiken und offene Punkte

- **Betreiberblindheit nur begrenzt machbar:** Chatnachrichten müssen im Klartext an Modelle gehen, Wissensdaten müssen gelesen und durchsucht werden – auf einem System, das der Betreiber kontrolliert. Zu klären: „geschützt im Ruhezustand" oder „geschützt auch während der Verarbeitung". Bei zentralen API-Schlüsseln laufen Inhalte zudem über den Anbieter-Account des Betreibers.
- **Kommerzieller Dienst als Nebenprojekt:** Haftung, Gewerbe, Umsatzsteuer, AGB, Auftragsverarbeitungsverträge und Zahlungsabwicklung vertragen sich schlecht mit „ohne Termin, wenn Kapazität da ist". Entschärft durch Ausbaustufe 1 (Eigenbetrieb).
- **Nutzungsbedingungen der Modellanbieter:** Weiterverkauf von API-Zugang an Dritte muss vor Stufe 2 pro Anbieter geprüft werden.
- **Abrechnungsgenauigkeit:** Gezählte Tokens müssen den tatsächlichen Anbieterkosten entsprechen; ab Stufe 2 rechtlich relevant.
- **Vorfinanzierung:** Anbieter berechnen Kosten, bevor Mandanten zahlen. Prepaid-Guthaben als möglicher Ausgleich.
- **Testperson für den Laientest:** noch nicht benannt; der Betreiber selbst ist zu nah dran.
- **Umfang:** Funktionsgleichstand mit TypingMind plus vier eigene Unterscheidungsmerkmale, betrieben von einer Person.
- **Lizenzlage bestehender Lösungen:** Branding-Klausel (Open WebUI), Community-Lizenz (LobeChat) und AGPL-Komponenten begrenzen die Wiederverwendung; bei Betrieb als Dienst für Mandanten verpflichtet AGPL zur Offenlegung eigener Änderungen.
- **Mandanten-Trennung lösungsneutral:** Ob Mandanten in einem gemeinsamen System oder in getrennten Instanzen laufen, ist offen und Architekturfrage für Modus 2. Ab Stufe 2 muss die Trennung vertrauensfest sein – ein Datenleck zwischen zahlenden Mandanten wäre der schwerste denkbare Fehler.
- **Arbeitsrechtliche Relevanz des Mitlesens:** Sind Mandanten Arbeitgeber, ist die Einsicht des Mandanten-Admins in Chats heikel; das System muss die nötige Transparenz ermöglichen.

## 10. Was diese Vision nicht ersetzt

Dieses Dokument ist Eingang in die Konzeptphase, nicht ihr Ergebnis.
Es ersetzt **nicht**:

- die Architekturentscheidung (kommt in `architecture.md`)
- die Stack-Entscheidung (kommt in `project-context.md` und `decisions.md`)
- die Roadmap (kommt in `fahrplan.md`)
- die Constraints in operationalisierter Form (kommt in `project-context.md`)

---

**Überführungs-Status:**

- [x] Vision von Mensch ausgefüllt
- [x] Konzeptphase abgeschlossen (Lücken geschlossen, Optionen entschieden)
- [ ] Härtungsphase abgeschlossen (Blocker und Inkonsistenzen geprüft)
- [ ] Vorlagen-Set initialisiert (project-context.md, architecture.md, fahrplan.md, decisions.md, blockers.md)
- [ ] ADR-001 angelegt: Anpassung des Vorlagen-Sets
- [ ] Datum der Initialisierungs-Abschluss: [YYYY-MM-DD]

**Nach abgeschlossener Initialisierung:** Diese Datei wird nicht mehr verändert.
Spätere Vision-Erweiterungen oder Pivots werden in einem ADR dokumentiert,
nicht in dieser Datei. Bei substantieller Vision-Änderung: neuer ADR mit Verweis hier.
