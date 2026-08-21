# AI-Powered Transaction Optimization & Risk Management

> An intelligent **n8n automation workflow** for transaction validation, duplicate detection, historical analysis, AI-powered risk assessment, automated routing, and operational notification.

[![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![AI](https://img.shields.io/badge/AI-Risk%20Analysis-8B5CF6?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-Business%20Logic-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Telegram](https://img.shields.io/badge/Telegram-Notifications-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://telegram.org/)

![Workflow](https://img.shields.io/badge/Workflow-End--to--End%20Automation-22C55E?style=flat-square)
![Risk Management](https://img.shields.io/badge/Risk%20Management-AI%20Assisted-F59E0B?style=flat-square)
![Database](https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-22C55E?style=flat-square)
![License](https://img.shields.io/badge/License-Educational-64748B?style=flat-square)

---

## Overview

This project implements an **AI-assisted transaction optimization and risk-management pipeline using n8n**.

The workflow receives transaction data through a webhook, validates and normalizes the payload, checks for duplicate transactions, analyzes historical customer activity, calculates preliminary risk metrics, and sends the transaction to an AI analysis layer.

The resulting risk assessment is then combined with deterministic business rules to determine the appropriate processing path:

* **AUTO_APPROVE** — low-risk transactions can proceed automatically.
* **MANUAL_REVIEW** — transactions requiring additional verification are routed to a review process.
* **HOLD** — high-risk or potentially duplicated transactions are prevented from proceeding automatically.

Every transaction is logged in PostgreSQL, while relevant events can be sent to an operations or finance team through Telegram.

The architecture is intentionally designed so that **AI assists the decision process rather than acting as the sole authorization mechanism for financial operations**.

---

# Key Capabilities

* Webhook-based transaction ingestion
* Input normalization
* Transaction validation
* Unique transaction ID generation
* Duplicate transaction detection
* Customer transaction-history analysis
* Historical amount comparison
* Deterministic preliminary risk scoring
* AI-powered transaction analysis
* Structured JSON AI output
* Anomaly detection
* Duplicate probability estimation
* Transaction prioritization
* Automated decision routing
* Human-in-the-loop review
* High-risk transaction handling
* PostgreSQL transaction logging
* Telegram operational notifications
* Structured webhook responses
* Extensible API integration architecture

---

# Workflow Architecture

```text
┌──────────────────────────────┐
│          Webhook             │
│     Transaction Intake       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Normalize Transaction    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Validate Transaction     │
└──────────────┬───────────────┘
               │
          ┌────┴────┐
          │         │
        VALID     INVALID
          │         │
          ▼         ▼
┌────────────────┐  ┌──────────────┐
│ Generate ID    │  │ Error Response│
└───────┬────────┘  └──────────────┘
        │
        ▼
┌──────────────────────────────┐
│      Check Duplicate         │
│        PostgreSQL            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Customer Transaction      │
│          History             │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Calculate Risk Metrics    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      AI Transaction          │
│          Analysis            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       Parse AI Result        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Decision Engine          │
└──────────────┬───────────────┘
               │
       ┌───────┼────────┐
       │       │        │
       ▼       ▼        ▼
 AUTO_APPROVE REVIEW   HOLD
       │       │        │
       ▼       ▼        ▼
   Process   Review    Hold
     API     Queue      API
       │       │        │
       └───────┼────────┘
               │
               ▼
┌──────────────────────────────┐
│      Log Transaction         │
│        PostgreSQL            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        Notification          │
│          Telegram            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Webhook Response        │
└──────────────────────────────┘
```

---

# Project Structure

Recommended repository structure:

```text
transaction-optimization/
│
├── workflow/
│   └── transaction-optimization.json
│
├── database/
│   └── schema.sql
│
├── examples/
│   ├── low-risk.json
│   ├── medium-risk.json
│   └── high-risk.json
│
├── docs/
│   └── architecture.md
│
├── .env.example
├── .gitignore
└── README.md
```

---

# Technology Stack

| Technology                       | Role                                    |
| -------------------------------- | --------------------------------------- |
| **n8n**                          | Workflow orchestration                  |
| **PostgreSQL**                   | Transaction and historical data storage |
| **OpenRouter / OpenAI / Gemini** | AI transaction analysis                 |
| **Telegram**                     | Operational notifications               |
| **HTTP Request**                 | External transaction/API integration    |
| **JavaScript**                   | Data transformation and business logic  |
| **Webhook**                      | Transaction API entry point             |

---

# Prerequisites

Before installing the workflow, make sure you have:

* n8n
* PostgreSQL
* An AI provider API key
* Telegram Bot credentials
* Docker and Docker Compose, if using the containerized setup
* A PostgreSQL client such as `psql`, pgAdmin, or Adminer

The official PostgreSQL Docker image supports running PostgreSQL through Docker and Docker Compose.

---

# Installation

## 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/transaction-optimization.git
cd transaction-optimization
```

Replace `<your-username>` with your GitHub username.

---

## 2. Verify the Repository Structure

Run:

```bash
ls
```

You should have something similar to:

```text
workflow/
database/
examples/
docs/
.env.example
.gitignore
README.md
```

---

# PostgreSQL Setup

## Option A — Existing PostgreSQL Installation

If PostgreSQL is already installed, create a dedicated database:

```bash
sudo -u postgres psql
```

Then:

```sql
CREATE DATABASE transaction_optimization;
```

Exit:

```sql
\q
```

---

## Option B — PostgreSQL with Docker

Create a `compose.yml`:

```yaml
services:
  postgres:
    image: postgres:16
    container_name: transaction-postgres
    restart: unless-stopped
    environment:
      POSTGRES_USER: transaction_user
      POSTGRES_PASSWORD: change_this_password
      POSTGRES_DB: transaction_optimization
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

Start PostgreSQL:

```bash
docker compose up -d
```

Verify:

```bash
docker ps
```

You should see:

```text
transaction-postgres
```

Check the logs:

```bash
docker logs transaction-postgres
```

The PostgreSQL image uses environment variables such as `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB` during initial database creation.

> **Important:** Change the example database password before using this outside a local development environment.

---

# Database Schema

Create:

```text
database/schema.sql
```

Add:

```sql
CREATE TABLE IF NOT EXISTS transactions (
    id BIGSERIAL PRIMARY KEY,

    transaction_id VARCHAR(100) UNIQUE NOT NULL,

    customer_name VARCHAR(255) NOT NULL,

    customer_email VARCHAR(255) NOT NULL,

    amount NUMERIC(18,2) NOT NULL,

    currency VARCHAR(10) NOT NULL DEFAULT 'PHP',

    transaction_type VARCHAR(100),

    payment_method VARCHAR(100),

    description TEXT,

    risk_score NUMERIC(5,2),

    risk_level VARCHAR(20),

    anomaly_detected BOOLEAN DEFAULT FALSE,

    duplicate_detected BOOLEAN DEFAULT FALSE,

    priority VARCHAR(20),

    final_action VARCHAR(50),

    processing_status VARCHAR(50),

    ai_reason TEXT,

    optimization_recommendation TEXT,

    timestamp TIMESTAMPTZ NOT NULL DEFAULT NOW(),

    processed_at TIMESTAMPTZ
);
```

Create the review table:

```sql
CREATE TABLE IF NOT EXISTS transaction_reviews (
    id BIGSERIAL PRIMARY KEY,

    transaction_id VARCHAR(100) NOT NULL,

    risk_score NUMERIC(5,2),

    priority VARCHAR(20),

    reason TEXT,

    status VARCHAR(30) DEFAULT 'PENDING',

    reviewed_by VARCHAR(255),

    reviewed_at TIMESTAMPTZ,

    created_at TIMESTAMPTZ DEFAULT NOW()
);
```

Create the customer table:

```sql
CREATE TABLE IF NOT EXISTS customers (
    id BIGSERIAL PRIMARY KEY,

    customer_id VARCHAR(100),

    customer_name VARCHAR(255),

    customer_email VARCHAR(255) UNIQUE NOT NULL,

    transaction_count INTEGER DEFAULT 0,

    total_transaction_value NUMERIC(18,2) DEFAULT 0,

    average_transaction_value NUMERIC(18,2) DEFAULT 0,

    last_transaction_at TIMESTAMPTZ,

    risk_profile VARCHAR(30)
);
```

---

# Apply the Schema

For a local PostgreSQL installation:

```bash
psql \
  -U transaction_user \
  -d transaction_optimization \
  -f database/schema.sql
```

If PostgreSQL is running inside Docker:

```bash
docker exec -i transaction-postgres \
  psql -U transaction_user \
  -d transaction_optimization \
  < database/schema.sql
```

Verify:

```bash
docker exec -it transaction-postgres \
  psql -U transaction_user \
  -d transaction_optimization
```

Then:

```sql
\dt
```

You should see:

```text
customers
transaction_reviews
transactions
```

---

# n8n Setup

## 1. Start n8n

If you already have an n8n instance, open it in your browser.

For a local installation, this may be:

```text
http://localhost:5678
```

If you use another host or deployment platform, open your configured n8n URL.

---

# 2. Import the Workflow

Inside n8n:

```text
Workflows
    ↓
Import from File
    ↓
Select workflow/transaction-optimization.json
```

Alternatively, use the workflow JSON import option available in your n8n version.

After importing, the workflow should appear on the canvas.

---

# 3. Review the Nodes

The imported workflow should contain the following processing stages:

```text
Webhook
↓
Normalize Transaction
↓
Validate Transaction
↓
Transaction Valid?
↓
Generate Transaction ID
↓
Check Duplicate Transaction
↓
Analyze Duplicate
↓
Get Customer History
↓
Calculate Transaction Metrics
↓
Calculate Risk Metrics
↓
AI Transaction Analysis
↓
Parse AI Analysis
↓
Transaction Decision Engine
↓
Route Transaction
```

Then:

```text
AUTO_APPROVE
      ↓
Process Approved Transaction

MANUAL_REVIEW
      ↓
Create Review Record
      ↓
Notify Finance Team

HOLD
      ↓
Hold Transaction
      ↓
High-Risk Notification
```

Finally:

```text
        ↓
Log Transaction
        ↓
Generate Optimization Result
        ↓
Final Notification
        ↓
Respond to Webhook
```

---

# Credential Configuration

Do **not** hard-code credentials directly into Code nodes.

Create n8n credentials for each external service.

---

## PostgreSQL Credential

In n8n:

```text
Credentials
→ New Credential
→ PostgreSQL
```

Use:

```text
Host: localhost
Port: 5432
Database: transaction_optimization
User: transaction_user
Password: YOUR_DATABASE_PASSWORD
SSL: according to your deployment
```

### Docker networking

If n8n and PostgreSQL are running in the **same Docker Compose network**, do not normally use `localhost` for the PostgreSQL host.

Use the PostgreSQL service name instead:

```text
Host: postgres
Port: 5432
```

For example:

```text
postgresql://transaction_user:PASSWORD@postgres:5432/transaction_optimization
```

---

# AI Provider Configuration

The AI analysis node can use:

* OpenRouter
* OpenAI
* Google Gemini

Configure the provider according to the node used in the workflow.

The AI must return structured JSON matching:

```json
{
  "risk_score": 0,
  "risk_level": "LOW",
  "anomaly_detected": false,
  "duplicate_probability": 0,
  "priority": "NORMAL",
  "optimization_action": "AUTO_APPROVE",
  "requires_human_review": false,
  "reason": "",
  "optimization_recommendation": ""
}
```

The `Parse AI Analysis` node then converts this response into structured n8n data.

---

# Telegram Configuration

Create a Telegram bot using BotFather and obtain the bot token.

In n8n:

```text
Credentials
→ New Credential
→ Telegram
```

Configure the bot credentials.

Then configure the notification nodes with the target chat/channel.

The workflow uses Telegram for:

* Manual review alerts
* High-risk transaction alerts
* Processing notifications
* Operational status updates

---

# External Transaction API

The `Process Approved Transaction` and `Hold Transaction` nodes are designed as integration points.

Replace the placeholder HTTP requests with your actual API.

Typical structure:

```text
POST /transactions/{transaction_id}/process
```

and:

```text
POST /transactions/{transaction_id}/hold
```

Configure:

* Base URL
* Authentication
* Headers
* Request body
* Timeout
* Error handling
* Idempotency key

For development, these nodes can remain mocked.

---

# Environment Variables

Create:

```text
.env
```

from:

```text
.env.example
```

Example:

```env
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=transaction_optimization
POSTGRES_USER=transaction_user
POSTGRES_PASSWORD=change_this_password

AI_PROVIDER=openrouter
AI_API_KEY=your_api_key

TELEGRAM_BOT_TOKEN=your_bot_token

TRANSACTION_API_URL=https://example.com/api
TRANSACTION_API_KEY=your_transaction_api_key
```

### Never commit `.env`

Add this to `.gitignore`:

```gitignore
.env
.env.*
!.env.example
```

---

# Webhook Configuration

Open the:

```text
Webhook
```

node.

Set:

```text
HTTP Method: POST
```

During development, use the **Test URL**.

For example:

```text
POST https://your-n8n-instance/webhook-test/transaction
```

The exact URL is generated by your n8n instance.

Once the workflow is active, use the production webhook URL generated by n8n.

---

# Transaction Request

Send a POST request containing:

```json
{
  "customer_name": "ABC Corporation",
  "customer_email": "finance@abc.com",
  "amount": 85000,
  "currency": "PHP",
  "transaction_type": "purchase",
  "payment_method": "bank_transfer",
  "description": "Purchase of 10 laptops"
}
```

---

# Testing with cURL

```bash
curl -X POST \
  "http://localhost:5678/webhook-test/transaction" \
  -H "Content-Type: application/json" \
  -d '{
    "customer_name": "ABC Corporation",
    "customer_email": "finance@abc.com",
    "amount": 85000,
    "currency": "PHP",
    "transaction_type": "purchase",
    "payment_method": "bank_transfer",
    "description": "Purchase of 10 laptops"
  }'
```

Replace the URL with the webhook URL generated by your n8n instance.

---

# Test Scenarios

## Scenario 1 — Low Risk

```json
{
  "customer_name": "Regular Customer",
  "customer_email": "regular@example.com",
  "amount": 5000,
  "currency": "PHP",
  "transaction_type": "purchase",
  "payment_method": "bank_transfer",
  "description": "Office supplies"
}
```

Expected:

```text
Risk Level: LOW
Action: AUTO_APPROVE
```

---

## Scenario 2 — Medium Risk

```json
{
  "customer_name": "Business Customer",
  "customer_email": "business@example.com",
  "amount": 60000,
  "currency": "PHP",
  "transaction_type": "purchase",
  "payment_method": "bank_transfer",
  "description": "Large equipment purchase"
}
```

Expected:

```text
Risk Level: MEDIUM
Action: MANUAL_REVIEW
```

---

## Scenario 3 — High Risk

```json
{
  "customer_name": "Customer",
  "customer_email": "customer@example.com",
  "amount": 500000,
  "currency": "PHP",
  "transaction_type": "purchase",
  "payment_method": "bank_transfer",
  "description": "Unusually large transaction"
}
```

Expected:

```text
Risk Level: HIGH
Action: HOLD
```

> These are test scenarios, not guarantees. The actual result depends on transaction history, deterministic rules, AI output, and the final decision-engine logic.

---

# Duplicate Transaction Test

Submit the same transaction multiple times.

Example:

```json
{
  "customer_name": "ABC Corporation",
  "customer_email": "finance@abc.com",
  "amount": 85000,
  "currency": "PHP",
  "transaction_type": "purchase",
  "payment_method": "bank_transfer",
  "description": "Purchase of 10 laptops"
}
```

The duplicate-detection query should identify matching recent transaction characteristics.

The decision engine should route the transaction toward:

```text
DUPLICATE
    ↓
HOLD
    ↓
REVIEW
```

---

# Expected API Response

A successful workflow can return:

```json
{
  "success": true,
  "transaction_id": "TX-1755768625123-A81F42BC",
  "status": "OPTIMIZED",
  "action": "AUTO_APPROVE",
  "risk_score": 18,
  "risk_level": "LOW",
  "priority": "NORMAL",
  "requires_human_review": false
}
```

---

# Risk Decision Model

The workflow uses both **deterministic rules and AI analysis**.

```text
                 Transaction
                      │
                      ▼
             Deterministic Rules
                      │
                      ▼
              Preliminary Risk
                      │
                      ▼
                  AI Analysis
                      │
                      ▼
             Decision Engine
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       LOW RISK    REVIEW       HIGH RISK
          │           │           │
          ▼           ▼           ▼
     AUTO_APPROVE  MANUAL       HOLD
```

This layered approach reduces dependence on an AI model for critical transaction decisions.

---

# Error Handling

The workflow should account for:

### Invalid Input

```text
Missing fields
Invalid amount
Invalid email
Invalid transaction type
```

### Database Errors

```text
Connection failure
Query failure
Timeout
Constraint violation
```

### AI Errors

```text
API failure
Timeout
Invalid JSON
Unexpected response
Rate limit
```

### External API Errors

```text
401 Unauthorized
403 Forbidden
404 Not Found
429 Rate Limited
500 Server Error
```

### Recommended Production Pattern

```text
Main Workflow
      │
      ├── Success
      │
      └── Error
             ↓
       Error Workflow
             ↓
       Log Error
             ↓
       Notify Admin
```

---

# Security

This repository is intended for development and portfolio demonstration.

Before processing real financial transactions, implement:

* API authentication
* Request signing
* Authorization
* HTTPS
* Input validation
* Rate limiting
* Idempotency
* Audit logging
* Transaction limits
* Role-based approvals
* Secret management
* Database access controls
* Monitoring
* Alerting
* Backup and recovery
* Compliance requirements applicable to your deployment

**Do not allow an AI model to independently authorize unrestricted movement of real funds.**

The AI layer should provide analysis and recommendations, while deterministic controls and appropriate authorization remain responsible for final execution.

---

# Performance Optimization

The workflow is designed to optimize processing by automatically separating transactions into different paths.

### Low-risk transactions

```text
Transaction
→ Validate
→ Analyze
→ Auto-process
```

### Uncertain transactions

```text
Transaction
→ Analyze
→ Human Review
```

### High-risk transactions

```text
Transaction
→ Detect Risk
→ Hold
→ Notify
```

This prevents every transaction from requiring the same level of manual processing.

---

# Monitoring

Monitor the following metrics:

| Metric                  | Purpose                    |
| ----------------------- | -------------------------- |
| Total transactions      | Overall transaction volume |
| Auto-approved           | Automation effectiveness   |
| Manual reviews          | Human intervention rate    |
| Held transactions       | Risk-control activity      |
| Duplicate transactions  | Duplicate detection        |
| Average risk score      | Risk distribution          |
| AI failures             | AI reliability             |
| Processing failures     | System reliability         |
| Average processing time | Workflow performance       |

These metrics can later be connected to a dashboard using tools such as Grafana, Metabase, or a custom web dashboard.

---

# Future Improvements

Planned extensions include:

* Real-time anomaly detection
* Customer risk profiles
* Transaction velocity monitoring
* Geographic anomaly detection
* Device fingerprint analysis
* Machine-learning models
* Dynamic transaction thresholds
* Approval dashboards
* Role-based review assignment
* SLA monitoring
* Automatic retry logic
* Transaction analytics
* Cost optimization
* Processing-time optimization
* Fraud detection
* Audit dashboards
* Human approval interface

---

# Troubleshooting

## PostgreSQL Connection Failed

Check:

```bash
docker ps
```

Then:

```bash
docker logs transaction-postgres
```

Verify:

```text
Host
Port
Database
Username
Password
```

If n8n and PostgreSQL are in separate containers, make sure they share a Docker network.

---

## AI JSON Parsing Failed

Check the output from:

```text
AI Transaction Analysis
```

The response must be valid JSON.

The expected structure is:

```json
{
  "risk_score": 0,
  "risk_level": "LOW",
  "anomaly_detected": false,
  "duplicate_probability": 0,
  "priority": "NORMAL",
  "optimization_action": "AUTO_APPROVE",
  "requires_human_review": false,
  "reason": "",
  "optimization_recommendation": ""
}
```

Do not allow the AI node to return Markdown code fences if the parser expects raw JSON.

---

## Webhook Not Triggering

Check:

1. The workflow is active when using the production webhook.
2. The HTTP method is `POST`.
3. The correct webhook URL is being used.
4. The request uses `Content-Type: application/json`.
5. The n8n instance is accessible from the client sending the request.

---

## Telegram Notification Failed

Verify:

```text
Bot Token
Chat ID
Bot permissions
Telegram credentials
```

Also make sure the bot has access to the destination chat/channel.

---

# Development Roadmap

### Phase 1 — Core Transaction Pipeline

* [x] Webhook intake
* [x] Data normalization
* [x] Validation
* [x] Transaction ID generation
* [x] PostgreSQL integration

### Phase 2 — Risk Intelligence

* [x] Duplicate detection
* [x] Historical analysis
* [x] Preliminary risk scoring
* [x] AI transaction analysis
* [x] Structured AI output

### Phase 3 — Automated Decision Making

* [x] Auto-approval routing
* [x] Manual review routing
* [x] High-risk hold routing
* [x] Transaction logging
* [x] Notifications

### Phase 4 — Advanced Optimization

* [ ] Real-time anomaly detection
* [ ] Customer risk profiles
* [ ] Transaction velocity analysis
* [ ] Analytics dashboard
* [ ] Automated review assignment
* [ ] Machine-learning risk model
* [ ] Production payment API integration

---

# Files

| File                                     | Description                   |
| ---------------------------------------- | ----------------------------- |
| `workflow/transaction-optimization.json` | n8n workflow                  |
| `database/schema.sql`                    | PostgreSQL database schema    |
| `examples/low-risk.json`                 | Low-risk test payload         |
| `examples/medium-risk.json`              | Medium-risk test payload      |
| `examples/high-risk.json`                | High-risk test payload        |
| `docs/architecture.md`                   | Architecture documentation    |
| `.env.example`                           | Environment variable template |
| `.gitignore`                             | Git exclusions                |
| `README.md`                              | Project documentation         |

---

# Important Disclaimer

This project is an **automation and AI decision-support demonstration**.

It is not a production-ready financial system or fraud-detection solution by default. Risk scores and AI classifications are illustrative and should not be treated as definitive financial, compliance, or fraud determinations.

For production use, integrate the workflow with appropriate security, authorization, audit, compliance, monitoring, and financial-control mechanisms.

---

# License

This project is available for educational, portfolio, and development purposes.

Add an appropriate open-source license to the repository if you intend to permit redistribution or modification.
