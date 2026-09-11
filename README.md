# JFXAI4CRM — Open-Source Alternative Integration Architecture
## LinkedIn Sales Navigator + Local gpt-oss Inference

> **Project focus:** AI-Powered CRM & Customer Relationship Management Platform  
> **Goal:** reorganize the JFXAI4CRM technology catalog into a modular, open, replaceable CRM architecture and add an **optional licensed LinkedIn Sales Navigator integration boundary** connected to a **private local gpt-oss inference layer**.
>
> **Key principle:** the JFXAI4CRM core remains open-source. LinkedIn Sales Navigator is treated as an **external proprietary integration** isolated behind an adapter so the platform can operate without it.

---

# 1. Source Project Direction

JFXAI4CRM is an open-source AI-powered CRM ecosystem integrating:

- CRM;
- ERP;
- hotel management;
- contact-center operations;
- sales automation;
- B2B outreach;
- low-code platforms;
- business intelligence;
- Customer 360;
- predictive sales intelligence;
- AI agents and business workflows.

The current technology catalog includes:

- LeadCMS
- ExcursioX
- OMniLeads
- OpenOutreach
- Frappe CRM
- Apex Libra
- Corteza
- openCRX
- ONLYOFFICE CRM
- Axelor
- EspoCRM
- NocoBase
- Huly
- Krayin CRM
- Twenty
- Odoo
- SuiteCRM
- Idurar ERP/CRM
- Dolibarr

The project also preserves the engineering lifecycle:

```text
MBSE
├── CAD
├── CAM
└── CAS
```

with Arcadia/Capella as a systems-engineering reference.

---

# 2. Target Integration Principle

The catalog should not become one monolithic deployment.

Instead:

```text
Customer / Prospect Data
        ↓
CRM Core
        ↓
Integration Bus
        ↓
AI / Sales Intelligence
        ↓
Workflow / BPM
        ↓
Human Sales Action
        ↓
Outcome
        ↓
Learning
```

The platform should use stable contracts so CRM, ERP, contact-center, low-code, BI and AI components can be replaced independently.

---

# 3. High-Level Alternative Architecture

```text
┌─────────────────────────────────────────────────────────────────────────┐
│                            USERS                                        │
│ Sales | Marketing | Support | Managers | Executives                    │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     CRM EXPERIENCE LAYER                                │
│ Twenty | Frappe CRM | EspoCRM | SuiteCRM | Travel / Hotel UI          │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                       API / DOMAIN LAYER                                │
│ Accounts | Contacts | Leads | Opportunities | Activities | Cases       │
│ REST | GraphQL | Webhooks | Events | MCP                               │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                ┌──────────────┼────────────────┐
                │              │                │
                ▼              ▼                ▼
┌───────────────────┐ ┌─────────────────┐ ┌─────────────────────────────┐
│ BPM / LOW-CODE    │ │ CRM INTEGRATION │ │ SALES INTELLIGENCE          │
│ Axelor            │ │ ERP / Hotel     │ │ Lead scoring                │
│ Corteza           │ │ Contact Center  │ │ Opportunity ranking         │
│ NocoBase          │ │ E-commerce      │ │ Next-best-action            │
└─────────┬─────────┘ └────────┬────────┘ └────────────┬────────────────┘
          │                    │                       │
          └────────────────────┼───────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                    AI ORCHESTRATION LAYER                               │
│ Sales Agent | Research Agent | Marketing Agent | Support Agent          │
│ RAG | Structured Outputs | Business Rules | Human Approval             │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                    LOCAL gpt-oss INFERENCE                              │
│ gpt-oss-20b → workstation / edge / low-latency                         │
│ gpt-oss-120b → private GPU server / datacenter                          │
│ Ollama | vLLM | llama.cpp | Transformers                               │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
         ┌─────────────────────┼─────────────────────────┐
         ▼                     ▼                         ▼
┌─────────────────┐  ┌─────────────────────┐  ┌──────────────────────────┐
│ CRM DATA        │  │ RAG / KNOWLEDGE     │  │ LINKEDIN SALES NAVIGATOR │
│ PostgreSQL      │  │ Qdrant              │  │ Licensed External Adapter│
│ OpenSearch      │  │ Documents           │  │ CRM Sync / approved APIs │
└─────────────────┘  └─────────────────────┘  └──────────────────────────┘
```

---

# 4. Open Core vs External Services

```text
OPEN-SOURCE CORE
────────────────────────────────────────────
CRM
BPM
Low-code
AI orchestration
gpt-oss
RAG
PostgreSQL
Qdrant
OpenSearch
BI
Contact center
Integration APIs

                ↕ controlled adapter

EXTERNAL / PROPRIETARY SERVICES
────────────────────────────────────────────
LinkedIn Sales Navigator
Commercial email providers
Commercial telephony
Optional cloud AI
Optional commercial CRM bridges
```

This prevents Sales Navigator from becoming a mandatory runtime dependency.

---

# 5. Recommended CRM Core

A production architecture should select **one primary CRM core**.

## Twenty

Best for:

- modern CRM workflows;
- developer-oriented extensibility;
- account/contact/opportunity management;
- API-first customization.

**Classification:** Primary modern CRM candidate.

## Frappe CRM

Best for:

- CRM + Frappe ecosystem;
- rapid customization;
- integration with ERP-style business systems;
- open enterprise applications.

**Classification:** Primary integrated-business CRM candidate.

## EspoCRM

Best for:

- lightweight mature CRM;
- sales automation;
- extensible customer-management workflows.

**Classification:** Mature CRM alternative.

## SuiteCRM

Best for:

- broad enterprise CRM capabilities;
- migration from traditional CRM environments;
- feature-rich open deployments.

**Classification:** Enterprise CRM alternative.

Recommended selection profile:

```text
Modern Developer CRM      → Twenty
ERP-Centric Open Platform → Frappe CRM
Lightweight Mature CRM    → EspoCRM
Feature-Rich Enterprise   → SuiteCRM
```

---

# 6. Canonical CRM Domain Model

```text
Account
├── Organization
├── Contacts
├── Leads
├── Opportunities
├── Activities
├── Communications
├── Campaigns
├── Cases
├── Orders
├── Contracts
├── Payments
├── Reservations
└── AI Insights
```

Canonical API examples:

```text
GET  /accounts/{id}
GET  /contacts/{id}
POST /leads
POST /opportunities
POST /activities
GET  /customer360/{id}
POST /ai/score-lead
POST /ai/next-best-action
```

---

# 7. LinkedIn Sales Navigator Integration Boundary

Sales Navigator should be treated as an **optional external sales-intelligence system**.

Preferred integration paths:

1. Sales Navigator CRM Sync, where supported and licensed.
2. Embedded Profiles / Embedded Experiences, where supported.
3. LinkedIn-approved partner APIs / Sales and Marketing Systems Connect capabilities, if authorized.
4. An optional certified CRM bridge when direct integration is unavailable.
5. Manual user-driven workflows when no approved programmatic path exists.

JFXAI4CRM should **not** depend on browser scraping or unsupported automation.

---

# 8. Important Sales Navigator Constraint

Current official Sales Navigator documentation associates CRM Sync and full CRM integration with **Sales Navigator Advanced Plus**.

Major CRM Sync integrations currently include:

- Salesforce;
- Microsoft Dynamics 365;
- HubSpot;
- Oracle Sales.

Therefore:

> JFXAI4CRM must not claim direct native CRM Sync for Frappe CRM, Twenty, EspoCRM, SuiteCRM or another open-source CRM unless LinkedIn explicitly approves that integration.

The correct architecture is an adapter boundary.

---

# 9. Sales Navigator Adapter Gateway

```text
                       LINKEDIN
                   SALES NAVIGATOR
                         │
             approved/licensed integration
                         │
                         ▼
┌──────────────────────────────────────────────────┐
│        SALES NAVIGATOR ADAPTER GATEWAY           │
│                                                  │
│ OAuth / enterprise authorization                 │
│ CRM Sync mapping                                 │
│ Activity writeback mapping                       │
│ Lead/account mapping                             │
│ Field allowlists                                 │
│ Retention controls                               │
│ Audit logs                                       │
│ Contract-policy enforcement                      │
└────────────────────────┬─────────────────────────┘
                         │
                         ▼
                 Canonical CRM API
                         │
              ┌──────────┼───────────┐
              ▼          ▼           ▼
            Lead       Account    Activity
              │          │           │
              └──────────┼───────────┘
                         ▼
                   JFXAI4CRM
```

---

# 10. Optional Certified-CRM Bridge

Where LinkedIn does not provide an approved direct integration with the selected open-source CRM, a deployment may use a supported CRM as an optional bridge:

```text
Sales Navigator
       ↕
Approved CRM Sync
       ↕
Supported CRM
       ↕
Integration Adapter
       ↕
JFXAI4CRM Canonical API
       ↕
Twenty / Frappe / Espo / SuiteCRM
```

This component remains:

**optional, proprietary, replaceable and outside the open-source core.**

---

# 11. No-Scraping Rule

The architecture should prohibit:

```text
Browser scraping
DOM extraction
Unofficial bulk export
Credential sharing
Session-cookie automation
Bypassing LinkedIn access controls
```

Process only data received through:

- approved integrations;
- permitted CRM synchronization;
- user-entered CRM data;
- authorized exports when explicitly supported.

Sales Navigator does not currently provide a general lead/account CSV/XLS export workflow, so JFXAI4CRM should not design around bulk Sales Navigator export.

---

# 12. Sales Navigator → Local gpt-oss Flow

```text
LinkedIn Sales Navigator
         │
         │ approved CRM integration only
         ▼
Canonical CRM Records
         │
         ▼
Data Minimization / Policy Filter
         │
         ├── allowed fields
         ├── retention rules
         ├── provenance
         └── access control
         │
         ▼
Private AI Context Builder
         │
         ▼
Local gpt-oss
         │
         ▼
Structured Recommendation
         │
         ▼
CRM Sales Workspace
         │
         ▼
Human Review
         │
         ▼
Sales Action
```

The local model should never browse or scrape Sales Navigator directly.

---

# 13. Local gpt-oss Inference Layer

Recommended deployment topology:

```text
gpt-oss-20b
    ↓
Local / workstation / edge inference


gpt-oss-120b
    ↓
Private GPU server / datacenter inference
```

Suggested runtimes:

- Ollama;
- vLLM;
- llama.cpp;
- Transformers.

The inference infrastructure is controlled by the organization, which is useful when CRM data should remain within a private environment.

---

# 14. gpt-oss Deployment Profiles

## Profile A — Sales Workstation

```text
CRM UI
  ↓
Local AI Gateway
  ↓
gpt-oss-20b
  ↓
Lead Summary / Draft / Recommendation
```

Use for:

- account summaries;
- lead summaries;
- follow-up drafting;
- CRM search;
- call preparation;
- structured notes.

## Profile B — Private Sales AI Server

```text
CRM Users
   ↓
AI Gateway
   ↓
vLLM
   ↓
gpt-oss-120b
   ↓
Shared Private Inference
```

Use for:

- complex account research;
- opportunity reasoning;
- cross-record analysis;
- multi-agent workflows;
- enterprise sales planning.

---

# 15. Model Router

```text
CRM Request
     │
     ▼
Task Classifier
     │
 ┌───┼─────────────────────┐
 ▼   ▼                     ▼
Rules ML Model           LLM
 │    │                    │
 │    │               ┌────┴────┐
 │    │               ▼         ▼
 │    │          gpt-oss-20b  gpt-oss-120b
 │    │
 └────┼─────────────────────┐
      ▼                     ▼
Deterministic          Generative
Business Action        Recommendation
```

| Task | Preferred engine |
|---|---|
| Deduplicate contacts | deterministic / ML |
| Lead score | calibrated ML model |
| Forecast pipeline | statistical / ML |
| Summarize account | gpt-oss |
| Draft outreach | gpt-oss |
| Explain score | gpt-oss + model evidence |
| CRM authorization | deterministic policy |
| Opportunity approval | human + business rules |

---

# 16. Sales Research Agent

```text
Salesperson
    ↓
"Prepare this account"
    ↓
Sales Research Agent
    ↓
┌────────────┬────────────┬────────────┐
│ CRM        │ Knowledge  │ LinkedIn   │
│ history    │ RAG        │ authorized │
│            │            │ CRM data   │
└────────────┴────────────┴────────────┘
    ↓
Local gpt-oss
    ↓
Structured Account Brief
```

Possible output:

```yaml
account:
  summary: ...
  open_opportunities: ...
  recent_activity: ...
  known_contacts: ...
  risks: ...
  relevant_products: ...
  recommended_next_action: ...
  evidence:
    - crm_record: ...
    - internal_document: ...
```

---

# 17. Lead Qualification Agent

```text
New Lead
   ↓
CRM Enrichment
   ↓
Allowed Sales Navigator-derived CRM fields
   ↓
Company / Product Fit
   ↓
ML Lead Score
   ↓
gpt-oss Explanation
   ↓
Human Sales Review
   ↓
Qualified / Nurture / Reject
```

Use a calibrated predictive model for numeric scoring; gpt-oss should explain and contextualize the score rather than invent it.

---

# 18. Opportunity Intelligence

```text
Opportunity
   ↓
CRM Data
   +
Activities
   +
Authorized External Sales Signals
   +
Internal Product Knowledge
   ↓
Opportunity Agent
   ↓
gpt-oss
   ↓
Opportunity Brief
   ├── buyer context
   ├── unresolved objections
   ├── missing stakeholders
   ├── inactivity risk
   ├── suggested next step
   └── confidence / evidence
```

---

# 19. Next-Best-Action Engine

```text
Customer 360
    ↓
Business Rules
    +
Predictive Models
    +
Local gpt-oss
    ↓
Candidate Actions
    ↓
Ranking
    ↓
Human Approval
    ↓
CRM Task
```

Possible actions:

- schedule call;
- send follow-up;
- request technical meeting;
- provide case study;
- update opportunity stage;
- assign account owner;
- create nurture task.

---

# 20. Outreach Architecture

The source includes OpenOutreach.

Recommended flow:

```text
Lead / Account
      ↓
Qualification
      ↓
Message Draft
      ↓
Compliance / Policy Filter
      ↓
Human Approval
      ↓
Permitted Outreach Channel
```

Avoid uncontrolled bulk messaging or autonomous outreach loops.

---

# 21. CRM Agent Architecture

```text
                      AI ORCHESTRATOR
                            │
 ┌────────────┬─────────────┼─────────────┬──────────────┐
 ▼            ▼             ▼             ▼              ▼
Research    Sales        Marketing      Support       Data Quality
Agent       Agent          Agent         Agent           Agent
 │            │             │             │              │
 └────────────┴─────────────┼─────────────┴──────────────┘
                            ▼
                      Tool Gateway / MCP
                            │
             ┌──────────────┼───────────────┐
             ▼              ▼               ▼
          CRM API         RAG API      Integration API
                                             │
                                             ▼
                                    Sales Navigator Adapter
```

---

# 22. RAG Architecture

```text
Product Documentation
Sales Playbooks
Contracts
Case Studies
CRM Notes
Support History
Hotel / Travel Catalog
        │
        ▼
Document Processing
        │
        ▼
Embeddings
        │
        ▼
Qdrant
        │
        ▼
RAG Gateway
        │
        ▼
Local gpt-oss
```

Private customer knowledge should be segmented by tenant, account and role.

---

# 23. Source Technology Classification

## Tier 1 — CRM Core Candidates

- Twenty
- Frappe CRM
- EspoCRM
- SuiteCRM

## Tier 2 — ERP / BPM / Low-Code

- Axelor
- Corteza
- NocoBase
- Odoo
- Dolibarr
- Idurar

## Tier 3 — Sales / Contact Center

- OMniLeads
- OpenOutreach
- LeadCMS
- Krayin CRM

## Tier 4 — Travel / Hospitality

- ExcursioX
- Odoo hotel-management extensions
- booking integrations

## Tier 5 — Collaboration

- Huly
- ONLYOFFICE CRM / collaboration functionality

## Tier 6 — Reference / Specialized

- openCRX
- Apex Libra
- other catalog entries requiring upstream/license validation

---

# 24. Contact Center Integration

```text
Voice / Chat / Email
       ↓
OMniLeads
       ↓
Transcription
       ↓
Conversation Processing
       ↓
Local gpt-oss
       ↓
Summary / Intent / Suggested Action
       ↓
CRM Activity
```

All LLM-generated intent, sentiment or recommendations should remain labelled as AI inference.

---

# 25. Low-Code / BPM Integration

```text
Business Requirement
       ↓
Corteza / NocoBase / Axelor
       ↓
Workflow
       ↓
Canonical CRM API
       ↓
AI Tool
       ↓
Local gpt-oss
```

Low-code systems should consume canonical services rather than write directly into AI stores.

---

# 26. ERP Integration

```text
CRM
 ↕
Integration Bus
 ↕
Axelor / Odoo / Dolibarr / Idurar
 ↕
Orders
Invoices
Products
Inventory
Payments
```

CRM remains the engagement system; ERP remains the transactional business system of record.

---

# 27. Travel / Hotel CRM

```text
Sales / Guest CRM
      ↓
ExcursioX / Hotel Layer
      ↓
Booking / Reservation
      ↓
Stay / Service
      ↓
Feedback
      ↓
Customer 360
      ↓
Local gpt-oss
      ↓
Personalized Service Recommendation
```

---

# 28. Data Platform

```text
PostgreSQL
   ├── CRM transactional data
   ├── account/contact records
   ├── opportunities
   ├── permissions
   └── audit metadata

Qdrant
   └── document / knowledge embeddings

OpenSearch
   └── search / analytics

MinIO
   └── files / documents / attachments

DuckDB
   └── local analytics / experimentation
```

---

# 29. Provenance Model

Every AI output should record where its supporting information came from.

```yaml
insight:
  type: "recommendation"
  model: "gpt-oss-20b"
  generated_at: "..."
  source_records:
    - crm:account:123
    - crm:opportunity:456
    - rag:document:789
  external_source:
    provider: "LinkedIn Sales Navigator"
    ingestion: "authorized CRM integration"
  confidence: 0.78
  human_review_required: true
```

---

# 30. FACT vs INFERENCE

JFXAI4CRM should explicitly distinguish:

```text
FACT
customer/CRM-provided field

EXTERNAL FACT
authorized LinkedIn-derived CRM field

INFERENCE
gpt-oss interpretation

PREDICTION
ML model output

RECOMMENDATION
AI/rule proposed action
```

Do not merge these categories into one unlabeled customer profile.

---

# 31. Privacy Boundary for Sales Navigator + gpt-oss

Local inference improves control of the AI processing layer, but it does **not** remove contractual restrictions on LinkedIn data.

Recommended controls:

- field-level allowlists;
- explicit source provenance;
- tenant isolation;
- RBAC / ABAC;
- encryption at rest;
- TLS in transit;
- retention limits;
- audit logs;
- deletion propagation;
- purpose limitation;
- prompt logging controls;
- no model training on LinkedIn-derived data unless explicitly permitted.

---

# 32. Sales Navigator Data Gateway

```text
Authorized Source
      ↓
Schema Validator
      ↓
Contract / License Policy
      ↓
Data Minimization
      ↓
Canonical Mapping
      ↓
CRM Record
      ↓
AI Context Eligibility Check
      ↓
Local gpt-oss
```

This is safer and more maintainable than connecting Sales Navigator directly to the LLM.

---

# 33. Human-in-the-Loop Sales Control

```text
AI Recommendation
        ↓
Evidence
        ↓
Confidence
        ↓
Policy Rules
        ↓
Human Salesperson
        ↓
Approved CRM Action
```

Human review should remain mandatory for:

- outbound messages;
- opportunity-stage changes;
- account-owner reassignment;
- contract or pricing proposals;
- high-value lead rejection;
- sensitive customer classification.

---

# 34. Recommended Open-Source Stack

| Layer | Recommended |
|---|---|
| CRM | Twenty / Frappe CRM / EspoCRM |
| Enterprise CRM alternative | SuiteCRM |
| ERP | Axelor / Odoo / Dolibarr |
| BPM | Axelor / Corteza |
| Low-Code | NocoBase / Corteza |
| Contact Center | OMniLeads |
| Outreach | OpenOutreach |
| Local LLM | gpt-oss-20b / gpt-oss-120b |
| LLM Runtime | Ollama / vLLM / llama.cpp |
| RAG | Qdrant |
| Transaction DB | PostgreSQL |
| Search | OpenSearch |
| Object Storage | MinIO |
| BI | Superset / Metabase / Grafana |
| API | FastAPI / REST / GraphQL |
| Agent Tools | MCP |
| Identity | Keycloak / OIDC |
| Containers | Docker |
| Orchestration | Kubernetes / k3s |
| Observability | OpenTelemetry / Prometheus / Grafana |
| External Sales Intelligence | LinkedIn Sales Navigator adapter |

---

# 35. Alternative Architecture Profiles

## Profile A — Fully Open CRM

```text
Frappe CRM
   ↓
FastAPI Integration
   ↓
PostgreSQL
   ↓
Qdrant
   ↓
gpt-oss-20b
   ↓
Sales Agent
```

**Best for:** fully open/private deployments with no Sales Navigator dependency.

## Profile B — Sales Navigator Assisted CRM

```text
Sales Navigator
      ↓
Approved Integration
      ↓
Sales Navigator Adapter
      ↓
Canonical CRM API
      ↓
Twenty / Frappe CRM
      ↓
Private AI Gateway
      ↓
gpt-oss-20b
```

**Best for:** sales teams using LinkedIn while keeping AI inference private.

## Profile C — Enterprise Private AI

```text
Sales Navigator
      ↓
Approved CRM Integration
      ↓
CRM
      ↓
Event Bus
      ↓
Private AI Cluster
      ↓
vLLM + gpt-oss-120b
      ↓
Sales / Account / BI Agents
```

**Best for:** larger sales organizations.

## Profile D — Contact Center CRM

```text
OMniLeads
   ↓
Conversation Data
   ↓
CRM
   ↓
RAG
   ↓
gpt-oss
   ↓
Agent Assist
   ↓
Human Operator
```

## Profile E — Travel / Hospitality

```text
ExcursioX / Odoo Hotel
        ↓
CRM Customer 360
        ↓
RAG
        ↓
gpt-oss
        ↓
Guest Service / Sales Assistant
```

---

# 36. Recommended MVP

Start with:

```text
Frappe CRM OR Twenty
       ↓
Canonical API
       ↓
PostgreSQL
       +
Qdrant
       ↓
FastAPI AI Gateway
       ↓
gpt-oss-20b
       ↓
Sales Assistant
       ↓
Human Approval
```

MVP capabilities:

- account summary;
- contact summary;
- opportunity summary;
- RAG over product documentation;
- follow-up drafting;
- lead explanation;
- next-best-action suggestions;
- structured outputs;
- audit trail.

---

# 37. MVP Phase 2 — Sales Navigator

Add only after licensing and integration-path verification:

```text
Sales Navigator
      ↓
Approved CRM Sync / Partner Integration
      ↓
Sales Navigator Adapter
      ↓
Canonical CRM Records
      ↓
gpt-oss Context
```

Initial use cases:

- account brief;
- synchronized activity context;
- CRM account/contact matching;
- CRM lead/contact creation where supported;
- activity writeback where supported;
- meeting preparation.

---

# 38. MVP Phase 3 — Predictive Sales

Add:

- calibrated lead scoring;
- opportunity scoring;
- sales forecasting;
- churn models;
- cross-sell models.

```text
CRM Features
      ↓
Predictive Models
      ↓
Scores
      ↓
gpt-oss Explanation
      ↓
Human Decision
```

---

# 39. MBSE → CAD → CAM → CAS Mapping

```text
MBSE
Arcadia / Capella
CRM ecosystem architecture
        ↓
CAD
Customer journeys, workflows, UI/domain models
        ↓
CAM
Application/service assembly and deployment
        ↓
CAS
CRM simulations
Sales-process scenarios
Load/performance testing
AI evaluation
Workflow validation
        ↓
Production
```

For JFXAI4CRM, CAS should include:

- lead-routing simulation;
- sales-funnel simulation;
- contact-center scenarios;
- AI quality testing;
- policy/access-control testing.

---

# 40. Suggested Repository Structure

```text
jfxai4crm/
├── README.md
├── docs/
│   ├── architecture/
│   ├── crm/
│   ├── sales-intelligence/
│   ├── linkedin-sales-navigator/
│   ├── local-ai/
│   ├── rag/
│   ├── privacy/
│   └── validation/
│
├── MBSE/
│   ├── Capella/
│   ├── CAD/
│   ├── CAM/
│   └── CAS/
│
├── crm/
│   ├── canonical-model/
│   ├── frappe/
│   ├── twenty/
│   ├── espocrm/
│   └── suitecrm/
│
├── integrations/
│   ├── linkedin-sales-navigator/
│   │   ├── adapter/
│   │   ├── mappings/
│   │   ├── policies/
│   │   └── tests/
│   ├── erp/
│   ├── contact-center/
│   ├── hotel/
│   └── ecommerce/
│
├── ai/
│   ├── gateway/
│   ├── gpt-oss/
│   ├── agents/
│   ├── prompts/
│   ├── structured-output/
│   └── evaluation/
│
├── rag/
│   ├── ingestion/
│   ├── embeddings/
│   └── qdrant/
│
├── data/
│   ├── postgres/
│   ├── provenance/
│   └── schemas/
│
└── tests/
    ├── crm/
    ├── linkedin/
    ├── ai/
    ├── security/
    └── integration/
```

---

# 41. Roadmap

## Phase 1 — CRM Core
- select Frappe CRM / Twenty / EspoCRM;
- canonical domain model;
- PostgreSQL;
- APIs.

## Phase 2 — Local AI
- gpt-oss-20b;
- AI gateway;
- structured outputs;
- human approval.

## Phase 3 — RAG
- Qdrant;
- product knowledge;
- sales playbooks;
- customer-history retrieval.

## Phase 4 — Sales Intelligence
- scoring;
- forecasting;
- next-best-action;
- account prioritization.

## Phase 5 — LinkedIn Sales Navigator
- verify Advanced Plus licensing;
- verify approved integration path;
- implement adapter;
- provenance and retention controls.

## Phase 6 — Contact Center
- OMniLeads;
- transcription;
- agent assist.

## Phase 7 — Enterprise AI
- gpt-oss-120b;
- vLLM;
- private GPU cluster.

## Phase 8 — BI
- Superset / Metabase / Grafana;
- CRM KPIs;
- AI quality dashboards.

---

# 42. Strategic Priority Matrix

| Component | Strategic Value | Role |
|---|---:|---|
| Frappe CRM | 5/5 | Open CRM core |
| Twenty | 5/5 | Modern CRM core |
| EspoCRM | 5/5 | Mature CRM alternative |
| SuiteCRM | 4/5 | Enterprise CRM alternative |
| Axelor | 5/5 | ERP/BPM integration |
| Corteza | 5/5 | Low-code/workflow |
| NocoBase | 4/5 | Low-code applications |
| OMniLeads | 5/5 | Contact-center core |
| OpenOutreach | 4/5 | Controlled outreach |
| ExcursioX | 4/5 | Travel CRM |
| Odoo | 4/5 | ERP/hotel integration |
| PostgreSQL | 5/5 | Transactional data |
| Qdrant | 5/5 | RAG/vector layer |
| OpenSearch | 4/5 | Search/analytics |
| gpt-oss-20b | 5/5 | Local sales inference |
| gpt-oss-120b | 5/5 | Private enterprise reasoning |
| LinkedIn Sales Navigator | 5/5 business value | Optional external sales intelligence |
| Sales Navigator Adapter | 5/5 | Isolation/compliance boundary |

---

# 43. Final Recommended Architecture

```text
                         JFXAI4CRM
                             │
                    CRM EXPERIENCE
               Frappe / Twenty / Espo
                             │
                             ▼
                     CANONICAL CRM API
                             │
              ┌──────────────┼───────────────┐
              ▼              ▼               ▼
             BPM          CRM DATA       INTEGRATIONS
       Corteza/Axelor    PostgreSQL            │
              │              │                 ├── ERP
              │              │                 ├── OMniLeads
              │              │                 ├── Hotel
              │              │                 └── Sales Navigator
              │              │                      │
              │              │               approved adapter
              │              │                      │
              └──────────────┼──────────────────────┘
                             ▼
                      AI DATA POLICY
                             │
                             ▼
                        RAG / Qdrant
                             │
                             ▼
                   LOCAL AI GATEWAY
                 ┌───────────┴───────────┐
                 ▼                       ▼
           gpt-oss-20b             gpt-oss-120b
           Local / Edge            Private Server
                 │                       │
                 └───────────┬───────────┘
                             ▼
                     CRM AI AGENTS
                             │
               ┌─────────────┼─────────────┐
               ▼             ▼             ▼
             Sales        Marketing      Support
               │             │             │
               └─────────────┼─────────────┘
                             ▼
                       HUMAN REVIEW
                             │
                             ▼
                       CRM ACTION
```

---

# 44. Strategic Recommendation

The strongest open/private stack is:

```text
Frappe CRM or Twenty
        +
PostgreSQL
        +
Qdrant
        +
FastAPI
        +
MCP
        +
gpt-oss-20b
        +
optional gpt-oss-120b
        +
Corteza / Axelor
        +
OMniLeads
```

with LinkedIn Sales Navigator treated strictly as a **licensed optional external sales-intelligence source** connected through an approved integration boundary.

> **LinkedIn provides permitted sales context; JFXAI4CRM owns the CRM workflow; gpt-oss performs private inference; humans remain responsible for customer-facing actions.**

---

# 45. External Integration Notes — LinkedIn Sales Navigator

Current Sales Navigator documentation indicates:

- CRM integration requires **Sales Navigator Advanced Plus**;
- CRM Sync can support auto-save/import and selected activity writeback depending on CRM and configuration;
- major supported CRM Sync integrations include Salesforce, Microsoft Dynamics 365, Oracle Sales and HubSpot;
- Sales Navigator uses dedicated partner integration mechanisms such as Sales and Marketing Systems Connect for approved CRM partners;
- general Sales Navigator lead/account CSV or XLS export is not currently provided.

JFXAI4CRM should verify the organization's LinkedIn contract, plan, partner eligibility, permissions, retention rules and allowed data uses before implementation.

---

# 46. External Integration Notes — gpt-oss

OpenAI currently provides:

- **gpt-oss-20b** — open-weight reasoning model intended for lower-latency, local or specialized workloads;
- **gpt-oss-120b** — higher-capacity open-weight reasoning model suitable for private GPU infrastructure.

The models are distributed under the Apache 2.0 license subject to the applicable gpt-oss usage policy and can be self-hosted with runtimes such as:

- vLLM;
- Ollama;
- llama.cpp;
- Transformers.

The open-weight models are self-managed rather than served through the OpenAI API.

---

# 47. Responsible AI & Sales Governance

Do not use the system to:

- infer protected or highly sensitive personal traits;
- rank prospects based on protected characteristics;
- fabricate information about contacts;
- send uncontrolled automated outreach;
- bypass LinkedIn access controls;
- scrape Sales Navigator;
- treat AI inference as CRM fact.

Recommended flow:

```text
Authorized Data
      ↓
Local AI
      ↓
Evidence + Confidence
      ↓
Human Review
      ↓
Permitted CRM Action
```

---

# 48. References

## JFXAI4CRM
- https://github.com/robotics-intelligent-systems/jfxai4crm

## LinkedIn Sales Navigator
- https://www.linkedin.com/help/sales-navigator/answer/a106005/integration-between-sales-navigator-and-your-crm-overview
- https://www.linkedin.com/help/sales-navigator/answer/a107066
- https://www.linkedin.com/help/sales-navigator/answer/a110717

## gpt-oss
- https://openai.com/open-models/
- https://help.openai.com/en/articles/11870455

---

# 49. Disclaimer

This is a proposed integration architecture derived from the current JFXAI4CRM software catalog plus a proposed LinkedIn Sales Navigator and local gpt-oss integration.

It does not claim that LinkedIn Sales Navigator natively supports the open-source CRM products in the repository.

LinkedIn licensing, partner eligibility, API availability, CRM Sync capabilities, data use, retention requirements and integration permissions must be verified before implementation.

gpt-oss is an open-weight model family; surrounding inference infrastructure, hardware, CRM systems, LinkedIn services and third-party integrations may have separate licenses and operating costs.

AI-generated lead assessments, customer summaries, outreach drafts, sales recommendations and predictions should be treated as decision-support outputs and remain subject to business rules and human review.
