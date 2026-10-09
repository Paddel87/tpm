# Recherche: Basiswahl (A-1) und Mandanten-Trennung (A-2)

<!-- Eingefrorenes Begründungsdokument für ADR-006 bis ADR-008 (Modus 2, 2026-10-09).
     Hält die Kandidatenprüfung mit Quellen fest. Wird nicht fortgeschrieben; neue Erkenntnisse
     (z. B. aus dem PoC) landen in decisions.md, architecture.md und blockers.md.
     Kennzeichnung: F = belegter Fakt mit Quelle, E = Einschätzung. -->

Stand: 2026-10-09

## 1. Chat-Frontend

### LibreChat – gewählt (ADR-006)

- **Lizenz:** F: MIT (https://github.com/danny-avila/LibreChat). Das neue Admin-Panel ist ein separates Repo unter **AGPL-3.0** (https://github.com/ClickHouse/librechat-admin-panel). E: Hauptprodukt darf verändert unter eigenem Namen betrieben werden; das Admin-Panel nur unverändert oder gar nicht.
- **Eigentümer und Takt:** F: Von ClickHouse am 4.11.2025 übernommen (https://clickhouse.com/blog/clickhouse-acquires-librechat). v0.8.7 (24.6.2026), v0.8.8 (1.10.2026), beide als Pre-release markiert.
- **Mandantenfähigkeit:**
  - F: Mongoose-Plugin `applyTenantIsolation` setzt `tenantId` aus dem Request-Kontext in jede Query und jeden Insert; angewendet auf rund 40 Modelle, u. a. User, Group, Role, Agent, Prompt, McpServer, File, Convo, Message, Memory, ChatProject, Balance, Transaction, Config.
  - F: `TENANT_ISOLATION_STRICT=true` lehnt Anfragen ohne Mandantenkontext ab. `X-Tenant-Id` wird nur vor dem Login und nur mit `TRUST_TENANT_HEADER=true` gelesen; die Zuordnung (z. B. Subdomain → Mandant) ist Aufgabe des Reverse-Proxys. Nach dem Login kommt `tenantId` aus dem Nutzerdokument.
  - F: Admin-Rechte (`manage:users`, `manage:groups`, `manage:configs:<section>`, `read:usage` u. a.) tragen eine `tenantId` und lassen sich so auf einen Mandanten beschränken.
  - F: Kein Mandanten-Objekt, keine Mandanten-Anlage per UI oder API; der erste Nutzer eines Mandanten wird nicht automatisch Admin. Branding (App-Titel) nur global.
  - F: Isolations-Bug #15975 (fehlende Owner-Rechte im Mandantenkontext) erst am 17.9.2026 behoben. PR #16850 (Nutzer im Mandanten per CLI anlegen) offen.
  - F: Interner Plan im Repo („FerretDB Multi-Tenancy Plan", Active Investigation): eine Datenbank pro Organisation auf FerretDB/Postgres.
  - E: Datenschicht ernsthaft und getestet, Produkt- und Admin-Ebene Beta.
- **Abrechnung:** F: Guthaben pro Nutzer in Credits (1 Mio. = 1 USD), `currency` wirkt nur auf die Anzeige.
- **Datenhaltung:** F: MongoDB 8, Meilisearch (Volltextsuche), Postgres/pgvector mit `rag_api`. Automatische Feldverschlüsselung (CSFLE/Queryable Encryption) nur in MongoDB Enterprise/Atlas; in der Community Edition nur explizite Verschlüsselung.
- **Gateway-Anbindung:** F: OpenAI-kompatible Custom Endpoints mit Header-Platzhaltern, u. a. `{{LIBRECHAT_USER_ID}}`, `{{LIBRECHAT_USER_TENANT_ID}}`.
- **Funktionen:** F: Agenten, Prompt-Bibliothek mit Freigaben, MCP, RAG/Dateien, Projekte, SSO (OIDC, SAML, LDAP), Memory, Code Interpreter. E: auf oder über TypingMind-Teams-Niveau.

### Verworfene Kandidaten

| Kandidat | Grund | Quelle |
|---|---|---|
| Open WebUI | Branding-Klausel: eigener Name ab mehr als 50 Nutzern nur mit Enterprise-Lizenz; keine Mandanten, keine delegierten Admins, keine Abrechnung | https://github.com/open-webui/open-webui/blob/main/LICENSE |
| LobeHub | Veränderte Fassung braucht kommerzielle Lizenz; Workspace-Modell fachlich passend | https://github.com/lobehub/lobehub/blob/main/LICENSE |
| Dify | Lizenz verbietet Mehrmandanten-Betrieb ohne Genehmigung | https://github.com/langgenius/dify/blob/main/LICENSE |
| Onyx CE | Mandanten-Provisionierung, Admin und Limits nur im Enterprise-Teil; hoher Betriebsaufwand | https://github.com/onyx-dot-app/onyx/blob/main/LICENSE |
| AnythingLLM | MIT, aber keine Mandanten, nur Rollen admin/manager/default | https://github.com/Mintplex-Labs/anything-llm |
| HF chat-ui | Apache-2.0, aber kein Admin, keine Mandanten, RAG entfernt | https://github.com/huggingface/chat-ui |
| big-AGI | MIT, Daten im Browser, keine Server-Nutzerverwaltung | https://github.com/enricoros/big-AGI |
| BionicGPT | Apache-2.0, Teams mit Postgres; Funktionsumfang und Community deutlich kleiner – Plan B | https://github.com/bionic-gpt/bionic-gpt |

## 2. Gateway

### Bifrost OSS – gewählt (ADR-007)

- **Lizenz:** F: Apache-2.0. Enterprise (Preis auf Anfrage): RBAC, SSO, Audit-Logs, Cluster, Vault u. a. (https://www.getmaxim.ai/bifrost/pricing).
- **Hierarchie:** F: Customer → Team → Virtual Key, Budgets auf allen drei Ebenen mit Reset-Perioden; nicht als Enterprise markiert (https://docs.getbifrost.ai/features/governance/virtual-keys, https://docs.getbifrost.ai/features/governance/budget-and-limits). Einschränkung: „Customer scoping" bei Teams mit mehreren Customers ist Enterprise. Delegierte Admins nur Enterprise.
- **Kosten:** F: Preisblatt des Herstellers, per URL überschreibbar, täglicher Sync; Cache-Preise und Staffeln unterstützt; Reasoning-Tokens nicht dokumentiert; **fehlt ein Preis, wird 0,00 gebucht** (nur Debug-Log) (https://docs.getbifrost.ai/architecture/framework/model-catalog). Nur USD.
- **Eigene Schlüssel:** F: Virtual Key kann auf bestimmte Anbieter-Schlüssel (`key_ids`) und erlaubte Modelle festgelegt werden, standardmäßig alles verboten.
- **Logging:** F: Inhaltslogging ist **standardmäßig an** (Prompts und Antworten in SQLite/Postgres); `disable_content_logging: true` schaltet global ab (https://docs.getbifrost.ai/features/observability/default).
- **Betrieb:** F: Go, ein Binary oder Docker, SQLite oder Postgres; mehrere OSS-Knoten mit Postgres nicht unterstützt (Budgets im Arbeitsspeicher).

### LiteLLM – zweite Wahl

- F: MIT außer `enterprise/`. Organisationen, Org- und Team-Admins, eigene Schlüssel pro Team, Logging pro Team und Spend-Reports sind Enterprise; Preis nicht veröffentlicht (https://docs.litellm.ai/docs/enterprise, https://docs.litellm.ai/docs/proxy/multi_tenant_architecture).
- F: Inhalte standardmäßig nicht in den Spend-Logs. Bekannte Kostenfehler bei Cache-Preisen (Issues #27191, #15056).
- F: Lieferketten-Vorfall 24.3.2026 (PyPI 1.82.7/1.82.8 mit Credential-Stealer; Docker-Image laut Maintainer nicht betroffen).

### Verworfene Kandidaten

| Kandidat | Grund |
|---|---|
| Portkey Gateway OSS | zustandslos, keine Budgets/Mandanten im OSS; Übernahme durch Palo Alto Networks |
| Kong AI Gateway | Kostenlimits nur Enterprise, ab 3.10 Lizenz nötig (Forenaussage) |
| Envoy AI Gateway / Agent Router | Kubernetes-Baustein ohne Abrechnung |
| agentgateway | Budgets nur in Tokens, kein Spend-Ledger |
| Helicone | seit März 2026 im Wartungsmodus; speichert Inhalte |
| TensorZero | LLMOps-Fokus, keine Mandanten oder Budgets in Geld |
| New API | AGPL-3.0, Reselling-Modell ohne echte Mandanten |
| One API | stagniert |
| Otari (Mozilla.ai) | sehr jung – beobachten |

## 3. Abgleich mit Anbieterrechnungen (für RB-11)

| Anbieter | Kosten-API | Zuordnung pro Mandant |
|---|---|---|
| OpenAI | `/v1/organization/costs` täglich, USD, gruppierbar nach Projekt; Usage-API bis Minute, mit `api_key_id` | ein Projekt pro Mandant (per Admin-API anlegbar, nur archivierbar) |
| Anthropic | Cost-Report täglich in USD-Cent nach Workspace; Usage-Report bis Minute nach Key/Workspace | ein Workspace pro Mandant (per Admin-API anlegbar) |
| Google | Cloud Billing Export nach BigQuery; Vertex-Request-Labels (nur PayGo, max. 1.000 Werte je Label-Key) | ein GCP-Projekt pro Mandant oder Label `tenant` |
| Mistral | Admin-API (Preview) monatlich nach Workspace | ein Workspace pro Mandant, mit Ausgabelimit |

Quellen: https://developers.openai.com/cookbook/examples/completions_usage_api, https://platform.claude.com/docs/en/manage-claude/usage-cost-api, https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/add-labels-to-api-calls, https://docs.mistral.ai/admin/admin-api/usage-metrics

**Muster (E):** Gateway berechnet Echtzeitkosten für Budgets; ein Anbieter-Projekt bzw. Workspace pro Mandant; täglicher Abgleich gegen die Kosten-APIs (Alarm ab 1 %); am Monatsende ist die Anbieterrechnung maßgeblich und wird anteilig auf Gruppen und Nutzer verteilt – damit gilt ≤ 2 % auf Mandantenebene per Konstruktion. Bei eigenen Schlüsseln eines Mandanten ist der Gateway-Wert nur informativ. Projekt- und Workspace-Obergrenzen der Anbieter sind ungeprüft.

## 4. Mandanten-Trennung (ADR-008)

| Option | Für | Gegen |
|---|---|---|
| Ein gemeinsames System (LibreChat mit `TENANT_ISOLATION_STRICT`) | geringster Betrieb und Ressourcenbedarf | Trennung hängt an Beta-Code (vgl. #15975); Datenleck zwischen Mandanten wäre der schwerste Fehler; Verschlüsselung pro Mandant auf Feldebene nötig |
| **App-Instanz je Mandant, eigene Datenbank je Mandant, gemeinsamer DB-Server und gemeinsames Gateway** – gewählt | Trennung über Prozess- und Datenbankgrenzen statt Query-Filter; Verschlüsselung und Löschung pro Mandant über eigene Datenbank einfacher; deckt sich mit LibreChats eigener Richtung (DB pro Organisation); Branding pro Mandant über eigene Konfiguration | N Instanzen updaten und überwachen (per Skript); ca. 1–2 GB RAM je Mandant (E); Betreiber-Ebene über alle Instanzen selbst bauen |
| Komplett getrennte Stacks je Mandant | maximale Trennung | höchster Betriebs- und Kostenaufwand für eine Person |
