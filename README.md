# Donatus Gwer — Full-Stack / Backend Engineer

I build payment systems, operational software, secure APIs, automation, and internal business tools with Python and Django. My work focuses on reliable workflows: access boundaries, transaction correctness, reconciliation, auditability, and recovery when dependencies fail.

## Technical Stack

- **Backend & data:** Python, Django, Django REST Framework, FastAPI, PostgreSQL, Redis, Celery, Kafka.
- **Frontend:** React, Next.js, TypeScript.
- **Delivery & operations:** Docker, GitHub Actions, container deployment configurations for Kubernetes and VPS environments; pytest, Django tests, linting and type checks.
- **Security & observability:** role-based access control, tenant/workspace scoping, signed webhooks and audit records, encrypted integration credentials; Prometheus, Grafana, OpenTelemetry, structured logging.

## Featured Engineering Work

### 1. [Sentinel](https://github.com/Gwerdonatus/Sentinel) — Security and audit platform

Centralizes security events, risk signals, and audit trails for business applications. A modular Django/DRF backend separates services and repositories, with tenant-aware access, role permissions, API keys, and HMAC-signed audit records. Celery/Redis and Kafka support event processing; a Next.js interface exposes the workflows. Unit and integration tests, coverage-gated CI, container/Kubernetes configurations, monitoring configuration, architecture decisions, and incident runbooks demonstrate attention to operating the system.

### 2. [TxCore](https://github.com/Gwerdonatus/txcore) — Payment processing prototype

Explores transaction intake, settlement, and reconciliation as a backend system. Decimal transaction storage and database uniqueness underpin idempotency; Redis supports replay responses, HMAC validates incoming webhooks, Kafka publishes events, and Celery models settlement work. API and reconciliation tests, an 80% CI coverage gate, Docker Compose, and Prometheus metrics make the design inspectable. Settlement is simulated; provider integration and failure recovery still need hardening.

### 3. [drift-recon](https://github.com/Gwerdonatus/drift-recon) — Reconciliation and drift detection

Helps identify discrepancies between financial data sources. The FastAPI service separates ingestion from a deterministic weighted matcher, prevents duplicate match assignments, and quarantines invalid CSV rows. PostgreSQL upserts, persistent scheduled jobs, API-key checks, structured logs, and operational runbooks support repeatable operation. Its green CI builds both API and dashboard images and runs 68 tests with a 70% coverage gate.

### 4. [FinOps](https://github.com/Gwerdonatus/FinOps) — Refund and dispute operations

Organizes financial support work around workspaces, case status, and SLA risk. Django modules handle Stripe synchronization, refund/dispute workflows, alerts, and CSV/PDF evidence exports. Encrypted integration credentials, workspace membership checks, POST-only mutations, and CSRF protection establish security boundaries. Its Python 3.11/3.12 CI verifies access isolation, exports, risk calculations, and workflow safety with a coverage gate.

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

[Email](mailto:donatusgwer@gmail.com) · [LinkedIn](https://linkedin.com/in/donatus-gwer) · [Portfolio](https://donatus-gwer.vercel.app)
