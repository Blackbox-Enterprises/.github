# BlackRoad Architecture Overview

> **The Core Thesis:** BlackRoad is a routing company, not an AI company.

---

## Executive Summary

We don't train models or buy GPUs. We route requests to the right tool through an orchestration layer running on hardware we own — a Raspberry Pi cluster with Hailo-8 accelerators for local inference, plus NumPy, legal databases, and domain-specific APIs.

**The insight:** The value is in routing requests to the right tool at the right time — not in paying providers or building another brain. All inference runs locally on our Pi fleet.

---

## Infrastructure (~$40/month recurring)

| Layer | Service | Role |
|-------|---------|------|
| Edge/CDN | Cloudflare | Handles millions of connections, DNS, DDoS |
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
                     ├── Language task? → Hailo-8 local inference (octavia/lucidia)
                     ├── Customer lookup? → Salesforce API
                     ├── Legal question? → Legal database
                     └── Agent task? → Pi fleet (aria orchestration)
```

The agent doesn't need to be smart. It needs to know **who to call.** All inference stays on our hardware.

---

## The Business Model

| What We Own | What We Don't Need |
|-------------|-------------------|
| Customer relationships | Training models |
| Routing/orchestration logic | GPUs |
| Data and state | Data centers |
| The Operator | The intelligence itself |

When better local models come out, we deploy them to the Pi fleet. No provider dependencies. Infrastructure stays the same.

---

## The Math

At $1/user/month:

- 1M users = $12M/year
- 100M users = $1.2B/year
- 1B users = $12B/year

Ceiling: everyone who ever talks to AI.

---

## Organization Structure

BlackRoad operates across 15 specialized GitHub organizations:

| Organization | Focus |
|--------------|-------|
| **BlackRoad-OS** | Core operating system, operator, infrastructure |
| **BlackRoad-AI** | AI models, routing, inference |
| **BlackRoad-Cloud** | Cloud services, deployment |
| **BlackRoad-Labs** | Research, experiments |
| **BlackRoad-Security** | Security tools, auditing |
| **BlackRoad-Foundation** | CRM, business tools |
| **BlackRoad-Media** | Content, publishing |
| **BlackRoad-Hardware** | IoT, ESP32, Pi projects |
| **BlackRoad-Education** | Learning, documentation |
| **BlackRoad-Gov** | Governance, voting |
| **BlackRoad-Interactive** | Games, 3D, metaverse |
| **BlackRoad-Archive** | Storage, backup |
| **BlackRoad-Studio** | Design, creative tools |
| **BlackRoad-Ventures** | Business, commerce |
| **Blackbox-Enterprises** | Enterprise solutions |

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
- **Authorization:** Alexa's pattern via BlackRoad Operator

---

*Last Updated: 2026-03-03*
*BlackRoad OS, Inc. - Proprietary and Confidential*
