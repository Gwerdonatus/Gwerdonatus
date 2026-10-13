# Donatus Gwer — Full-Stack / Backend Engineer

I build payment systems, operational software, secure APIs, automation, and internal business tools with Python and Django. My work focuses on reliable workflows: access boundaries, transaction correctness, reconciliation, auditability, and recovery when dependencies fail.

Based in Nigeria. Open to backend and full-stack opportunities, including international roles with relocation and visa support.

## Product and Client Work

### [Proova](https://proova.app) — Live-tested founder product

I built and tested Proova live: a revenue-attribution product that connects campaign and influencer clicks to payments, including sales that continue through WhatsApp or other off-site channels. The implementation includes server-side event capture, CSV reconciliation, revenue reporting and Stripe/Paystack billing integrations. I own the product's API design, data models and deployment workflows. The public site currently offers early access; live testing is not a claim of established customer adoption.

### Sinzu and Sanmark — Client websites

Designed and built websites for client brands, including Sinzu and Sanmark. My website work also includes Stripe and Paddle payment integrations. These are client engagements, separate from the independent engineering projects below.

### Blakdhut — Client crypto platform

Built a crypto-to-naira platform with Django, a double-entry ledger, deposit processing, wallet APIs and Flutter mobile clients. Deposit and sweep workflows have recorded verification on TRON Shasta and Ethereum Sepolia testnets. The application is currently offline; this is not a claim of mainnet operation or a production launch.

[Portfolio and engineering writing](https://www.gwer.space)

## Open-source Contributions

These upstream pull requests are **submitted and awaiting review**, not merged. Status checked 13 October 2026.

| Project | Contribution | Verification |
|---|---|---|
| [Anymail #495](https://github.com/anymail/django-anymail/pull/495) | Document Django 6.1 MAILERS configuration, provider options and multiple backends | 1,242 local tests; upstream CI and documentation build passed |
| [dj-stripe #2250](https://github.com/dj-stripe/dj-stripe/pull/2250) | Correct the Stripe Connect SDK argument and remove obsolete customer-source synchronization | 568 tests passed on both SQLite and PostgreSQL; Actions awaits maintainer approval |
| [django-redis #851](https://github.com/jazzband/django-redis/pull/851) | Distinguish cached `None` from missing keys during version changes | 2,065 tests passed, 7 skipped; pre-commit.ci passed; Actions awaits maintainer approval |

[Engineering case study: versioning a cached None value](case-studies/django-redis-cached-none.md)

## Technical Stack

- **Backend & data:** Python, Django, Django REST Framework, FastAPI, PostgreSQL, Redis, Celery, Kafka.
- **Frontend:** React, Next.js, TypeScript.
- **Delivery & operations:** Docker, GitHub Actions, container deployment configurations for Kubernetes and VPS environments; pytest, Django tests, linting and type checks.
- **Security & observability:** role-based access control, tenant/workspace scoping, signed webhooks and audit records, encrypted integration credentials; Prometheus, Grafana, OpenTelemetry, structured logging.

## Selected Independent Engineering Projects

### 1. [Sentinel](https://github.com/Gwerdonatus/Sentinel) — Security and audit platform

Records activity from people, services and AI agents, then links explainable risk alerts to triggering events and actor history. Django/DRF and Next.js support scoped API keys, credential-derived actor identity, versioned HMAC signatures, a transactional outbox and idempotent alert creation. The walkthrough shows synthetic AI-agent and human incidents; Sentinel does not move money or automatically block another application's actions. Local verification recorded 314 passing backend tests and 72.58% statement coverage.

[Screenshots, scoring examples and setup](https://github.com/Gwerdonatus/Sentinel/tree/fix/reliable-audit-pipeline) · [Implementation PR](https://github.com/Gwerdonatus/Sentinel/pull/1)

### 2. [TxCore](https://github.com/Gwerdonatus/txcore) — Payment operations sandbox

Implements caller-scoped idempotent payment intake, Stripe-hosted test Checkout, signed and deduplicated provider events, missed-webhook recovery, a transactional outbox and statement reconciliation. A real Stripe sandbox Checkout completed the verified local workflow; no live funds moved. The `settled` state means a verified paid Checkout session, not bank payout settlement. Local checks recorded 88 PostgreSQL tests and 91.34% application coverage in the SQLite suite.

[Screenshots, provider workflow and setup](https://github.com/Gwerdonatus/txcore/tree/docs/recruiter-walkthrough) · [Implementation PR](https://github.com/Gwerdonatus/txcore/pull/1)

### 3. [drift-recon](https://github.com/Gwerdonatus/drift-recon) — Reconciliation and drift detection

Compares internal transactions with statement rows using an explainable weighted matcher, then flags changes in reconciliation quality. FastAPI/PostgreSQL ingestion includes duplicate protection, invalid-row quarantine and recorded human review. Read-only Stripe sandbox synchronization matched three independently imported TxCore payments totaling USD 33; it does not establish a bank deposit. Local verification recorded 87 backend tests and 77.01% coverage.

[Screenshots, matching rules and setup](https://github.com/Gwerdonatus/drift-recon/tree/fix/recruiter-demo) · [Implementation PR](https://github.com/Gwerdonatus/drift-recon/pull/1)

### 4. [FinOps](https://github.com/Gwerdonatus/FinOps) — Refund and dispute operations

Helps a support team prioritize refund deadlines, investigate disputes and export PDF/CSV evidence summaries. Django workflows include workspace isolation, encrypted connector credentials, read-only Stripe sandbox imports and private attachments. Optional OpenAI case briefs require consent and exact supporting quotes; a real AI-provider call remains unverified because credentials are not configured. Local verification recorded 42 tests and 75.93% coverage. No provider refund or dispute submission is performed.

[Screenshots, deadline rules and setup](https://github.com/Gwerdonatus/FinOps/tree/fix/recruiter-demo) · [Implementation PR](https://github.com/Gwerdonatus/FinOps/pull/1)

The four walkthrough branches above contain the current demo updates; their implementation PRs remain unmerged. Screenshots use labelled synthetic data or Stripe test-mode records. Verification numbers describe recorded local runs, not production traffic or performance benchmarks.

### 5. [Ledgerlens-recon](https://github.com/Gwerdonatus/Ledgerlens-recon) — Focused payment reconciliation tool

Compares processor records with internal ledger data and produces actionable discrepancy reports. The Python CLI keeps matching separate from Stripe/CSV/database adapters and Excel output, using exact Decimal arithmetic, currency-aware Stripe minor units, bounded cursor pagination, duplicate detection, and deterministic classification. CI covers Python 3.10–3.12, packaging, formatting, linting, and 21 tests with an 80% coverage gate.

### 6. [alerts-monitoring-dashboard](https://github.com/Gwerdonatus/alerts-monitoring-dashboard) — Operational alerts interface

A full-stack operational interface for reviewing employee alerts across a management hierarchy. Django/DRF and React/TypeScript implement direct/subtree filtering, bounded pagination, validation, and idempotent dismissal. Token authentication derives manager identity server-side, while object-level checks prevent cross-manager reads and dismissals. Green CI runs 14 backend tests with a coverage gate and an optimized React production build.

## Engineering Principles

- **Start with the business workflow:** model states, responsibilities, exceptions, and operational needs before choosing infrastructure.
- **Prefer a modular monolith:** separate domain boundaries clearly; introduce microservices when scale or team ownership justifies the cost.
- **Treat payments as architecture:** account for transaction state, reconciliation, security, and audit trails throughout the system.
- **Design for failure:** make retries, idempotency, auditability, and recovery explicit, and test the boundaries where work can be duplicated or interrupted.

## Contact

[Email](mailto:donatusgwer@gmail.com) · [LinkedIn](https://www.linkedin.com/in/donatus-gwer-857610338/) · [Portfolio and blog](https://www.gwer.space)
