# FraudWatch — Real-Time Fraud Detection & Risk Scoring Engine | PROJECT LINK  
**Pre-authorization risk intelligence for modern payment infrastructure with streaming decisions, ledger-grade auditability, and low-latency guardrails**

<img width="2294" height="3541" alt="Fraudwatch-3" src="https://github.com/user-attachments/assets/b3f25c7f-67d6-455c-b0ce-bf56cce9efb6" />

![License](https://img.shields.io/badge/License-MIT-success)
![Status](https://img.shields.io/badge/Status-Public%20Prototype-blue)
![Domain](https://img.shields.io/badge/Domain-Embedded%20Payments%20%7C%20Risk%20%7C%20Fraud-0b7285)
![Streaming](https://img.shields.io/badge/Streaming-Apache%20Kafka-231F20)
![Backend](https://img.shields.io/badge/Backend-Python%20%7C%20FastAPI-009688)
![APIs](https://img.shields.io/badge/APIs-REST%20(Representational%20State%20Transfer)-111111)
![Data](https://img.shields.io/badge/Data-PostgreSQL%20%7C%20Redis-336791)
![Architecture](https://img.shields.io/badge/Architecture-Event--Driven%20%7C%20Policy%20%2B%20Model%20Hybrid-black)
![Identity](https://img.shields.io/badge/Signals-KYC%20(Know%20Your%20Customer)%20%7C%20KYB%20(Know%20Your%20Business)-6d28d9)
![Risk](https://img.shields.io/badge/Risk-Velocity%20%7C%20Device%20Fingerprint%20%7C%20Merchant%20Trust-critical)
![Ledger](https://img.shields.io/badge/Audit-Ledger--Style%20Risk%20Decisions-7c3aed)
![Observability](https://img.shields.io/badge/Observability-Prometheus%20%7C%20OpenTelemetry-111111)
![Deploy](https://img.shields.io/badge/Deploy-Docker%20%7C%20Amazon%20Web%20Services%20(AWS)-2496ED)
![Latency](https://img.shields.io/badge/Performance-p95%20(target)%20%3C%20350ms-brightgreen)
![Mindset](https://img.shields.io/badge/Mindset-Safety%20%7C%20Conversion%20%7C%20Latency%20Trade--offs-1f6feb)

FraudWatch is a **real-time fraud detection and risk scoring engine** built to operate **in the critical pre-authorization path** of payment flows.  
It ingests transaction-like events via **Apache Kafka**, applies a **hybrid rules + machine-learning feature pipeline**, and serves **low-latency risk decisions** through **FastAPI**.

This repository is designed to demonstrate the systems thinking expected in modern embedded payments risk teams:

- high-throughput, event-driven ingestion  
- near-real-time scoring  
- **KYC (Know Your Customer)** and **KYB (Know Your Business)**-aware risk posture  
- merchant trust and onboarding risk gates  
- velocity and device fingerprint anomaly detection  
- dispute and chargeback feedback alignment  
- **ledger-grade auditability** for explainability and investigations  
- observability shaped around **p95 latency** and false-positive pressure

**Core philosophy**  
**Pre-authorization safety → Explainable decisions → Ledger-grade traceability → Low latency by design**

---

## Table of Contents
- Why Real-Time Payment Risk Is Hard  
- Vision and Motivation  
- What FraudWatch Does (End-to-End)  
- Design Tenets  
- What’s Implemented  
- Feature Deep Dives  
  - Streaming Ingestion  
  - Risk Orchestrator  
  - Identity and Merchant Risk (KYC/KYB)  
  - Velocity and Device Fingerprinting  
  - Disputes/Chargebacks Feedback Modeling  
  - Ledger-Style Audit Store  
  - Observability and Latency Discipline  
- Architecture  
- Decision Lifecycle  
- Core Data Structures and Algorithms  
- Technology Stack  
- Repository Structure  
- Quickstart  
- Configuration  
- Example API Requests  
- Safety and Compliance Notes  
- Roadmap  
- Maintainer  

---

## Why Real-Time Payment Risk Is Hard

Fraud prevention in payment infrastructure is not a background task.  
It is a **milliseconds-sensitive, conversion-critical decision system** that must balance three competing truths:

1. **Safety** — stop fraud loss early.  
2. **Conversion** — avoid blocking legitimate customers and merchants.  
3. **Latency** — slow risk checks degrade authorization success and user trust.

The costliest failures often come from system-level gaps:

- inconsistent policy enforcement across rails  
- incomplete or stale identity signals  
- over-aggressive velocity rules that punish normal growth  
- weak linkage between risk decisions and downstream outcomes  
- poor audit trails that make false positives unexplainable  
- brittle tuning workflows that require code changes

FraudWatch is structured to show how modern platforms build a **policy + model hybrid** risk layer with auditability and observability as first-class requirements.


## Vision and Motivation

FraudWatch demonstrates the engineering mindset required for payment risk systems that scale:

- treat risk decisions as **financial events**  
- store them with **ledger semantics**  
- design for **investigation** as a primary user  
- cleanly separate **policy** from **model** for safe, rapid tuning  
- instrument for **latency budgets** and rule/model drift

The project reflects how modern risk teams enable marketplace and platform growth without blind exposure—by building fast, explainable decisioning that can be reconciled against disputes and chargebacks.

---

## What FraudWatch Does (End-to-End)

1. **Consumes transaction-like events** from Apache Kafka topics (simulated card networks and payment rails).  
2. **Enriches events** with identity, merchant, device, and historical context.  
3. **Computes features** for velocity, anomaly signals, and trust baselines.  
4. **Evaluates deterministic rules** for high-confidence policy gates.  
5. **Calculates model-ready features** for nuanced scoring.  
6. **Returns a structured risk decision** that can:  
   - allow  
   - block  
   - step-up (additional verification)  
7. **Writes a ledger-style decision record** to PostgreSQL and caches hot signals in Redis.  
8. **Exposes REST risk APIs** for synchronous pre-authorization checks, testing, and investigation workflows.  
9. **Emits metrics, logs, and traces** for operational tuning and incident response.

---

## Design Tenets

1. **Risk is an inline service.**  
2. **Rules and models must co-exist safely.**  
3. **Identity posture is a first-class signal.**  
4. **Every decision should be explainable.**  
5. **Latency budgets are product requirements.**  
6. **Disputes/chargebacks must close the loop.**

---

## What’s Implemented

### Streaming + Decisioning
- Apache Kafka consumer pipeline for transaction-like events  
- risk orchestrator integrating:  
  - deterministic policy rules  
  - machine-learning feature computation  

### Signals Modeled
- **KYC** and **KYB** posture  
- merchant onboarding risk and trust baselines  
- velocity limits across user, device, and merchant entities  
- device fingerprint anomalies  
- historical disputes/chargebacks alignment (simulated)

### Storage + Audit
- PostgreSQL for durable transaction and decision ledgers  
- Redis for hot counters and sliding-window caches  
- ledger-style audit records enabling:  
  - false-positive debugging  
  - fraud-ring hypothesis building  
  - reconciliation against downstream outcomes

### Observability + Deployment
- Prometheus metrics  
- OpenTelemetry traces  
- Dockerized services  
- Amazon Web Services (AWS)-ready deployment scaffolding

---

## Feature Deep Dives

### Streaming Ingestion

FraudWatch consumes high-throughput transaction-like events via Apache Kafka.  
The ingestion layer is structured for platform-style growth:

- partition-friendly consumer groups  
- idempotent processing semantics  
- deterministic replays for evaluation  
- clean separation of ingestion vs enrichment vs decisioning

---

### Risk Orchestrator (Policy + Model Hybrid)

The orchestrator enforces the sequence that modern risk stacks rely on:

**Enrich → Gate → Score → Decide → Audit**

Rules act as high-confidence guardrails.  
Feature-driven scoring provides probabilistic nuance and supports safer threshold tuning without destabilizing core policy.

---

### Identity and Merchant Risk (KYC/KYB)

FraudWatch models identity posture as a primary axis:

- KYC completeness, tier, and verification age  
- KYB depth and onboarding risk signals  
- merchant trust scoring  
- early indicators of abnormal dispute exposure

This reflects how modern platforms evaluate both sides of risk: **payer** and **merchant**.

---

### Velocity and Device Fingerprinting

The velocity engine models:

- short-window bursts  
- medium-window drift  
- entity-linked cascades across device and merchant graphs  

Redis-backed counters support authorization-speed checks.

---

### Disputes/Chargebacks Feedback Modeling

FraudWatch stores decision context so it can be reconciled against:

- simulated chargebacks  
- dispute categories  
- merchant portfolio risk changes  

This creates the foundation for drift analysis and policy recalibration.

---

### Ledger-Style Audit Store

FraudWatch treats risk decisions like financial records:

- structured snapshots of reasons and features  
- policy and model version identifiers  
- decision-latency capture  
- reproducible investigation trails

---

### Observability and Latency Discipline

Instrumentation supports:

- p50 and p95 latency tracking  
- rule-trigger rates  
- step-up action ratios  
- Kafka lag and consumer health  
- false-positive simulation baselines

---

## Architecture

<img width="2794" height="1479" alt="Fraudwatch-1" src="https://github.com/user-attachments/assets/ac4b3c0b-d148-4de4-92e7-7482e8ca80ef" />

## Decision Lifecycle

<img width="4096" height="794" alt="Fraudwatch-2" src="https://github.com/user-attachments/assets/c387d2bf-65a8-4ef1-a09a-befc35c04933" />

## Core Data Structures and Algorithms

### Core data structures

**TransactionEvent**  
- id, timestamp, amount, currency  
- payer_id, merchant_id, device_id  
- rail_type, country, risk_context

**IdentityProfile**  
- KYC tier, verification_age, anomalies

**MerchantProfile**  
- KYB tier, onboarding_risk, historical_dispute_rate

**VelocityWindow**  
- entity_id, window_size, count, amount_sum

**RiskDecision**  
- fraud_score, risk_level  
- action: allow | block | step_up  
- rule_hits, feature_snapshot  
- policy_version, model_version  
- decision_latency_ms

### Key algorithms

- sliding-window velocity aggregation with Redis-backed counters  
- rule-priority short-circuiting for high-confidence blocks  
- score thresholding tuned for safety vs conversion trade-offs  
- ledger-style write patterns enabling replay and investigation

---

## Technology Stack

### Backend
- Python  
- FastAPI  
- Apache Kafka  
- PostgreSQL  
- Redis  
- Prometheus  
- OpenTelemetry  

### Infrastructure
- Docker  
- Amazon Web Services (AWS) deployment scaffolding

---

## Repository Structure

```text
/
├── backend/
│   ├── api/
│   ├── consumers/
│   ├── orchestrator/
│   ├── rules/
│   ├── features/
│   ├── scoring/
│   ├── storage/
│   └── observability/
├── infra/
│   ├── docker/
│   └── aws/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── golden-events/
└── docs/
    ├── brand/
    │   ├── fraudwatch-logo.svg
    │   ├── fraudwatch-favicon-32.png
    │   ├── fraudwatch-favicon-48.png
    │   └── fraudwatch-favicon-96.png
    └── images/
        ├── problem-map-fraud.png
        ├── ui-risk-dashboard.png
        └── architecture.png
```

---

## Quickstart

```bash
git clone <YOUR_REPO_URL>
cd FRAUDWATCH-REALTIME-FRAUD-RISK-ENGINE
```

### Start dependencies (example)

```bash
docker compose up -d kafka postgres redis
```

### Backend

```bash
cd backend
cp .env.example .env
pip install -r requirements.txt
pytest
uvicorn api.main:app --reload
```

---

## Configuration

Example `.env` keys you can align to your implementation:

```bash
# Kafka
KAFKA_BROKERS=localhost:9092
KAFKA_TOPIC_TRANSACTIONS=fraudwatch.transactions
KAFKA_CONSUMER_GROUP=fraudwatch-risk

# Postgres
POSTGRES_DSN=postgresql://user:pass@localhost:5432/fraudwatch

# Redis
REDIS_URL=redis://localhost:6379/0

# Risk
RISK_POLICY_VERSION=v1
RISK_MODEL_VERSION=baseline-v0
RISK_BLOCK_THRESHOLD=0.92
RISK_STEPUP_THRESHOLD=0.65

# Observability
OTEL_SERVICE_NAME=fraudwatch
PROMETHEUS_ENABLED=true
```

---

## Example API Requests

### Pre-authorization risk check

```http
POST /risk/score
Content-Type: application/json
Authorization: Bearer <JWT>

{
  "transaction_id": "tx_123",
  "amount": 129.50,
  "currency": "USD",
  "payer_id": "u_1001",
  "merchant_id": "m_9009",
  "device_id": "d_77",
  "rail_type": "card_sim",
  "country": "US",
  "kyc_tier": "verified",
  "kyb_tier": "standard"
}
```

Example response:

```json
{
  "transaction_id": "tx_123",
  "fraud_score": 0.71,
  "risk_level": "medium",
  "action": "step_up",
  "rule_hits": ["velocity_spike_5m"],
  "policy_version": "v1",
  "model_version": "baseline-v0",
  "decision_latency_ms": 143
}
```

---

## Safety and Compliance Notes

FraudWatch is a public engineering prototype intended to demonstrate:

- real-time risk architecture  
- KYC/KYB-aware decisioning  
- ledger-style audit patterns  
- pre-authorization safety controls  
- conversion-aware latency discipline

It is not a certified production fraud platform.  
No real payment credentials are required or intended for use in this demo.

---

## Roadmap

- Graph-based fraud-ring detection across payer-device-merchant clusters  
- Replayable incident timelines with decision diffing  
- Expanded rail simulation (wallet-like and account-to-account flows)  
- Policy-as-configuration with hot reload  
- Advanced evaluation harness for:  
  - false positive rate  
  - conversion impact simulation  
  - chargeback alignment accuracy  
- Multi-tenant risk isolation patterns for platform-style merchants

---

## Maintainer

**Pavankalyan Ghanta**  
GitHub: <your link>  
Portfolio: <your link>  
LinkedIn: <your link>

<!-- End of README -->


