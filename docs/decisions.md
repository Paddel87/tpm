# Entscheidungen (ADR-Log)

<!-- Lebendes Dokument, aber nur ergänzend: Entscheidungen werden angehängt, nie umgeschrieben.
     Eine überholte Entscheidung erhält Status „Ersetzt durch ADR-xxx"; die neue verweist zurück.
     Vision-Änderungen und Pivots werden hier dokumentiert, nicht in VISION.md.
     Format je ADR: Status, Datum, Kontext, Entscheidung, Konsequenzen, Verweise.
     Status: Vorgeschlagen · Angenommen · Ersetzt durch ADR-xxx · Verworfen
     Herkunft: initialisiert am 2026-10-09. -->

## Übersicht

| ADR | Titel | Status | Datum |
|---|---|---|---|
| ADR-001 | Anpassung des Vorlagen-Sets | Angenommen | 2026-10-09 |
| ADR-002 | Bedrohungsmodell der Inhaltsgrenze | Angenommen | 2026-10-09 |
| ADR-003 | Verbrauchsausweis und Abrechnungsgenauigkeit | Angenommen | 2026-10-09 |
| ADR-004 | Einsichtsmodus des Mandanten-Admins | Angenommen | 2026-10-09 |
| ADR-005 | Hosting auf gemietetem EU-Server | Angenommen | 2026-10-09 |

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
