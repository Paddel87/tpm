# Entscheidungen (ADR-Log)

<!-- Lebendes Dokument, aber nur ergänzend: Entscheidungen werden angehängt, nie umgeschrieben.
     Eine überholte Entscheidung erhält Status „Ersetzt durch ADR-xxx"; die neue verweist zurück.
     Vision-Änderungen und Pivots werden hier dokumentiert, nicht in VISION.md.
     Format je ADR: Status, Datum, Kontext, Entscheidung, Konsequenzen, Verweise.
     Status: Vorgeschlagen · Angenommen · Angenommen (PoC-Vorbehalt) · Ersetzt durch ADR-xxx · Verworfen
     „PoC-Vorbehalt": gilt, solange die Prüfkriterien in architecture.md Abschnitt 8 bestehen;
     scheitert ein Kriterium, wird die Entscheidung per neuem ADR ersetzt.
     Herkunft: initialisiert am 2026-10-09. -->

## Übersicht

| ADR | Titel | Status | Datum |
|---|---|---|---|
| ADR-001 | Anpassung des Vorlagen-Sets | Angenommen | 2026-10-09 |
| ADR-002 | Bedrohungsmodell der Inhaltsgrenze | Angenommen | 2026-10-09 |
| ADR-003 | Verbrauchsausweis und Abrechnungsgenauigkeit | Angenommen | 2026-10-09 |
| ADR-004 | Einsichtsmodus des Mandanten-Admins | Angenommen | 2026-10-09 |
| ADR-005 | Hosting auf gemietetem EU-Server | Angenommen | 2026-10-09 |
| ADR-006 | LibreChat als Chat-Frontend | Angenommen (PoC-Vorbehalt) | 2026-10-09 |
| ADR-007 | Bifrost OSS als Gateway | Angenommen (PoC-Vorbehalt) | 2026-10-09 |
| ADR-008 | App-Instanz je Mandant | Angenommen (PoC-Vorbehalt) | 2026-10-09 |

---

## ADR-001: Anpassung des Vorlagen-Sets

- **Status:** Angenommen
- **Datum:** 2026-10-09

**Kontext:** Die Vision verweist auf ein Vorlagen-Set (`project-context.md`, `architecture.md`, `fahrplan.md`, `decisions.md`, `blockers.md`). Die Original-Vorlagen lagen bei der Initialisierung nicht vor.

**Entscheidung:** Das Vorlagen-Set wurde neu entworfen, im Stil der `VISION.md` (Kopfkommentar mit Zweck, Pflegeregeln und Herkunft). Festlegungen:

- Alle Projektdokumente liegen in `docs/`.
- `haertung-vision.md` ergänzt das Set als eingefrorenes Begründungsdokument der Härtung, mit Quellen des Faktencheck.
- ADRs werden fortlaufend in dieser einen Datei geführt, nicht als Einzeldateien.
- Randbedingungen in `project-context.md` erhalten IDs (`RB-xx`), offene Architekturfragen in `architecture.md` IDs (`A-x`), Blocker IDs (`B-xx`), damit Dokumente aufeinander verweisen können.
- `project-context.md` beginnt mit einem Wiedereinstiegs-Abschnitt, weil das Projekt längere Pausen tragen muss.
- Dokumentensprache ist Deutsch.

**Konsequenzen:** Sollten die Original-Vorlagen später auftauchen, werden Abweichungen per neuem ADR bewertet. `VISION.md` und `haertung-vision.md` werden ab jetzt nicht mehr verändert.

---

## ADR-002: Bedrohungsmodell der Inhaltsgrenze

- **Status:** Angenommen
- **Datum:** 2026-10-09

**Kontext:** Die Vision verlangte ursprünglich, dass der Betreiber Inhalte auch mit Server- und Datenbankzugriff technisch nicht lesen kann. Die Härtung zeigte: Verarbeitung durch Modelle und Durchsuchen von Wissen brauchen Klartext auf dem Server; Confidential Computing ist bei physischem Zugriff angreifbar (TEE.fail, Okt. 2025) und widerspricht wenig Betriebsaufwand; externe Modellanbieter speichern Inhalte 30–55 Tage.

**Entscheidung:** Inhalte sind im Ruhezustand technisch geschützt (Verschlüsselung mit Mandantenschlüsseln in Datenbank, Dateiablage und Backups). Während der Verarbeitung gilt organisatorische Absicherung: Selbstverpflichtung, Protokollierung jedes administrativen Zugriffs, Zusage im Auftragsverarbeitungsvertrag. Schutz während der Verarbeitung (Confidential Computing) ist ausdrücklich nicht Ziel.

**Konsequenzen:** Gegenüber Mandanten wird keine absolute Zusage gemacht. Anbieter-Logging muss abgeschaltet, Zero-Data-Retention beantragt werden. Schlüsselverwaltung (A-3) und Zugriffsprotokoll (A-7) sind Architekturfragen.

**Verweise:** RB-01 bis RB-03, `haertung-vision.md` (A1).

---

## ADR-003: Verbrauchsausweis und Abrechnungsgenauigkeit

- **Status:** Angenommen
- **Datum:** 2026-10-09

**Kontext:** Die Vision ließ den Betreiber Preise festlegen und verlangte zugleich, dass der ausgewiesene Verbrauch den Anbieterkosten entspricht. Exakte Genauigkeit pro Modell ist wegen USD-Abrechnung, Cache-Rabatten, Reasoning-Tokens, Staffelpreisen und Werkzeugkosten nicht realistisch messbar.

**Entscheidung:** Anbieterkosten und Betreiberpreis (Kosten plus Aufschlag) werden getrennt ausgewiesen. Die ausgewiesenen Anbieterkosten dürfen pro Monat höchstens 2 % von der Anbieterrechnung abweichen; Prüfung durch monatlichen Abgleich, Umrechnung mit festem Wechselkurs-Stichtag.

**Konsequenzen:** Ein Abgleichprozess gegen Anbieterrechnungen ist Pflicht. Gateway-Preistabellen allein genügen nicht.

**Verweise:** RB-10 bis RB-12, `haertung-vision.md` (B1, B2).

---

## ADR-004: Einsichtsmodus des Mandanten-Admins

- **Status:** Angenommen
- **Datum:** 2026-10-09

**Kontext:** Die Vision sah vor, dass der Mandanten-Admin alle Inhalte seines Mandanten sieht. Bei Mandanten, die Arbeitgeber sind, ist das arbeitsrechtlich heikel (u. a. § 87 Abs. 1 Nr. 6 BetrVG).

**Entscheidung:** Der Mandanten-Admin wählt pro Mandant einen Einsichtsmodus: aus / nur bei Anlass (begründet und protokolliert) / immer. Der aktuelle Modus ist für alle Nutzer sichtbar.

**Konsequenzen:** Rollenmodell und Laientest umfassen die Wahl des Einsichtsmodus. Schlüsselverwaltung (A-3) muss den Modus technisch abbilden.

**Verweise:** RB-06, `haertung-vision.md` (C4).

---

## ADR-005: Hosting auf gemietetem EU-Server

- **Status:** Angenommen
- **Datum:** 2026-10-09

**Kontext:** „Self-Hosting" war nicht konkretisiert; die Wahl beeinflusst Betriebsaufwand, Unterauftragsverarbeiter und das Bedrohungsmodell.

**Entscheidung:** Betrieb auf einem gemieteten Server bei einem Hoster in der EU. Kein fremder SaaS für den Workspace selbst.

**Konsequenzen:** Der Hoster wird Unterauftragsverarbeiter (AVV nötig). Die Wahl des konkreten Hosters erfolgt in Phase 2.

**Verweise:** RB-20, `haertung-vision.md` (C5).

---

## ADR-006: LibreChat als Chat-Frontend

- **Status:** Angenommen (PoC-Vorbehalt)
- **Datum:** 2026-10-09

**Kontext:** Für A-1 wurden acht Chat-Frontends geprüft (`recherche-basis.md`). Gesucht war eine Basis, die unter eigenem Namen verändert als Dienst betrieben werden darf und Mandanten, delegierte Admins und vollen Funktionsumfang mitbringt.

**Entscheidung:** LibreChat (MIT) wird Basis des Chat-Workspace. Das AGPL-lizenzierte Admin-Panel wird nicht verändert ausgeliefert; die laientaugliche Admin-Oberfläche wird selbst gebaut.

**Konsequenzen:**
- Versionen eng pinnen, Upstream regelmäßig nachziehen; Pre-release-Takt und Kurs des Eigentümers ClickHouse beobachten (B-09).
- Selbst zu bauen: Mandanten-Lebenszyklus, Mandanten-Admin-Oberfläche, Branding pro Mandant, Selbstbedienung für eigene API-Schlüssel, Verschlüsselung im Ruhezustand.
- Meilisearch (Volltextsuche) und die Vektor-Datenbank speichern Klartext; ihr Umgang mit RB-01 ist Teil von A-3.
- Plan B bei Scheitern: BionicGPT oder kommerzielle LobeHub-Lizenz.

**Verweise:** A-1, `recherche-basis.md` Abschnitt 1.

---

## ADR-007: Bifrost OSS als Gateway

- **Status:** Angenommen (PoC-Vorbehalt)
- **Datum:** 2026-10-09

**Kontext:** Für Budgets und Kostenerfassung wurden neun Gateways geprüft. Kein Gateway rechnet in Euro, delegierte Admins gibt es nur in Enterprise-Versionen.

**Entscheidung:** Bifrost OSS (Apache-2.0) als einzelne Instanz vor allen Modellanbietern. Abbildung: Customer = Mandant, Team = Gruppe, Virtual Key je Nutzer. Inhaltslogging wird abgeschaltet (`disable_content_logging: true`).

**Konsequenzen:**
- Alarm auf Buchungen mit 0,00 USD (fehlender Preis) ist Pflicht.
- Für betreiberbezahlte Schlüssel wird je Mandant ein eigenes Anbieter-Projekt bzw. Workspace angelegt; ein täglicher Abgleich gegen die Kosten-APIs der Anbieter und die Euro-Umrechnung werden selbst gebaut (RB-11, RB-12).
- Keine Hochverfügbarkeit im OSS; für Stufe 1 akzeptiert.
- Zweite Wahl bei Scheitern: LiteLLM OSS (Mandant = Team).

**Verweise:** A-1, A-5, `recherche-basis.md` Abschnitte 2 und 3.

---

## ADR-008: App-Instanz je Mandant

- **Status:** Angenommen (PoC-Vorbehalt)
- **Datum:** 2026-10-09

**Kontext:** A-2 – gemeinsames System oder getrennte Instanzen. LibreChats Mandanten-Isolation ist Beta (Bug #15975 erst im September behoben); ein Datenleck zwischen Mandanten wäre der schwerste Fehler. Gleichzeitig muss eine Person den Betrieb tragen.

**Entscheidung:** Jeder Mandant erhält eine eigene LibreChat-Instanz mit eigener Datenbank und eigenem Datenbank-Zugang. Gemeinsam genutzt werden der Datenbank-Server, das Gateway und der Reverse-Proxy (Subdomain je Mandant).

**Konsequenzen:**
- Trennung über Prozess- und Datenbankgrenzen, unabhängig von LibreChats Beta-Isolation.
- Verschlüsselung und Löschung pro Mandant lassen sich auf Datenbankebene ansetzen (A-3, A-4).
- Branding pro Mandant über die Konfiguration der eigenen Instanz.
- Updates, Backups und Überwachung laufen per Skript über alle Instanzen (RB-21); Ressourcenbedarf wächst je Mandant.
- Die Betreiber-Ebene (A-6) muss Instanzen anlegen, konfigurieren und Metadaten einsammeln.

**Verweise:** A-2, B-02, `recherche-basis.md` Abschnitt 4.
