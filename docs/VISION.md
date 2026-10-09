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
     wurde aber nicht einzeln bestätigt – in der Härtung prüfen.
     Härtung am 2026-10-09: Befund, Faktencheck und Entscheidungen in docs/haertung-vision.md.
     Alle „(abgeleitet)"-Aussagen wurden dabei bestätigt oder präzisiert. -->

## 1. Kernidee

Ein selbst gehosteter KI-Workspace, in dem ein Betreiber mehrere voneinander getrennte Gruppen (Mandanten) mit Chat, Agenten und Wissen versorgt. Jeder Mandant verwaltet sich über einen eigenen, technisch nicht versierten Admin selbst – innerhalb der Grenzen, die der Betreiber setzt. Chat und Governance bilden ein zusammenhängendes Produkt; der Verbrauch wird über gezählte Tokens in Geld umgerechnet und abgerechnet.

## 2. Problem und Anlass

- **Welches Problem löst das System?** Bestehende Team-KI-Workspaces bieten keine tragfähige Governance für mehrere Gruppen: Es fehlt eine zweite Verwaltungsebene, auf der Gruppen sich selbst verwalten, eine Inhaltsgrenze gegenüber dem Betreiber und eine Abrechnung in Geld statt bloßer Mengenlimits.
- **Wer hat dieses Problem heute?** Ein einzelner Betreiber, der mehreren Gruppen KI-Zugang bereitstellen will – zunächst für eigene Gruppen, später für fremde, zahlende Organisationen.
- **Wie wird das Problem heute gelöst (oder nicht)?** TypingMind Teams: Admin-Rollen nur innerhalb einer Instanz, Limits nur über Nachrichten, Zeichen und Tokens, nicht über Geld; Mehrkunden-Betrieb bisher über getrennte Instanzen (Reseller-Modell, seit März 2026 ausgesetzt). Selbst hostbare Alternativen (LibreChat, Open WebUI, LobeChat) bieten Rollen und Gruppen, aber keine ausgereifte Mandanten-Ebene; bei LibreChat ist sie im Aufbau (Abschnitt 8).
- **Warum reicht das nicht?** Die Governance fehlt oder ist zu schwach – insbesondere die **Delegation** an Mandanten-Admins, die ohne Betreiber-Eingriff selbst verwalten.

## 3. Zielbild

Der Betreiber legt einen neuen Mandanten an. Der Mandanten-Admin erhält Zugang, lädt seine Nutzer ein und sortiert sie in Gruppen – danach ist der Mandant arbeitsfähig. Modelle, Agenten, Limits und weitere Einstellungen kommen aus sinnvollen Voreinstellungen, die der Betreiber als Vorlage für neue Mandanten pflegt. Der Mandanten-Admin kann zusätzlich eigene Vorlagen für seine Gruppen pflegen. Die Nutzer arbeiten in einem vollwertigen Chat-Workspace und können Projekte, Agenten und Wissensbasen innerhalb ihrer Gruppen teilen – nie über Mandantengrenzen hinweg. Der Mandanten-Admin verfeinert Rechte und Kontingente nach Bedarf selbst; der Betreiber sieht dabei nur Metadaten, nie Inhalte. Der Verbrauch jedes Mandanten ist in Euro sichtbar, getrennt nach Anbieterkosten und Betreiberpreis.

**Rollenmodell:**

| Rolle | Verantwortung | Sicht |
|---|---|---|
| Betreiber | Plattform, zentrale API-Schlüssel, strukturelle Grenzen (erlaubte Anbieter/Modelle), Voreinstellungen, Preise (Anbieterkosten plus Aufschlag) | Nur Metadaten (Nutzerzahlen, Verbrauch, Limits, Konfiguration) – keine Inhalte (Schutzumfang siehe Abschnitt 6) |
| Mandanten-Admin | Nutzer, Gruppen, Rechte, Kontingente, eigene Vorlagen, Einsichtsmodus innerhalb der Betreiber-Grenzen; bei eigenen API-Schlüsseln: Mengen und Budgets allein | Metadaten des eigenen Mandanten; Inhalte gemäß gewähltem Einsichtsmodus |
| Endnutzer | Arbeit im Chat im Rahmen der Freigaben beider Ebenen; Teilen innerhalb der eigenen Gruppen | Eigene Chats und in ihren Gruppen geteilte Inhalte; der aktuelle Einsichtsmodus ist für sie sichtbar |

**Einsichtsmodus:** Der Mandanten-Admin legt pro Mandant fest, ob er Chats seiner Nutzer einsehen kann: aus, nur bei Anlass (begründet und protokolliert) oder immer.

**Modellzugänge:** Zentrale API-Schlüssel des Betreibers als Standard; ein Mandant kann sie durch eigene ersetzen. Bei eigenen Schlüsseln gelten nur noch die strukturellen Vorgaben des Betreibers.

**Ausbaustufen:**

- **Stufe 1 – Eigenbetrieb:** Der Betreiber ist selbst erster Mandant und betreibt eigene Gruppen; diese bestehen aus anderen Personen (z. B. Verein, Familie, Bekannte), daher gilt die DSGVO bereits ab Stufe 1. Umfang: Kern-Chat-Workspace plus die vier Unterscheidungsmerkmale – mehrere Mandanten mit zwei Verwaltungsebenen, Inhaltsgrenze gegenüber dem Betreiber, Verbrauchsnachweis in Euro auf Token-Basis, Mandanten-Admin ohne Technikwissen. Funktionsgleichstand mit TypingMind ist Richtung, nicht Pflicht; die konkrete Muss/Kann-Liste entsteht in Modus 2 (`fahrplan.md`).
- **Stufe 2 – Kommerzieller Dienst:** Fremde, zahlende Organisationen als Mandanten. Zusätzlich: vollständige Abrechnung mit angebundener Zahlungsabwicklung, AGB und Rechtsrahmen.

**Beispielszenarien:**

- Ein Mandanten-Admin ohne Technikwissen bekommt Zugang, lädt seine Nutzer ein und ordnet sie Gruppen zu. Nach wenigen Minuten arbeiten alle im Workspace – ohne dass er Modelle, Limits oder Agenten selbst einrichten musste.
- Ein Mandant hinterlegt eigene API-Schlüssel. Der Betreiber gibt weiterhin vor, welche Anbieter erlaubt sind; über Mengen und Budgets entscheidet der Mandanten-Admin allein.
- Der Betreiber prüft im Überblick, welcher Mandant wie viel verbraucht hat und was das in Euro kostet – ohne einen einzigen Chatinhalt zu sehen.

## 4. Erfolgskriterien

- **Primär – Laientest:** Eine Person ohne Technikwissen richtet einen vom Betreiber angelegten Mandanten vollständig und ohne Hilfe ein. „Vollständig" umfasst: Nutzer einladen und Gruppen zuordnen, Rechte und Kontingente anpassen, eigene API-Schlüssel hinterlegen, Einsichtsmodus wählen sowie Name und Logo des Mandanten setzen. Dient als Abnahmekriterium; prüft, dass die Delegation sich selbst trägt.
- **Abrechnungsgenauigkeit:** Die ausgewiesenen Anbieterkosten weichen pro Monat höchstens 2 % von der tatsächlichen Rechnung des Modellanbieters ab, pro Modell und über Preisänderungen hinweg. Geprüft durch monatlichen Abgleich gegen die Anbieterrechnung, mit festem Wechselkurs-Stichtag (Anbieter rechnen in USD ab). Der Betreiberpreis wird getrennt davon ausgewiesen.

## 5. Bewusste Abgrenzung

**Was das System ausdrücklich NICHT tun soll:**

- **Keine öffentlichen Chatbots:** keine einbettbaren Widgets, kein Zugang ohne Anmeldung. Der Workspace ist nur für Mitglieder.
- **Kein Modelltraining und kein Fine-Tuning:** Das System nutzt Modelle, macht sie aber nicht.

**Ausdrücklich nicht ausgeschlossen (Entscheidung beim Umfang der Ausbaustufen):**

- Eigene Erweiterungen (Plugins, MCP-Server) durch Mandanten
- Native Apps neben der Web-Oberfläche

## 6. Harte Randbedingungen

- **Technologie:** offen.
- **Hosting:** Self-Hosting auf einem gemieteten Server bei einem Hoster in der EU. Kein SaaS fremder Anbieter für den Workspace selbst.
- **Datenschutz/Compliance:**
  - DSGVO verbindlich, bereits ab Stufe 1. Mandanten sind Verantwortliche, der Betreiber ist Auftragsverarbeiter (Auftragsverarbeitungsvertrag pro Mandant). Für seinen eigenen Mandanten ist der Betreiber selbst Verantwortlicher. Hoster, Modellanbieter und – ab Stufe 2 – Zahlungsdienstleister sind Unterauftragsverarbeiter.
  - Löschung und Auskunft pro Mandant und pro Nutzer, auch ohne dass der Betreiber Inhalte lesen kann. Löschung muss sich auch auf Backups erstrecken.
  - Inhaltsgrenze gegenüber dem Betreiber: **technisch erzwungen für gespeicherte Daten**, ergänzt um **organisatorische Absicherung** während der Verarbeitung.
    - Technisch: Inhalte in Datenbank, Dateiablage und Backups sind mit Schlüsseln des Mandanten verschlüsselt; mit Server- oder Datenbankzugriff allein sind sie für den Betreiber nicht lesbar, für den Mandanten-Admin im Rahmen des Einsichtsmodus schon.
    - Organisatorisch: Während der Verarbeitung (Anfrage an das Modell, Durchsuchen von Wissen) liegen Inhalte zwangsläufig im Klartext auf dem Server und beim Modellanbieter. Dafür gelten Selbstverpflichtung, Protokollierung jedes administrativen Zugriffs und vertragliche Zusage im Auftragsverarbeitungsvertrag.
    - Schutz auch während der Verarbeitung (Confidential Computing) ist bewusst nicht Ziel.
  - Transparenz: Nutzer sehen jederzeit den aktuellen Einsichtsmodus ihres Mandanten.
- **Lizenzmodell:** proprietär. Nur der Betreiber betreibt das System.
- **Zeitrahmen:** kein harter Termin. Das Projekt läuft nachrangig neben anderen Vorhaben; die Dokumentation muss Wiedereinstiege nach längeren Pausen tragen.
- **Budget für externe Dienste:** Kosten zentraler API-Schlüssel werden über die Token-basierte Abrechnung auf die Mandanten umgelegt; in Stufe 1 trägt der Betreiber sie als erster Mandant selbst.

## 7. Weiche Präferenzen

- Bewährtes vor Neuem – etablierte Bausteine, kein Experimentieren.
- Wiederverwendung vor Eigenbau – bestehende Lösungen ernsthaft als Basis prüfen, nicht nur als Inspiration.
- Wenig Betriebsaufwand – Updates, Backups und Überwachung mit minimalem Eingreifen, da ein einzelner Betreiber.
- Einfachheit der Umsetzung – motiviert die Überlegung, Mandanten in getrennten Instanzen statt in einem gemeinsamen System zu betreiben. Betrifft die Art der Umsetzung, nicht den Funktionsumfang.

## 8. Inspirationen und Vorbilder

<!-- Stand der Angaben: Faktencheck vom 2026-10-09, Quellen in docs/haertung-vision.md. -->

- **TypingMind Teams (proprietär):** Vorbild für den Funktionsumfang – Chat-Workspace mit Agenten, Prompt-Bibliothek, Plugins und MCP, Wissensbasis, Branding, SSO, Limit-Gruppen (global, pro Modell, Agent, Plugin, Nutzer), Sichtbarkeitssteuerung, Analytics (Teil der Funktionen erst in höheren Tarifen). Admin-Rechte lassen sich innerhalb einer Instanz über eigene Rollen fein delegieren, eine Mandanten-Ebene darüber gibt es nicht. Limits nur über Nachrichten, Zeichen und Tokens, nicht über Geld. Self-Hosting nur per individuellem Angebot mit Lizenzprüfung. Das Reseller-Programm (Instanz je Kunde) ist seit 1. März 2026 ausgesetzt. Bewusst anders: zweite Verwaltungsebene, Betreiber ohne Inhaltseinsicht, Abrechnung in Geld, Mandanten-Admin ohne Technikwissen.
- **LibreChat (MIT):** Guthabensystem mit Umrechnung von Tokens in Geld, Startguthaben und automatischer Aufladung; Guthaben-Einstellungen global, nicht pro Gruppe oder Mandant. Seit v0.8.5 eigene Rollen und Delegation einzelner Admin-Rechte (plattformweit). Seit v0.8.7/v0.8.8 im Aufbau: Mandanten-Isolation – noch unreif und kaum dokumentiert, Abrechnung pro Mandant und Rolle „Mandanten-Admin" nicht belegt. Als mögliche Basis beobachten.
- **Open WebUI:** Verbreitung und Reife. Lizenz ab v0.6.6 (April 2025) mit Branding-Klausel: Ersetzen des Brandings nur bis 50 Endnutzer pro 30 Tage, mit schriftlicher Genehmigung oder mit Enterprise-Lizenz; White-Label-Dienste und Weiterverkauf ausdrücklich nur mit Enterprise-Lizenz. Code bis v0.6.5 bleibt BSD-3. Keine Mandanten-Ebene; Nutzerlimits und Abrechnung nur über Erweiterungen bzw. vorgeschaltete Gateways.
- **LobeChat / LobeHub:** Agenten als zentrale Arbeitseinheit, großer Skill-Marktplatz. LobeHub Community License (Apache 2.0 mit Zusatzbedingungen): unveränderter Betrieb auch kommerziell als Dienst erlaubt, veränderte Fassungen brauchen eine kommerzielle Lizenz; Contributors stimmen zu, dass die Bedingungen künftig strenger oder lockerer werden können. LDAP und SCIM nicht dokumentiert.
- **Gateway-Muster:** Governance als eigene Schicht vor den Modellen. Vorbild dafür, dass Chat und Governance getrennt sein können.
  - **LiteLLM (MIT, Ordner `enterprise/` kommerziell):** Frei: Schlüssel, Nutzer, Teams, Budgets, Kostenzuordnung, globales Abschalten des Prompt-Loggings. Enterprise: Organisationen und Org-Admins (also echte zwei Ebenen), Logging-Abschaltung pro Team, SSO/SCIM, Audit-Logs. Kostenberechnung über Preistabelle – gute Näherung, nicht rechnungsgenau.
  - **Bifrost (Apache 2.0):** Hierarchie Kunde → Team → Schlüssel mit Budgets laut Doku im freien Teil; RBAC, SSO und Audit nur Enterprise.
  - **Portkey Gateway (MIT):** Workspaces und Organisationen nur in der Control Plane (Cloud/Enterprise).
- **Wegen Lizenz für Mehrmandanten-Betrieb ausgeschlossen:** Dify (Mehrmandanten-Betrieb ohne schriftliche Erlaubnis verboten, Logo-Pflicht) und FastGPT (mandantenfähiger SaaS-Betrieb verboten, Logo-Pflicht).
- **Weitere geprüft, ohne Mandanten-Ebene im freien Teil:** Onyx (MIT, Enterprise-Teile separat), AnythingLLM (MIT), Flowise (Organisationen nur Enterprise), New API (AGPL-3.0, Geld-Kontingente, keine Mandanten), One API (MIT).
- **Zwischenergebnis:** Kein selbst hostbares Produkt vereint nachweislich Chat-Workspace, Mandanten-Admin, Abrechnung in Geld und passende Lizenz.

## 9. Bekannte Risiken und offene Punkte

- **Betreiberblindheit nur begrenzt machbar:** Chatnachrichten müssen im Klartext an Modelle gehen, Wissensdaten müssen gelesen und durchsucht werden – auf einem System, das der Betreiber kontrolliert. Entschieden: geschützt im Ruhezustand plus organisatorische Absicherung (Abschnitt 6). Bei zentralen API-Schlüsseln laufen Inhalte zudem über den Anbieter-Account des Betreibers: Anbieter speichern sie ohne Zero-Data-Retention 30 bis 55 Tage, und je nach Konto-Einstellung (z. B. API-Logging bei OpenAI, Logging in Google AI Studio) erscheinen sie in der Anbieter-Konsole. Diese Protokollierung muss abgeschaltet und Zero-Data-Retention wo möglich beantragt werden.
- **Löschung in Backups und beim Anbieter:** Löschpflichten erstrecken sich auf Backups und auf beim Modellanbieter gespeicherte Inhalte. Lösungsansatz (z. B. Vernichtung des Mandanten- bzw. Nutzerschlüssels, „Kryptoshredding") ist Architekturfrage für Modus 2.
- **Keine fertige Basis:** Kein selbst hostbares Produkt erfüllt Chat, Mandanten-Admin, Abrechnung in Geld und passende Lizenz zugleich (Abschnitt 8). „Wiederverwendung vor Eigenbau" heißt realistisch: Chat-Frontend plus Gateway, Mandanten-Ebene selbst bauen – oder LibreChat-Mandantenisolation abwarten. Größtes Umfangsrisiko.
- **Kommerzieller Dienst als Nebenprojekt:** Haftung, Gewerbe, Umsatzsteuer, AGB, Auftragsverarbeitungsverträge und Zahlungsabwicklung vertragen sich schlecht mit „ohne Termin, wenn Kapazität da ist". Entschärft durch Ausbaustufe 1 (Eigenbetrieb).
- **Nutzungsbedingungen der Modellanbieter:** Stand 2026-10-09 erlauben OpenAI, Anthropic, Google (Gemini API) und Mistral die Bereitstellung über eine eigene Anwendung mit Mehrwert an Endnutzer. Verboten sind u. a. Kauf, Verkauf oder Weitergabe von Schlüsseln bzw. Konten, das Training konkurrierender Modelle und bei Google ein Dienst, der „im Wesentlichen wie die API" funktioniert; in der EU dürfen bei Google nur bezahlte Dienste an Nutzer weitergegeben werden, Nutzer müssen mindestens 18 Jahre alt sein. Der Betreiber haftet gegenüber den Anbietern für alle Endnutzer. Vor Stufe 2 erneut prüfen.
- **Drittlandübermittlung:** Die meisten Modellanbieter sitzen in den USA; Grundlage (EU-US Data Privacy Framework, Standardvertragsklauseln) ist pro Anbieter zu klären. Offen für Modus 2.
- **Abrechnung bei eigenen API-Schlüsseln:** Was der Betreiber einem Mandanten mit eigenen Schlüsseln in Stufe 2 berechnet (z. B. Plattformgebühr), ist offen. Offen für Modus 2.
- **Abrechnungsgenauigkeit:** Toleranz 2 % pro Monat (Abschnitt 4). Erschwert durch USD-Abrechnung, Cache-Rabatte, Reasoning-Tokens, Staffelpreise, Werkzeugkosten und Embeddings; Gateway-Preistabellen sind nur Näherungen. Ab Stufe 2 rechtlich relevant.
- **Vorfinanzierung:** Anbieter berechnen Kosten, bevor Mandanten zahlen. Prepaid-Guthaben als möglicher Ausgleich.
- **Testperson für den Laientest:** noch nicht benannt; der Betreiber selbst ist zu nah dran.
- **Umfang:** Funktionsgleichstand mit TypingMind (als Richtung) plus vier eigene Unterscheidungsmerkmale, betrieben von einer Person. Begrenzt durch die Muss/Kann-Liste für Stufe 1 in Modus 2.
- **Lizenzlage bestehender Lösungen:** Branding-Klausel (Open WebUI), Community-Lizenz (LobeChat) und AGPL-Komponenten begrenzen die Wiederverwendung; bei Betrieb als Dienst für Mandanten verpflichtet AGPL zur Offenlegung eigener Änderungen.
- **Mandanten-Trennung lösungsneutral:** Ob Mandanten in einem gemeinsamen System oder in getrennten Instanzen laufen, ist offen und Architekturfrage für Modus 2. Getrennte Instanzen vereinfachen die Umsetzung, vervielfachen aber Updates, Backups und Überwachung für einen einzelnen Betreiber; die Betreiber-Ebene über alle Instanzen muss ohnehin gebaut werden. Ab Stufe 2 muss die Trennung vertrauensfest sein – ein Datenleck zwischen zahlenden Mandanten wäre der schwerste denkbare Fehler.
- **Arbeitsrechtliche Relevanz des Mitlesens:** Sind Mandanten Arbeitgeber, ist die Einsicht des Mandanten-Admins in Chats heikel (u. a. Mitbestimmung des Betriebsrats bei technischer Überwachung, § 87 Abs. 1 Nr. 6 BetrVG). Entschärft durch den wählbaren Einsichtsmodus (aus / bei Anlass / immer), der für Nutzer sichtbar ist.

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
- [x] Härtungsphase abgeschlossen (Blocker und Inkonsistenzen geprüft) – 2026-10-09, siehe `docs/haertung-vision.md`
- [x] Vorlagen-Set initialisiert (project-context.md, architecture.md, fahrplan.md, decisions.md, blockers.md)
- [x] ADR-001 angelegt: Anpassung des Vorlagen-Sets
- [x] Datum der Initialisierungs-Abschluss: 2026-10-09

**Nach abgeschlossener Initialisierung:** Diese Datei wird nicht mehr verändert.
Spätere Vision-Erweiterungen oder Pivots werden in einem ADR dokumentiert,
nicht in dieser Datei. Bei substantieller Vision-Änderung: neuer ADR mit Verweis hier.
