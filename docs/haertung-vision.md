# Härtung der Vision

<!-- Ergebnis der Härtungsphase vom 2026-10-09 für docs/VISION.md.
     Hält Befund, Faktencheck, Entscheidungen und an Modus 2 übergebene Punkte fest.
     Die Entscheidungen sind in VISION.md eingearbeitet; dieses Dokument begründet sie.
     Kennzeichnung im Faktencheck: F = belegter Fakt mit Quelle, E = Einschätzung. -->

Stand: 2026-10-09

## 1. Ergebnis in Kürze

- **1 Blocker** (Inhaltsgrenze gegenüber dem Betreiber) – entschieden.
- **5 Widersprüche** – 4 entschieden, 1 an Modus 2 übergeben.
- **8 Lücken** – 6 entschieden, 2 an Modus 2 übergeben.
- **7 Faktenkorrekturen** zu Vorbildern und Anbieterbedingungen – in Abschnitt 8 und 9 der Vision eingearbeitet.
- **2 „(abgeleitet)"-Aussagen** – beide bestätigt bzw. präzisiert.

## 2. Befund und Entscheidungen

### Blocker

| Nr. | Befund | Entscheidung |
|---|---|---|
| A1 | „Betreiber kann Inhalte technisch nicht lesen, auch mit Server- und DB-Zugriff" ist mit Self-Hosting durch einen Einzelbetreiber und externen Modellanbietern nicht erfüllbar: Verarbeitung und Wissenssuche brauchen Klartext auf dem Server; Confidential Computing ist bei physischem Zugriff angreifbar (TEE.fail, Okt. 2025); Anbieter speichern Inhalte 30–55 Tage und zeigen sie je nach Einstellung in der Konsole. | **Geschützt im Ruhezustand plus organisatorisch.** Gespeicherte Inhalte mit Mandantenschlüsseln verschlüsselt; während der Verarbeitung Selbstverpflichtung, Zugriffsprotokoll, Zusage im AVV. Confidential Computing bewusst nicht Ziel. |

### Widersprüche

| Nr. | Befund | Entscheidung |
|---|---|---|
| B1 | Betreiber legt „Preise" fest, Erfolgskriterium verlangt Ausweis der „tatsächlichen Anbieterkosten". | **Beides getrennt ausweisen:** Anbieterkosten und Betreiberpreis (Kosten plus Aufschlag). |
| B2 | Genauigkeit „pro Modell" nicht messbar (USD, Cache, Reasoning, Staffelpreise, Werkzeuge, Embeddings). | **Höchstens 2 % Abweichung pro Monat** gegen Anbieterrechnung, monatlicher Abgleich, fester Wechselkurs-Stichtag. |
| B3 | „Einfachheit" (getrennte Instanzen) gegen „wenig Betriebsaufwand" (N Instanzen = N-facher Betrieb). | **An Modus 2 übergeben**; Spannung im Risiko „Mandanten-Trennung" der Vision vermerkt. |
| B4 | Löschpflicht pro Nutzer/Mandant gegen Backups und beim Anbieter gespeicherte Inhalte. | Löschung erstreckt sich auf Backups (Randbedingung ergänzt); **Lösungsansatz (z. B. Kryptoshredding) an Modus 2.** |
| B5 | „Konzeptphase abgeschlossen" abgehakt, obwohl Kernfragen offen waren. | Durch diese Härtung aufgelöst. |

### Lücken

| Nr. | Befund | Entscheidung |
|---|---|---|
| C1 | Funktionsumfang von Stufe 1 nicht festgelegt. | Stufe 1 = Kern-Chat plus die vier Unterscheidungsmerkmale; TypingMind-Gleichstand ist Richtung, nicht Pflicht. **Muss/Kann-Liste in Modus 2** (`fahrplan.md`). |
| C2 | Laientest: wer richtet was ein, was heißt „vollständig"? | Betreiber legt Mandant an; Testperson schafft ohne Hilfe: Nutzer einladen und Gruppen, Rechte und Kontingente, eigene API-Schlüssel, Einsichtsmodus, Name und Logo. |
| C3 | Teilen von Inhalten innerhalb eines Mandanten nicht geregelt. | **Ja, gruppenweit:** Projekte, Agenten, Wissensbasen; nie über Mandantengrenzen. |
| C4 | Einsicht des Mandanten-Admins in Chats: arbeitsrechtlich heikel (§ 87 Abs. 1 Nr. 6 BetrVG). | **Einsichtsmodus pro Mandant:** aus / nur bei Anlass (begründet, protokolliert) / immer; für Nutzer sichtbar. |
| C5 | „Self-Hosting" nicht konkret. | **Gemieteter Server bei EU-Hoster;** Hoster wird Unterauftragsverarbeiter. |
| C6 | Drittlandübermittlung an US-Modellanbieter nicht adressiert. | **An Modus 2 übergeben;** als Risiko in der Vision vermerkt. |
| C7 | Abrechnung bei eigenen API-Schlüsseln in Stufe 2 offen. | **An Modus 2 übergeben;** als Risiko in der Vision vermerkt. |
| C8 | Gilt die DSGVO schon in Stufe 1? | Eigene Gruppen sind **andere Personen** (Verein, Familie, Bekannte) → DSGVO ab Stufe 1. |

### „(abgeleitet)"-Aussagen

| Nr. | Aussage | Entscheidung |
|---|---|---|
| E1 | Betreiber pflegt Voreinstellungen als Vorlage für neue Mandanten. | **Bestätigt, erweitert:** Mandanten-Admin kann zusätzlich eigene Vorlagen für seine Gruppen pflegen. |
| E2 | Euro-Verbrauch entspricht den Anbieterkosten. | **Präzisiert** über B1 und B2. |

## 3. Faktencheck (Stand 2026-10-09)

Durchgeführt per Websuche gegen Primärquellen. Lizenzaussagen sind inhaltlich geprüft, ersetzen aber keine Rechtsberatung.

### TypingMind Teams

- F: Limits nur über Nachrichten, Zeichen pro Nachricht, Zeichen pro Zeitraum, Tokens pro Zeitraum; Ebenen global, Modell, Agent, Plugin, Nutzer; keine Geld-Limits. – https://docs.typingmind.com/typingmind-team/user-management/usage-limits
- F: Selbst definierbare Admin-Rollen (Modelle, Agenten, Reporting, Billing, Nutzerverwaltung u. a.), nur innerhalb einer Instanz. – https://docs.typingmind.com/typingmind-team/user-management/roles-and-permissions
- F: Reseller-Programm (Seat Resell, Instance Resell) seit 1. März 2026 „until further notice" ausgesetzt. – https://docs.typingmind.com/typingmind-team/reseller-program
- F: MCP ab Starter-Tarif; Analytics, Chat-Logs, Audit-Logs und RBAC erst im Professional-Tarif; Projekte nur für die Personal-Version ausdrücklich dokumentiert. – https://custom.typingmind.com/pricing, https://custom.typingmind.com/features/model-context-protocol
- F: Self-Hosting nur per individuellem Angebot, privates Repo, proprietäre Lizenz, Lizenz- und Nutzerzahlprüfung über das Netz. – https://docs.typingmind.com/typingmind-team/getting-started/self-host-typingmind-team

### LibreChat

- F: Lizenz MIT. – https://github.com/danny-avila/LibreChat/blob/main/LICENSE
- F: Guthaben (`startBalance`, Auto-Refill), 1 Mio. Credits = 1 USD, Preise pro Modell über `tokenConfig`; Einstellungen global, nicht pro Gruppe/Mandant. – https://www.librechat.ai/docs/configuration/librechat_yaml/object_structure/balance
- F: Seit v0.8.5 eigene Rollen, Gruppen und „System Grants" (plattformweit); Admin-Panel im Status „Preview". – https://www.librechat.ai/docs/features/access_control
- F: Seit v0.8.7/v0.8.8 (1. Okt. 2026, Pre-release) Mandanten-Isolation (`TENANT_ISOLATION_STRICT`, `X-Tenant-Id`); offene Baustellen (PR #16850, Issue #15975). – https://github.com/danny-avila/LibreChat/releases, https://github.com/danny-avila/LibreChat/pull/15662
- E: Mandantenfähigkeit im Aufbau, noch nicht produktionsreif; Abrechnung pro Mandant nicht belegt.

### Open WebUI

- F: Branding-Klausel seit v0.6.6 (19. April 2025). Ausnahmen: höchstens 50 Endnutzer pro rollierenden 30 Tagen, schriftliche Genehmigung, Enterprise-Lizenz. Code bis v0.6.5 bleibt BSD-3. White-Label-SaaS und Weiterverkauf nur mit Enterprise-Lizenz. – https://github.com/open-webui/open-webui/blob/main/LICENSE, https://docs.openwebui.com/license
- F: Keine nativen Token-, Nachrichten- oder Geld-Limits; keine Mandanten-Ebene. – https://github.com/open-webui/open-webui/issues/23323, https://github.com/open-webui/open-webui/discussions/15519
- E: Bei Mehrmandanten-Betrieb zählt vermutlich die Summe aller Nutzer der Installation.

### LobeChat / LobeHub

- F: LobeHub Community License (Apache 2.0 mit Zusatzbedingungen); unveränderter Betrieb auch kommerziell erlaubt, abgeleitete Werke brauchen kommerzielle Lizenz; Contributors stimmen künftigen strengeren oder lockereren Bedingungen zu. – https://github.com/lobehub/lobehub/blob/main/LICENSE
- F: Authentifizierung über OAuth/OIDC; LDAP und SCIM nicht dokumentiert. – https://lobehub.com/docs/self-hosting/auth

### LiteLLM

- F: MIT außer `enterprise/`. – https://github.com/BerriAI/litellm/blob/main/LICENSE
- F: Frei: Schlüssel, Nutzer, Teams, Budgets, Kostenzuordnung, globales `turn_off_message_logging`. Enterprise: Organisationen, Org- und Team-Admins, Logging-Abschaltung pro Team, SSO/SCIM, Audit-Logs. – https://www.litellm.ai/pricing, https://docs.litellm.ai/docs/proxy/access_control
- F: Kosten aus Preistabelle mit eigenen Feldern für Cache, Reasoning, Staffelpreise, Batch. – https://docs.litellm.ai/docs/proxy/cost_tracking
- E: Gute Näherung, nicht rechnungsgenau; Abgleich gegen Anbieterrechnung nötig.

### Weitere Kandidaten

| Produkt | Lizenz | Mandanten-Ebene | Abrechnung in Geld |
|---|---|---|---|
| Dify | Apache 2.0 + Verbot von Mehrmandanten-Betrieb ohne Erlaubnis, Logo-Pflicht | lizenzrechtlich gesperrt | nicht nativ (E) |
| FastGPT | Apache 2.0 + Verbot mandantenfähiger SaaS, Logo-Pflicht | lizenzrechtlich gesperrt | Kontingente (E, ungeprüft) |
| Onyx | MIT + Enterprise-Teile | nur Cloud/Enterprise (E) | Token-Budgets, Limits teils Enterprise |
| AnythingLLM | MIT (E) | nein | nein |
| Bifrost | Apache 2.0 | Kunde → Team → Schlüssel im freien Teil (laut Doku) | ja |
| Portkey Gateway | MIT | nur Control Plane (Cloud/Enterprise) | Budgets auf Schlüsseln |
| New API | AGPL-3.0 | nein (E) | ja (E) |
| One API | MIT (E) | nein (E) | ja (E) |
| Flowise | Apache 2.0 + Enterprise-Ordner (E) | nur Enterprise (E) | nein |

Quellen: https://github.com/langgenius/dify/blob/main/LICENSE, https://github.com/labring/FastGPT/blob/main/LICENSE, https://github.com/onyx-dot-app/onyx/blob/main/LICENSE, https://docs.anythingllm.com/features/security-and-access, https://docs.getbifrost.ai/features/governance/budget-and-limits, https://github.com/Portkey-AI/gateway/blob/main/LICENSE, https://github.com/QuantumNous/new-api/blob/main/LICENSE

Nicht im Detail geprüft: kommerzielle Angebote wie Langdock, Cohere North, Le Chat Enterprise; Jan Server.

### Nutzungsbedingungen der Modellanbieter

| Anbieter | Bereitstellung an Endnutzer | Verboten (Auszug) | Speicherung / Sichtbarkeit |
|---|---|---|---|
| OpenAI (Services Agreement, 1.1.2026) | erlaubt in eigenen Anwendungen (Ziff. 2.2) | Account weiterverkaufen/vermieten, API-Schlüssel kaufen/verkaufen/übertragen, Konkurrenzmodelle entwickeln | Abuse-Logs bis 30 Tage; ZDR nur nach Genehmigung; bei aktivem API-Logging Inhalte im Dashboard sichtbar (Quelle: Community-Foren) |
| Anthropic (Commercial Terms, 17.6.2025) | ausdrücklich erlaubt | konkurrierende Produkte/Modelle; Weiterverkauf nur mit Genehmigung | Löschung binnen 30 Tagen; bei Policy-Verstößen bis 2 Jahre; ZDR über Sales |
| Google Gemini API (Stand 28.4.2026) | erlaubt; in EU/EWR/CH/UK nur Paid Services; Nutzer ab 18 | Dienst, der „im Wesentlichen wie die API" funktioniert; Sublizenzierung; Konkurrenzmodelle | Abuse-Speicherung (55 Tage); optionales AI-Studio-Logging 7–55 Tage, für das Projekt sichtbar |
| Mistral (Commercial Terms, 25.9.2026) | „Customer Offering" vorgesehen | Kauf/Verkauf/Übertragung von Schlüsseln oder Konten | 30 Tage rollierend; ZDR auf Antrag, nur zustandslose Aufrufe |

Quellen: https://cdn.openai.com/osa/openai-services-agreement.pdf, https://developers.openai.com/api/docs/guides/your-data, https://www.anthropic.com/legal/commercial-terms, https://platform.claude.com/docs/en/manage-claude/api-and-data-retention, https://ai.google.dev/gemini-api/terms, https://ai.google.dev/gemini-api/docs/logs-policy, https://developers.google.com/terms, https://legal.mistral.ai/terms/commercial-terms-of-service, https://docs.mistral.ai/admin/monitor-comply/zero-data-retention

Unbestätigt (Drittquellen, vor Stufe 2 prüfen): Anthropic soll die Aufbewahrung auf 7 Tage verkürzt haben; Mistral soll am 28.7.2026 die Zusage „kein Training auf Daten bezahlter API-Nutzer" aus der Datenschutzerklärung entfernt haben.

### Machbarkeit „Betreiber kann nicht lesen"

- F: Confidential Computing für CPU (AMD SEV-SNP, Intel TDX) und GPU (NVIDIA H100/H200/B200) mit Remote Attestation verfügbar; Overhead unter 7 % Durchsatz bis +21,8 % Zeit bis zum ersten Token. – https://docs.trustauthority.intel.com/main/articles/concept-gpu-attestation.html
- F: Produkte für private Chat-Verarbeitung: Tinfoil, Privatemode (Edgeless Systems), Confer, Apple Private Cloud Compute, Google Private AI Compute. Kein mandantenfähiger Team-Workspace bekannt (E).
- F: TEE.fail (Okt. 2025): DDR5-Interposer unter 1.000 $ extrahiert Schlüssel aus TDX und SEV-SNP und bricht die NVIDIA-GPU-Attestation; physischer Zugriff liegt außerhalb des Bedrohungsmodells von Intel und AMD. – https://thehackernews.com/2025/10/new-teefail-side-channel-attack.html
- E: Für einen Einzelbetreiber mit Self-Hosting nicht vollständig erreichbar; externe Modell-APIs heben den Schutz zusätzlich auf. Daher Entscheidung A1.

## 4. An Modus 2 übergeben

- B3: gemeinsames System oder getrennte Instanzen pro Mandant – unter Berücksichtigung des Betriebsaufwands.
- B4: Löschkonzept für Backups und Anbieterdaten (z. B. Kryptoshredding, Zero-Data-Retention).
- C1: Muss/Kann-Liste für Stufe 1.
- C6: Rechtsgrundlage der Drittlandübermittlung pro Modellanbieter.
- C7: Abrechnungsmodell für Mandanten mit eigenen API-Schlüsseln.
- Basiswahl: Chat-Frontend plus Gateway (Bifrost frei, LiteLLM Enterprise) mit selbst gebauter Mandanten-Ebene, oder LibreChat-Mandantenisolation abwarten.
