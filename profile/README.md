<div align="center">

# ⚙️ Blackbox Enterprises

### Enterprise Automation. Production Ready.

The full enterprise automation stack — workflow orchestration, AI routing, ETL pipelines, and payments — for teams that ship at scale.

[![Platform](https://img.shields.io/badge/Platform-blackroad.io-FF1D6C?style=for-the-badge)](https://blackroad.io)
[![npm](https://img.shields.io/badge/npm-packages-CB3837?style=for-the-badge&logo=npm&logoColor=white)](https://www.npmjs.com/org/blackroad)
[![Stripe](https://img.shields.io/badge/Payments-Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://blackroad.io/pricing)
[![Agents](https://img.shields.io/badge/AI_Agents-30%2C000-9C27B0?style=for-the-badge)](https://agents.blackroad.io)
[![Status](https://img.shields.io/badge/Status-Production-44FF44?style=for-the-badge)](https://status.blackroad.io)
[![Cost](https://img.shields.io/badge/AI_Cost-%240-F5A623?style=for-the-badge)](https://blackroad.io)

</div>

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Products & Services](#products--services)
3. [npm Packages](#npm-packages)
4. [Payments & Stripe](#payments--stripe)
5. [Organizations](#organizations)
6. [Quick Start](#quick-start)
7. [Architecture](#architecture)
8. [Contributing](#contributing)
9. [Security](#security)
10. [Links](#links)

---

## Overview

**Blackbox Enterprises** is the enterprise division of [BlackRoad OS](https://blackroad.io) — a platform-as-a-service built on a single core principle:

> **Intelligence is already trained. We route to the right tool at the right time.**

We connect enterprises to the full automation stack: n8n, Airbyte, Prefect, Temporal, 30,000 AI agents, and a proprietary routing layer that costs **$0 in AI inference** by leveraging existing models (Claude, GPT, Llama, and local Hailo-8 inference).

**By the numbers:**
- 🤖 30,000 AI Agents deployed
- 🏢 17 GitHub Organizations
- 📦 1,800+ Repositories
- 💰 $0 AI Cost (routing-based, not model-based)
- ⚡ 26 TOPS local inference (Hailo-8)

---

## Products & Services

| Product | Description | Status |
|---------|-------------|--------|
| **BlackRoad Operator** | Core AI routing engine — routes any request to the right tool | ✅ Production |
| **Agent Fleet** | 30,000 managed AI agents for enterprise workflows | ✅ Production |
| **Workflow Automation** | n8n-powered no-code/low-code automation pipelines | ✅ Production |
| **ETL Pipelines** | Airbyte + Prefect data orchestration | ✅ Production |
| **AI Routing API** | REST API for intelligent request routing | ✅ Production |
| **BlackRoad SDK** | npm package suite for rapid integration | ✅ Production |

**Focus Areas:** `Workflow Automation` • `ETL` • `AI Orchestration` • `No-Code` • `Enterprise APIs` • `Edge Inference`

---

## npm Packages

Install the BlackRoad SDK to integrate enterprise automation into your Node.js or TypeScript projects:

```bash
# Core SDK
npm install @blackroad/sdk

# AI routing client
npm install @blackroad/operator

# Workflow automation helpers
npm install @blackroad/workflows

# Agent management
npm install @blackroad/agents
```

**Quick example:**

```js
import { BlackRoadOperator } from '@blackroad/operator';

const operator = new BlackRoadOperator({ apiKey: process.env.BLACKROAD_API_KEY });

const result = await operator.route({
  query: 'Summarize the latest sales report',
  context: { userId: 'user_123' }
});

console.log(result.answer);
```

📦 Browse all packages: [npmjs.com/org/blackroad](https://www.npmjs.com/org/blackroad)

---

## Payments & Stripe

Blackbox Enterprises uses **Stripe** for all billing and subscription management. Our pricing is usage-based and transparent.

### Plans

| Plan | Price | Agents | API Calls/mo | Support |
|------|-------|--------|--------------|---------|
| **Starter** | $49/mo | 10 | 100,000 | Community |
| **Growth** | $299/mo | 100 | 1,000,000 | Email |
| **Enterprise** | $999/mo | Unlimited | Unlimited | Dedicated |
| **Custom** | Contact us | Unlimited | Unlimited | SLA |

### Stripe Integration

```bash
npm install @blackroad/billing
```

```js
import { BlackRoadBilling } from '@blackroad/billing';

const billing = new BlackRoadBilling({
  stripePublishableKey: process.env.STRIPE_PUBLISHABLE_KEY
});

// Create a checkout session
const session = await billing.createCheckoutSession({
  plan: 'growth',
  successUrl: 'https://yourapp.com/success',
  cancelUrl: 'https://yourapp.com/cancel'
});
```

💳 Manage billing: [blackroad.io/billing](https://blackroad.io/billing)
📄 Pricing details: [blackroad.io/pricing](https://blackroad.io/pricing)

---

## Organizations

BlackRoad operates across 17 specialized GitHub organizations. Each owns a distinct layer of the stack:

| Organization | Focus | Key Repos |
|-------------|-------|-----------|
| [**BlackRoad-OS**](https://github.com/BlackRoad-OS) | Core OS, operator, infrastructure | operator, kernel, cli |
| [**BlackRoad-AI**](https://github.com/BlackRoad-AI) | AI models, routing, inference | router, hailo-bridge, llm-proxy |
| [**BlackRoad-Cloud**](https://github.com/BlackRoad-Cloud) | Cloud services, deployment | deploy, k8s, terraform |
| [**BlackRoad-Labs**](https://github.com/BlackRoad-Labs) | Research, experiments | experiments, benchmarks |
| [**BlackRoad-Security**](https://github.com/BlackRoad-Security) | Security tools, auditing | audit, scanner, vault |
| [**BlackRoad-Foundation**](https://github.com/BlackRoad-Foundation) | CRM, business tools | crm-sync, salesforce-bridge |
| [**BlackRoad-Media**](https://github.com/BlackRoad-Media) | Content, publishing | cms, media-pipeline |
| [**BlackRoad-Hardware**](https://github.com/BlackRoad-Hardware) | IoT, ESP32, Pi projects | pi-fleet, esp32-edge |
| [**BlackRoad-Education**](https://github.com/BlackRoad-Education) | Learning, documentation | docs, tutorials |
| [**BlackRoad-Gov**](https://github.com/BlackRoad-Gov) | Governance, voting | governance, voting |
| [**BlackRoad-Interactive**](https://github.com/BlackRoad-Interactive) | Games, 3D, metaverse | game-engine, 3d-tools |
| [**BlackRoad-Archive**](https://github.com/BlackRoad-Archive) | Storage, backup | archive, cold-storage |
| [**BlackRoad-Studio**](https://github.com/BlackRoad-Studio) | Design, creative tools | design-system, studio |
| [**BlackRoad-Ventures**](https://github.com/BlackRoad-Ventures) | Business, commerce | commerce, marketplace |
| [**Blackbox-Enterprises**](https://github.com/Blackbox-Enterprises) | Enterprise solutions | .github, enterprise-sdk |

---

## Quick Start

### 1. Get an API Key

Sign up at [blackroad.io](https://blackroad.io) and generate an API key from your dashboard.

### 2. Install the SDK

```bash
npm install @blackroad/sdk
```

### 3. Make your first request

```js
import { BlackRoad } from '@blackroad/sdk';

const client = new BlackRoad({ apiKey: process.env.BLACKROAD_API_KEY });

// Route a request to the best available AI/tool
const response = await client.operator.route('What is the boiling point of water?');
console.log(response.answer); // Routes to NumPy/SciPy or cached result

// Trigger a workflow
await client.workflows.trigger('onboarding-flow', { userId: 'user_456' });

// List running agents
const agents = await client.agents.list({ status: 'active' });
```

### 4. Subscribe via Stripe

```bash
npm install @blackroad/billing
```

```js
const session = await client.billing.checkout({ plan: 'starter' });
// Redirect user to session.url for Stripe checkout
```

📖 Full documentation: [docs.blackroad.io](https://docs.blackroad.io)

---

## Architecture

BlackRoad is built on the **Operator pattern** — a routing layer that sits between users and every available tool or intelligence:

```
[User Request] → [Operator] → [Route to Right Tool] → [Answer]
                     │
                     ├── Physics question?   → NumPy/SciPy
                     ├── Language task?      → Claude/GPT API
                     ├── Customer lookup?    → Salesforce API
                     ├── Legal question?     → Legal database
                     └── Fast inference?     → Hailo-8 local (26 TOPS)
```

**Infrastructure cost: ~$40/month** — Cloudflare edge, Salesforce free tier, GitHub Enterprise, Tailscale mesh, Digital Ocean gateway, and an owned Raspberry Pi cluster.

→ Full architecture: [BLACKROAD_ARCHITECTURE.md](../BLACKROAD_ARCHITECTURE.md)

---

## Contributing

We welcome contributions across all organizations. Before you start:

1. Read the [Architecture Overview](../BLACKROAD_ARCHITECTURE.md)
2. Review our [Contributing Guidelines](../CONTRIBUTING.md)
3. Check open issues labeled `good first issue` or `help wanted`
4. Open an issue to discuss significant changes before coding

**Branch naming:** `feature/*` • `fix/*` • `docs/*` • `claude/*`

---

## Security

Security vulnerabilities should **never** be reported in public issues.

📧 Email: **security@blackroad.io**

Response SLA: acknowledgment within 48 hours, assessment within 5 business days.

→ Full policy: [SECURITY.md](../SECURITY.md)

---

## Links

| Resource | URL |
|----------|-----|
| 🌐 **Website** | [blackroad.io](https://blackroad.io) |
| 🏢 **Enterprise** | [blackbox-enterprises.github.io](https://blackbox-enterprises.github.io) |
| 📖 **Documentation** | [docs.blackroad.io](https://docs.blackroad.io) |
| 📦 **npm Packages** | [npmjs.com/org/blackroad](https://www.npmjs.com/org/blackroad) |
| 💳 **Pricing / Stripe** | [blackroad.io/pricing](https://blackroad.io/pricing) |
| 💬 **Status** | [status.blackroad.io](https://status.blackroad.io) |
| 🤖 **Agents** | [agents.blackroad.io](https://agents.blackroad.io) |
| 🔒 **Security** | security@blackroad.io |

---

<div align="center">

**Part of [BlackRoad OS](https://blackroad.io)** — 30,000 AI Agents • 17 Organizations • 1,800+ Repos • $0 AI Cost

*© BlackRoad OS, Inc. All rights reserved.*

</div>
