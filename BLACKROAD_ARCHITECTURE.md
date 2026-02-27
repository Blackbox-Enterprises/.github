# BlackRoad Architecture Overview

> **The Core Thesis:** BlackRoad is a routing company, not an AI company.

---

## Executive Summary

We don't train models or buy GPUs. We connect users to intelligence that already exists (Claude, GPT, Llama, NumPy, legal databases, etc.) through an orchestration layer we own.

**The insight:** Intelligence is already trained. Libraries already exist. The value is in routing requests to the right tool at the right time—not in building another brain.

Central to this architecture is the deployment of autonomous routing matrices—specifically **@BlackRoadBot** and **@blackroad-agents**—which facilitate the distribution of high-level intent across cloud platforms, local hardware clusters, and organizational structures.

---

## Infrastructure (~$40/month recurring)

| Layer | Service | Role |
|-------|---------|------|
| Edge/CDN | Cloudflare | Handles millions of connections, DNS, DDoS, Tunnels |
| CRM/Data | Salesforce (Free Dev Edition) | Customer data, 15K API calls/day |
| Code/CI | GitHub Enterprise | 15 organizations, deployment |
| Mesh Network | Tailscale | Private encrypted connections between nodes |
| Cloud Node | Digital Ocean (Shellfish) | Internet-facing server |

---

## Hardware (Owned, Not Rented)

A Raspberry Pi cluster running specialized roles:

| Node | Hardware | Role |
|------|----------|------|
| **lucidia** | Pi 5 + Pironman + Hailo-8 | Salesforce sync, RoadChain/Bitcoin |
| **octavia** | Pi 5 + Pironman + Hailo-8 | AI routing decisions (26 TOPS), 3D printing |
| **aria** | Pi 5 | Agent orchestration, Cloudflare Workers |
| **alice** | Pi 400 | Kubernetes + VPN hub (mesh root) |
| **shellfish** | Digital Ocean droplet | Public-facing gateway |

Plus dev machines (Mac = "cecilia", iPhone = "arcadia") and edge devices (ESP32s, LoRa modules for future deployment).

### Local Inference via Raspberry Pi 5 Clusters

The system utilizes clusters of Raspberry Pi 5 nodes to host local Large Language Models (LLMs). These models serve as the reasoning engine for the @blackroad-agents scaffold, replacing centralized API calls with local, private inference.

| Component | Technical Specification | Functional Role |
|-----------|------------------------|-----------------|
| Compute Node | Raspberry Pi 5 (8GB LPDDR4X) | General Purpose Inference and Control |
| Inference Accelerator | Hailo-based NPU (Hailo-8: 26 TOPS per node; optional Raspberry Pi AI Hat 2 / Hailo 10H: 40 TOPS) | Dedicated INT8 LLM Processing |
| Network Layer | Gigabit Ethernet with PoE+ HAT | Synchronized Node Communication |
| Storage | NVMe SSD (M.2 Interface, 256GB+) | Model Weights and Agent Memory |
| Software Stack | LiteLLM Proxy / Ollama / llama.cpp | API Hosting and Load Balancing |

The cluster currently uses Hailo-8 accelerators (26 TOPS per node) on the lucidia and octavia Pi 5s. Nodes can optionally be upgraded to the Raspberry Pi AI Hat 2, featuring the Hailo 10H NPU (40 TOPS), which allows for efficient processing of quantized GGUF models, achieving 5–15 tokens per second in clustered configurations using OpenMPI for parallelization.

### Proxy Configuration for Copilot Offloading

To achieve seamless offloading, the system environment is configured to override the default GitHub Copilot endpoints:

```bash
export GH_COPILOT_OVERRIDE_PROXY_URL="http://raspberrypi.local:4000"
```

The LiteLLM proxy translates requests into an OpenAI-compatible format and distributes them across the cluster using a round-robin load-balancing strategy. This bypasses external rate limits and ensures that proprietary codebase context never leaves the local BlackRoad network.

---

## The Control Plane

```
┌─────────────────────────────────────────────────────────────┐
│              BLACKROAD UNIFIED CONTROL                       │
├─────────────────┬─────────────────┬─────────────────────────┤
│   SALESFORCE    │   CLOUDFLARE    │      GITHUB             │
│   CRM + API     │   Edge + DNS    │    Code + CI            │
└────────┬────────┴────────┬────────┴──────────┬──────────────┘
         │                 │                   │
         └────────────────┬┴───────────────────┘
                          ▼
                    ┌──────────┐
                    │ OPERATOR │  ← We own this
                    └────┬─────┘
         ┌───────────────┼───────────────┐
         ▼               ▼               ▼
    ┌─────────┐    ┌──────────┐    ┌─────────┐
    │ lucidia │    │ octavia  │    │  aria   │
    │ SF/Chain│    │ Hailo-8  │    │ Agents  │
    └────┬────┘    └────┬─────┘    └────┬────┘
         └───────────────┼───────────────┘
                         ▼
                    ┌─────────┐
                    │  alice  │  ← K8s + VPN hub
                    └─────────┘
```

**Key insight:** The OPERATOR sits between us and all external services. Cloudflare, Salesforce, and GitHub are utilities we command—not landlords we rent from. The control plane lives on hardware we own.

---

## The Routing Pattern

```
[User Request] → [Operator] → [Route to Right Tool] → [Answer]
                     │
                     ├── Physics question? → NumPy/SciPy
                     ├── Language task? → Claude/GPT API
                     ├── Customer lookup? → Salesforce API
                     ├── Legal question? → Legal database
                     └── Fast inference? → Hailo-8 local
```

The agent doesn't need to be smart. It needs to know **who to call.**

---

## The Business Model

| What We Own | What We Don't Need |
|-------------|-------------------|
| Customer relationships | Training models |
| Routing/orchestration logic | GPUs |
| Data and state | Data centers |
| The Operator | The intelligence itself |

When better models come out, we add them to the router. Infrastructure stays the same.

---

## The Math

At $1/user/month:

- 1M users = $12M/year
- 100M users = $1.2B/year
- 1B users = $12B/year

Ceiling: everyone who ever talks to AI.

---

## GitHub Enterprise Organizational Matrix

The operational surface area of BlackRoad OS is structured within a GitHub Enterprise environment at <https://github.com/enterprises/blackroad-os>. This enterprise-level abstraction provides governance and security boundaries for managing fifteen distinct organizations. Each organization is tasked with a specific functional domain, implementing the principle of least privilege so that agents in one domain are isolated from sensitive assets in another.

The fifteen organizations serve as the primary targets for the @blackroad-agents task distribution layer:

| Organization | Primary Responsibility | Repository Examples |
|--------------|----------------------|---------------------|
| **Blackbox-Enterprises** | Corporate and Enterprise Integrations | blackbox-api, enterprise-bridge |
| **BlackRoad-AI** | Core LLM and Reasoning Engine Development | lucidia-core, blackroad-reasoning |
| **BlackRoad-Archive** | Long-term Data Persistence and Documentation | blackroad-os-docs, history-ledger |
| **BlackRoad-Cloud** | Infrastructure as Code and Orchestration | cloud-orchestrator, railway-deploy |
| **BlackRoad-Education** | Onboarding and Documentation Frameworks | br-help, onboarding-portal |
| **BlackRoad-Foundation** | Governance and Protocol Standards | protocol-specs, governance-rules |
| **BlackRoad-Gov** | Regulatory Compliance and Policy Enforcement | compliance-audit, regulatory-tools |
| **BlackRoad-Hardware** | SBC and IoT Device Management | blackroad-agent-os, pi-firmware |
| **BlackRoad-Interactive** | User Interface and Frontend Systems | blackroad-os-web, interactive-ui |
| **BlackRoad-Labs** | Experimental R&D and Prototyping | experimental-agents, quantum-lab |
| **BlackRoad-Media** | Content Delivery and Public Relations | media-engine, pr-automation |
| **BlackRoad-OS** | Core System Kernel and CLI Development | blackroad-cli, kernel-source |
| **BlackRoad-Security** | Auditing, Cryptography, and Security | security-audit, hash-witnessing |
| **BlackRoad-Studio** | Production Assets and Creative Tooling | lucidia-studio, creative-assets |
| **BlackRoad-Ventures** | Strategic Growth and Ecosystem Funding | tokenomics-api, venture-cap |

The implementation utilizes GitHub Apps for cross-organization repository access, which is superior to Personal Access Tokens (PATs) due to their short-lived, granular permissions and ability to act on behalf of an organization rather than an individual user.

---

## Domain Architecture and Cloudflare Integration

The project manages a registry of primary domains orchestrated via Cloudflare. This domain layer serves as the ingress point for the @BlackRoadBot routing matrix. Cloudflare Tunnels securely expose local Raspberry Pi nodes to the public internet, allowing the bot to invoke local inference models without exposing internal network ports.

| Domain | Functional Use Case | Associated Organization |
|--------|-------------------|------------------------|
| blackboxprogramming.io | Developer Education and APIs | Blackbox-Enterprises |
| blackroad.io | Core Project Landing Page | BlackRoad-OS |
| blackroad.company | Corporate and HR Operations | BlackRoad-Ventures |
| blackroad.me | Personal Agent Identity Nodes | BlackRoad-AI |
| blackroad.network | Distributed Network Interface | BlackRoad-Cloud |
| blackroad.systems | Infrastructure and System Ops | BlackRoad-Cloud |
| blackroadai.com | AI Research and API Hosting | BlackRoad-AI |
| blackroadinc.us | US-based Governance and Legal | BlackRoad-Gov |
| blackroadqi.com | Quantum Intelligence Research | BlackRoad-Labs |
| blackroadquantum.com | Primary Quantum Lab Interface | BlackRoad-Labs |
| lucidia.earth | Memory Layer and Personal AI | BlackRoad-AI |
| lucidia.studio | Creative and Asset Management | BlackRoad-Studio |
| roadchain.io | Blockchain and Witnessing Ledger | BlackRoad-Security |
| roadcoin.io | Tokenomics and Financial Interface | BlackRoad-Ventures |

---

## The @blackroad-agents Deca-Layered Scaffold

Every task entered into the system follows a ten-step scaffolding process triggered by the `@blackroad-agents` command, ensuring high-fidelity execution through review, distribution, and deployment stages.

### 1. Initial Reviewer

The scaffold begins at the reasoning layer. A high-level agent residing in Layer 6 (Lucidia Core) reviews the incoming request for clarity, security compliance, and resource availability, then generates a preliminary execution plan.

### 2. Task Distributor to Organization

The task is routed to one of the fifteen BlackRoad organizations by identifying which functional domain—hardware, security, cloud, etc.—is best equipped to handle the task.

### 3. Task Distribution to Team

Within the selected organization, the task is further refined and distributed to a specific team. This layer handles human-in-the-loop (HITL) requirements, pausing for manual approval if the task involves high-risk operations.

### 4. Task Update to Project

The task is recorded in a GitHub Project board for visibility and telemetry. Metadata about the task—such as Request ID and intended timeline—is synchronized with Salesforce to maintain an enterprise-level audit trail.

### 5. Task Distribution to Agent

A specialized autonomous agent is instantiated or assigned by skill (e.g., "fastapi-coder-agent" or "doctl-infrastructure-agent"). These agents follow the "Planner-Executor-Reflector" design pattern, iterating on their own code until requirements are met.

### 6. Task Distribution to Repository

The agent identifies the target repository and creates a new branch, ensuring changes are tested in isolation following the standard GitHub Flow branching strategy.

### 7. Task Distribution to Device

If the task requires physical execution—such as deploying firmware to a Raspberry Pi or rebuilding a DigitalOcean Droplet—it is routed to the device layer. This is where offloading from centralized cloud services to local hardware clusters occurs.

### 8. Task Distribution to Drive

Relevant artifacts (log files, reports, documentation) are distributed to Google Drive via a Service Account (GSA) pattern, ensuring agents have consistent write access without interactive user logins.

### 9. Task Distribution to Cloudflare

Network configuration changes—such as creating a new Cloudflare Tunnel or modifying DNS records—are executed at this layer, ensuring newly deployed services are immediately reachable and secured.

### 10. Task Distribution to Website Editor

The final step routes changes to an AI-driven website editor or headless CMS, allowing autonomous generation of landing pages, blog posts, or documentation updates.

---

## The @BlackRoadBot Routing Matrix

When a user comments `@BlackRoadBot` on a GitHub issue or pull request, the bot identifies target platforms based on natural language intent.

### Salesforce CRM and Task Orchestration

- **Task Creation:** An Apex middleware triggers a "Case" or "Custom Task" object in Salesforce.
- **Data Activation:** Salesforce Data Cloud ingests telemetry from GitHub webhooks for real-time analytics.
- **Webhooks:** GitHub triggers are wired directly to Salesforce endpoints via salesforce-webhooks.

### Hugging Face and Ollama Reasoning

- **Hugging Face Inference Endpoints:** The bot can programmatically deploy dedicated model endpoints for high-compute tasks.
- **Ollama Integration:** For routine tasks, the bot utilizes the Ollama API exposed via a Cloudflare Tunnel (e.g., bartowski/Llama-3.2-3B-Instruct-GGUF).

### DigitalOcean and Railway Infrastructure

- **DigitalOcean Droplets:** Managed via `doctl` within GitHub Actions for scaling and rebuilding.
- **Railway Deployments:** Used for hosting ephemeral test environments for new feature branches.

---

## Layered Architecture of BlackRoad CLI v3

The BlackRoad CLI v3 is built upon a modular architecture defining agent behavior and infrastructure management:

| Layer | Name | Responsibility |
|-------|------|---------------|
| 3 | Agents/System | Autonomous agent lifecycle management and system-level processes |
| 4 | Deploy/Orchestration | Infrastructure provisioning across cloud and local nodes |
| 5 | Branches/Environments | Ephemeral environment management and git-branching logic |
| 6 | Lucidia Core/Memory | Long-term context, state transitions, and simulation data |
| 7 | Orchestration | High-level task distribution powering the @blackroad-agents scaffold |
| 8 | Network/API | REST and GraphQL endpoints for the @BlackRoadBot matrix |

This layered approach ensures resilience—a failure in Layer 8 (Network) does not affect the persistence of state in Layer 6 (Memory).

---

## roadchain and the Witnessing Architecture

The BlackRoad ecosystem incorporates a cryptographic strategy called **roadchain**. Unlike traditional blockchains that focus on consensus-based proof, roadchain functions as a "witnessing" architecture.

Every state transition—whether an agent committing code or a bot routing a task to Salesforce—is hashed using SHA-256 and appended to a non-terminating ledger. This creates an immutable record of *what happened* rather than *what is true*.

---

## Rate Limit Mitigation Strategies

Managing distributed agents at scale requires robust rate limit mitigation:

| Provider | Observed Limit | Mitigation Protocol |
|----------|---------------|-------------------|
| GitHub Copilot | RPM / Token Exhaustion | Redirect to local Raspberry Pi LiteLLM proxy |
| Hugging Face Hub | IP-based Rate Limit | Rotate HF_TOKEN or use authenticated SSH keys |
| Google Drive | Individual User Quota | Use Shared Drives with GSA "Content Manager" role |
| DigitalOcean API | Concurrent Build Limits | Queue tasks via Layer 7 Orchestration |
| Salesforce API | Daily API Request Cap | Batch updates via Data Cloud Streaming Transforms |

If a task fails at any scaffold layer, the system creates a GitHub Issue containing detailed logs from Layer 6 (Lucidia Core). A human reviewer or a "Reflect and Retry" plugin then assesses the failure.

---

## Future Scaling: 30k Agents

The BlackRoad ecosystem is designed for massive scale, with active development on the `blackroad-30k-agents` repository. This project aims to orchestrate 30,000 autonomous agents using Kubernetes auto-scaling and self-healing, transitioning from Raspberry Pi clusters to larger ARM-based data centers mirroring the decentralized witnessing architecture.

---

## Implementation Guide

The FastAPI pattern is the starting point:

1. **Expose endpoints** (`/physics/hydrogen`, `/relativity/time-dilation`)
2. **Operator routes** (keyword matching → right function)
3. **Log everything** (JSON audit trail → future ledger)

This is the Operator pattern in miniature. Start with physics, extend to every domain.

---

## Verification

- **Source of Truth:** GitHub (BlackRoad-OS) + Cloudflare
- **Hash Verification:** PS-SHA-∞ (infinite cascade hashing)
- **Authorization:** Alexa's pattern via Claude/ChatGPT

---

*Last Updated: 2026-02-27*
*BlackRoad OS, Inc. - Proprietary and Confidential*
