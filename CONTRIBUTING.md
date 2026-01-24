# Contributing to BlackRoad

Thank you for your interest in contributing to BlackRoad! This document provides guidelines for contributing across all BlackRoad organizations.

## Core Philosophy

Before contributing, understand our fundamental principle:

> **BlackRoad is a routing company, not an AI company.**

We don't build models or own GPUs. We orchestrate existing intelligence through a proprietary routing layer. Every contribution should align with this philosophy.

## The Routing Pattern

```
[User Request] → [Operator] → [Route to Right Tool] → [Answer]
                     ├── Physics question? → NumPy/SciPy
                     ├── Language task? → Claude/GPT API
                     ├── Customer lookup? → Salesforce API
                     ├── Legal question? → Legal database
                     └── Fast inference? → Hailo-8 local
```

When proposing features, think about **routing to existing tools** rather than building from scratch.

## Organizations

BlackRoad is organized into 15 specialized repositories:

| Organization | Focus |
|-------------|-------|
| BlackRoad-OS | Core OS, operator, infrastructure |
| BlackRoad-AI | AI models, routing, inference |
| BlackRoad-Cloud | Cloud services, deployment |
| BlackRoad-Labs | Research, experiments |
| BlackRoad-Security | Security tools, auditing |
| BlackRoad-Foundation | CRM, business tools |
| BlackRoad-Media | Content, publishing |
| BlackRoad-Hardware | IoT, ESP32, Pi projects |
| BlackRoad-Education | Learning, documentation |
| BlackRoad-Gov | Governance, voting |
| BlackRoad-Interactive | Games, 3D, metaverse |
| BlackRoad-Archive | Storage, backup |
| BlackRoad-Studio | Design, creative tools |
| BlackRoad-Ventures | Business, commerce |
| Blackbox-Enterprises | Enterprise solutions |

Route your contribution to the appropriate organization.

## Getting Started

1. **Read the Architecture**: Review [BLACKROAD_ARCHITECTURE.md](./BLACKROAD_ARCHITECTURE.md) to understand the system design.

2. **Find an Issue**: Look for issues labeled `good first issue` or `help wanted`.

3. **Discuss First**: For significant changes, open an issue to discuss your approach before coding.

## Development Process

### Branching Strategy

- `main` - Stable, production-ready code
- `develop` - Integration branch for features
- `feature/*` - Feature branches
- `fix/*` - Bug fix branches
- `claude/*` - AI-assisted development branches

### Commit Messages

Use clear, descriptive commit messages:

```
<type>: <short summary>

<optional body>
```

Types:
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation
- `refactor` - Code refactoring
- `test` - Adding tests
- `chore` - Maintenance tasks

### Pull Requests

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Write/update tests
5. Submit a pull request using the template

## Code Standards

### General Principles

- **Route, don't build**: Leverage existing tools and APIs
- **Keep it simple**: Minimal complexity, maximum clarity
- **Document routing decisions**: Explain why requests go where they go
- **Test routing paths**: Ensure requests reach the correct handlers

### Node-Specific Guidelines

When contributing code that runs on specific nodes:

- **lucidia/octavia** (Pi 5 + Hailo-8): Consider 26 TOPS inference capability
- **aria** (Pi 5): Keep agent orchestration lightweight
- **alice** (Pi 400): Kubernetes-compatible, mesh-network aware
- **shellfish** (Digital Ocean): Public-facing security considerations

## Infrastructure

### Cost Awareness

BlackRoad runs on ~$40/month infrastructure. Contributions should:
- Not require expensive cloud resources
- Work within Salesforce's 15K API calls/day free tier
- Prefer edge computing over cloud when possible

### Mesh Network

All nodes communicate via Tailscale. Consider network topology when designing features.

## Security

- Never commit secrets, API keys, or credentials
- Report security vulnerabilities privately via GitHub Security Advisories
- Follow the principle of least privilege

## Questions?

- Open a discussion in the appropriate repository
- Review existing documentation
- Check the architecture document for system design questions

---

*Intelligence is already trained. Libraries already exist. We just route to the right ones.*
