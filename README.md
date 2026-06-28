<div align="center">

<br/>

<img src="https://img.shields.io/badge/Aletheia-AI%20Reliability%20Platform-6366f1?style=for-the-badge&labelColor=0f0f0f" alt="Aletheia"/>

<h1>Aletheia</h1>

<h3>Trace. Evaluate. Guard. Ship reliably.</h3>

<p>
An AI Reliability, Evaluation, Monitoring &amp; Observability platform for engineering teams who want to catch LLM regressions <em>before</em> their users do.
</p>

<br/>

<p>
  <img alt="Version" src="https://img.shields.io/badge/version-3.192.2-6366f1?style=flat-square">
  <img alt="Node" src="https://img.shields.io/badge/node-24-339933?style=flat-square&logo=node.js&logoColor=white">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-22c55e?style=flat-square">
  <img alt="Status" src="https://img.shields.io/badge/status-portfolio%20project-f59e0b?style=flat-square">
  <img alt="pnpm" src="https://img.shields.io/badge/package_manager-pnpm-f97316?style=flat-square&logo=pnpm&logoColor=white">
</p>

<p>
  <img alt="Next.js" src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white">
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white">
  <img alt="ClickHouse" src="https://img.shields.io/badge/ClickHouse-FFCC00?style=flat-square&logo=clickhouse&logoColor=black">
  <img alt="Redis" src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white">
</p>

<br/>

<p>
  <a href="#-overview"><strong>Overview</strong></a> ·
  <a href="#-features"><strong>Features</strong></a> ·
  <a href="#-architecture"><strong>Architecture</strong></a> ·
  <a href="#-monorepo-structure"><strong>Structure</strong></a> ·
  <a href="#-getting-started"><strong>Quickstart</strong></a> ·
  <a href="#-deployment"><strong>Deploy</strong></a> ·
  <a href="#-engineering-highlights"><strong>Engineering</strong></a>
</p>

<br/>

> **Provenance Note:** Aletheia is a customized, rebranded, and extended derivative of [Langfuse](https://github.com/langfuse/langfuse) (MIT). It is **not** the official Langfuse project and is not affiliated with its maintainers. New features (guardrails, regression diffing, reliability workflows) and the full platform transformation were independently designed and implemented. See [Acknowledgements](#-acknowledgements).

</div>

---

## 📖 Overview

As LLM-powered applications move from prototypes to production, teams run into the same recurring problems:

- Prompts **drift silently** between versions
- Retrieval pipelines **fail without warning**
- Model outputs **regress** after a "minor" model swap
- There's **no structured way to catch** any of it before users do

Aletheia closes that gap. It gives engineering teams a single platform to:

| | |
|---|---|
| 👁️ **See** | What your LLM application is actually doing — call by call, session by session |
| 📏 **Measure** | Output quality with automated and human-in-the-loop evaluation |
| 🚨 **Catch regressions** | Before they ship, by diffing behavior across prompt, model, or code changes |
| 🛡️ **Enforce reliability** | At runtime with guardrails that intercept unsafe or malformed outputs |

The platform is built around one core idea: **LLM reliability is a continuous workflow**, not a one-time check.

---

## ✨ Features

### 🔍 Observability

<table>
<tr>
<td width="50%">

**LLM Tracing**

Full request/response capture for every LLM call — including nested spans for retrieval, embedding, tool calls, and agent steps. Visualize entire execution trees with latency, token usage, and cost breakdowns per node.

</td>
<td width="50%">

**Session Analytics**

Aggregate multi-turn conversations into sessions. Analyze user journeys, drop-off points, and conversational quality trends over time — not just individual calls.

</td>
</tr>
<tr>
<td width="50%">

**User Analytics**

Per-user breakdowns of usage, cost, latency, and quality scores. Identify high-friction users, cost drivers, and power users at a glance.

</td>
<td width="50%">

**Monitoring Dashboards**

Real-time charts for latency percentiles, token consumption, error rates, and cost. Drill down from aggregate trends into individual traces in one click.

</td>
</tr>
</table>

---

### 🧪 Quality & Evaluation

<table>
<tr>
<td width="33%">

**Prompt Management**

Centralized, version-controlled prompt storage with rollback and environment-based deployment. Fully decoupled from application code.

</td>
<td width="33%">

**Playground**

Interactive sandbox to iterate on prompts and model parameters directly against traced production examples. Compare outputs live.

</td>
<td width="33%">

**Evaluators**

Pluggable evaluation pipeline supporting LLM-as-a-judge scoring, deterministic code-based checks, and custom scoring functions.

</td>
</tr>
<tr>
<td width="33%">

**Human Annotation**

Manual labeling workflows for building ground-truth datasets and auditing model behavior.

</td>
<td width="33%">

**Datasets**

Curated test sets built from production traces, decoupled from live data. Used as the benchmark for all experiment runs.

</td>
<td width="33%">

**Experiments**

Structured runs comparing outputs across prompt/model variants against a fixed dataset, with visual score and latency breakdowns.

</td>
</tr>
</table>

---

### 🛡️ Reliability Engineering *(New in Aletheia)*

<table>
<tr>
<td width="33%">

**Guardrails** 🆕

A request-time sidecar proxy intercepting LLM inputs and outputs and applying configurable policies — schema validation, PII detection, blocklist filtering, moderation checks — without modifying application code.

</td>
<td width="33%">

**Regression Diffing** 🆕

Side-by-side comparison of evaluation results across two versions of a prompt, model, or pipeline. Surfaces behavioral drift before any deployment.

</td>
<td width="33%">

**Reliability Workflows** 🆕

Pre-deployment checklists that tie tracing, evaluation, and guardrail results into a single pass/fail signal. Powered by BullMQ worker queues.

</td>
</tr>
</table>

---

## 🏗️ Architecture

### System Architecture

How your LLM app, the ingestion API, guardrail proxy, databases, and web dashboard connect:

![Aletheia system architecture](assets/architecture.svg)

---

### Reliability Workflow

Every release moves through this loop before reaching production:

![Aletheia reliability loop](assets/reliability-loop.svg)

---

### Guardrail Pipeline

How the guardrail sidecar intercepts and validates requests — zero changes to your application code:

![Aletheia guardrail pipeline](assets/guardrail.svg)

---

### Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Next.js 14, React, TypeScript, Tailwind CSS |
| **Backend API** | Node.js, tRPC, REST |
| **Primary DB** | PostgreSQL + Prisma ORM |
| **Analytics DB** | ClickHouse (columnar, high-cardinality event storage) |
| **Queue / Jobs** | Redis + BullMQ |
| **Object Storage** | S3-compatible (MinIO for local / any S3 provider in prod) |
| **Guardrail Proxy** | Express.js sidecar (TypeScript, Zod validation) |
| **Package Manager** | pnpm + Turborepo monorepo |
| **Containerization** | Docker + Docker Compose |

---

### Architecture Principles

Aletheia is architected around **wide, richly-attributed events** rather than fragmented metrics + logs + traces:

- **Observations are the primary unit** — traces are correlation handles, not the only entry point
- **High-cardinality context preserved** — filter and debug unknown unknowns without predefining every query
- **Columnar-first** for analytics (ClickHouse): narrow field selection, time-bounded scans, useful ordering keys
- **Immutable / append-oriented** event records for high-volume telemetry
- **Compact query representations** for lists and dashboards; raw payloads fetched only on detail views

---

## 📦 Monorepo Structure

```
aletheia/
├── web/                     # Next.js app — UI, tRPC, public REST API
├── worker/                  # BullMQ queue consumers & background jobs
├── packages/
│   ├── shared/              # Domain models, DB schema, queue contracts, repositories
│   ├── guardrail/           # @aletheia/guardrail — Express sidecar proxy
│   ├── aletheia/            # @aletheia/aletheia — JS/TS SDK for instrumentation
│   ├── aletheia-core/       # Core SDK primitives
│   ├── aletheia-langchain/  # LangChain integration
│   └── config-*/            # Shared ESLint / TypeScript configs
├── ee/                      # Enterprise feature package (consumed by web)
├── fern/                    # API definition sources (OpenAPI / Fern)
├── generated/               # Generated API clients (do not hand-edit)
├── scripts/                 # Repo tooling scripts
├── .agents/                 # Agent config (AGENTS.md, skills, MCP config)
├── docker-compose.yml       # Production compose
└── docker-compose.dev.yml   # Local dev compose
```

**Dependency direction:**
```
web ──────────────────────┐
worker ───────────────────┤──▶ @aletheia/shared ──▶ (no internal imports)
@aletheia/ee ─────────────┘
```

---

## 🚀 Getting Started

### Prerequisites

| Tool | Version |
|---|---|
| Node.js | `24` |
| pnpm | latest |
| Docker + Docker Compose | any recent version |

---

### Local Development (Docker — recommended)

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/aletheia.git
cd aletheia

# 2. Install dependencies
pnpm install

# 3. Copy environment config
cp .env.example .env
# Fill in secrets (see comments marked # CHANGEME)

# 4. Full dev reset + seed
pnpm run dx
```

The app will be available at **http://localhost:3000**.

> `pnpm run dx` installs deps → prunes + starts Docker infra → resets databases → seeds example data → starts the dev server across all packages.

---

### Individual Commands

```bash
pnpm run infra:dev:up      # start Postgres, ClickHouse, Redis, MinIO
pnpm run dev               # dev server (web + worker)
pnpm run dev:web           # web only
pnpm run dev:worker        # worker only
pnpm run db:migrate        # run database migrations
pnpm run db:seed:examples  # seed example data
pnpm run typecheck         # typecheck all packages
pnpm run test              # run all tests
pnpm run lint              # lint all packages
```

---

### Key Environment Variables

```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/postgres
NEXTAUTH_URL=http://localhost:3000
SALT=<random string>
ENCRYPTION_KEY=<openssl rand -hex 32>

CLICKHOUSE_URL=http://localhost:8123
CLICKHOUSE_USER=clickhouse
CLICKHOUSE_PASSWORD=<your password>

ALETHEIA_S3_EVENT_UPLOAD_BUCKET=aletheia
ALETHEIA_S3_EVENT_UPLOAD_ENDPOINT=http://localhost:9000
ALETHEIA_S3_EVENT_UPLOAD_ACCESS_KEY_ID=minio
ALETHEIA_S3_EVENT_UPLOAD_SECRET_ACCESS_KEY=miniosecret
```

---

## 🐳 Deployment

### Docker Compose (recommended)

```bash
docker compose up -d
```

Services:
- `aletheia-web` — Next.js web app (port `3000`)
- `aletheia-worker` — BullMQ background worker (port `3030`)
- `postgres`, `clickhouse`, `redis`, `minio`

### Compose Variants

| File | Use Case |
|---|---|
| `docker-compose.yml` | Standard production |
| `docker-compose.dev.yml` | Local development |
| `docker-compose.build.yml` | Production with local build |
| `docker-compose.dev-azure.yml` | Azure Blob Storage variant |
| `docker-compose.dev-redis-cluster.yml` | Redis Cluster variant |

### Manual Deploy

```bash
pnpm install
pnpm run build
pnpm --filter=shared run db:migrate
pnpm run start
```

> **Single-tenant only.** All multi-tenant SaaS billing, plan-gating, and usage-metering code has been removed.

---

## 🛠️ Engineering Highlights

### What Was Built (New in Aletheia)

**Guardrail Sidecar Proxy** (`packages/guardrail/`)

A TypeScript Express.js proxy that intercepts LLM requests and responses at runtime and applies configurable policies — Zod schema validation, PII detection, blocklist/allowlist filtering, moderation checks — without requiring changes to application code.

**Regression Diffing Engine**

Side-by-side comparison of evaluation outputs and scores across two prompt/model/pipeline versions against the same dataset. Surfaces behavioral drift — score deltas, semantic output changes — as a structured diff view.

**Reliability Workflows**

Pre-deployment checklists powered by BullMQ worker queues. Ties tracing, evaluation scoring, and guardrail results into a single automated pass/fail signal before a prompt or model change merges.

**Platform Transformation**

- Removed all billing, subscription, plan-gating, and usage-metering subsystems
- Stripped multi-tenant SaaS onboarding flows, upgrade prompts, and external telemetry
- Rebuilt navigation around the develop → trace → evaluate → guard → diff → ship workflow
- Full rebrand: UI strings, color system, logos, metadata
- Hardened ingestion and evaluation API error handling for malformed/partial trace payloads

---

### Technical Skills Demonstrated

| Skill | Applied |
|---|---|
| **Full Stack** | Next.js/React/TypeScript frontend + Node.js backend + dual-database persistence |
| **AI Infrastructure** | Guardrail sidecar for runtime LLM request/response interception |
| **Observability Systems** | Distributed tracing (spans, nested observations, session aggregation) applied to LLM call graphs |
| **Columnar DB Design** | ClickHouse schema for wide-event observability (high-cardinality, time-bounded, append-oriented) |
| **Relational DB Design** | Extended Prisma/PostgreSQL schema for evaluation and regression-diffing data models |
| **API Development** | tRPC + REST ingestion and evaluation APIs with defensive error handling |
| **Queue Architecture** | BullMQ + Redis async job orchestration for parallel evaluation runs |
| **System Design** | Re-architected multi-tenant SaaS platform into a focused single-tenant reliability tool |
| **Monorepo Engineering** | pnpm + Turborepo workspace with strict dependency direction and shared configs |

---

## 🔌 SDK Usage

```typescript
import Aletheia from "@aletheia/aletheia";

const aletheia = new Aletheia({
  publicKey: "pk-...",
  secretKey: "sk-...",
  baseUrl: "http://localhost:3000",
});

const trace = aletheia.trace({ name: "my-llm-call", userId: "user-123" });

const generation = trace.generation({
  name: "openai-completion",
  model: "gpt-4o",
  input: messages,
});

// ... call your LLM provider ...

generation.end({ output: response, usage: { promptTokens: 100, completionTokens: 50 } });
```

**LangChain integration:**

```typescript
import { AletheiaCallbackHandler } from "@aletheia/aletheia-langchain";

const handler = new AletheiaCallbackHandler();
const chain = new LLMChain({ llm, prompt, callbacks: [handler] });
```

---

## 🤝 Acknowledgements

Aletheia is built on top of [Langfuse](https://github.com/langfuse/langfuse) (MIT), an open-source LLM engineering platform. The original codebase provided the foundational tracing pipeline, data model, and UI scaffolding.

The following are my own work: guardrail sidecar proxy, regression diffing engine, reliability workflow restructuring, full platform transformation (billing removal, rebrand, SaaS cleanup), and architecture hardening.

Not affiliated with, endorsed by, or representative of Langfuse or its maintainers.

---

## 📄 License

Derived from [Langfuse](https://github.com/langfuse/langfuse), licensed under the MIT License.

```
Original copyright: Copyright (c) 2022–2026 Langfuse GmbH
Modifications for Aletheia: Copyright (c) 2026 Jayanth
```

See [LICENSE](LICENSE) for the full MIT License text.

---

<div align="center">

<br/>

**Aletheia** — AI Reliability Engineering, from trace to ship.

<img alt="Made with care" src="https://img.shields.io/badge/made%20with-care-ff69b4?style=flat-square">
<img alt="Reliability first" src="https://img.shields.io/badge/philosophy-reliability%20first-6366f1?style=flat-square">
<img alt="Self hosted" src="https://img.shields.io/badge/deployment-self--hosted-22c55e?style=flat-square">

<br/><br/>

<sub>Portfolio project by Jayanth · Not affiliated with Langfuse</sub>

</div>
