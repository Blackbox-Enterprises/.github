# CLAUDE.md — Blackbox-Enterprises/.github

> Organization-wide default community health files and CI/CD workflows for the BlackRoad ecosystem.

## Repository Purpose

This is the **organization-level `.github` repository** for Blackbox-Enterprises. Files here serve as defaults across all repositories in the organization — including issue/PR templates, workflows, security policy, and contribution guidelines. It is **not** an application codebase; it is infrastructure and governance configuration.

## Core Philosophy

**BlackRoad is a routing company, not an AI company.** The system routes user requests to the correct existing tool (Claude/GPT, NumPy, Salesforce, Hailo-8, legal databases) rather than building models from scratch. All contributions must align with this routing-first principle.

```
[User Request] → [Operator] → [Route to Right Tool] → [Answer]
```

## Repository Structure

```
.github/
├── .github/
│   ├── dependabot.yml          # Automated dependency updates (npm, pip, actions)
│   └── workflows/
│       ├── auto-deploy.yml         # Deploy to Cloudflare/Railway on push to main
│       ├── blackroad-agent.yml     # Agent identity CI (runs on Pi fleet)
│       ├── bot-issue-triage.yml    # Auto-label/triage issues by keywords
│       ├── security-scan.yml       # Trufflehog, CodeQL, dependency audit
│       ├── self-healing.yml        # Health monitoring + auto-rollback (every 30 min)
│       ├── self-healing-master.yml # Master healer (every 10 min + on failure)
│       ├── test-auto-heal.yml      # Test runner with auto-fix on failure
│       └── upstream-sync.yml       # Weekly fork sync (n8n, prefect, temporal, etc.)
├── ISSUE_TEMPLATE/
│   ├── config.yml              # Disable blank issues, add contact links
│   ├── bug_report.yml          # Bug report with component/node dropdowns
│   └── feature_request.yml     # Feature request with routing pattern field
├── profile/
│   ├── README.md               # Organization profile (shown on GitHub org page)
│   └── BLACKROAD_ARCHITECTURE.md
├── agent.json                  # Agent fleet configuration (ALICE primary)
├── BLACKROAD_ARCHITECTURE.md   # System design and infrastructure docs
├── CONTRIBUTING.md             # Development guidelines and conventions
├── FUNDING.yml                 # GitHub Sponsors + blackroad.io links
├── LICENSE                     # Proprietary (BlackRoad OS, Inc.)
├── PULL_REQUEST_TEMPLATE.md    # PR template with org/node/routing fields
└── SECURITY.md                 # Vulnerability reporting policy
```

## Key Conventions

### Branching Strategy

| Branch | Purpose |
|--------|---------|
| `main` | Production-ready, protected |
| `develop` | Integration branch |
| `feature/*` | New features |
| `fix/*` | Bug fixes |
| `claude/*` | AI-assisted changes |

### Commit Messages

Use conventional commit prefixes:
- `feat:` — new feature
- `fix:` — bug fix
- `docs:` — documentation only
- `refactor:` — code restructuring
- `test:` — adding/updating tests
- `chore:` — maintenance, deps, CI

### Pull Requests

PRs must use the template in `PULL_REQUEST_TEMPLATE.md` which requires:
- Summary of changes
- Type of change (bug fix, feature, breaking, docs, infra, refactor)
- Target organization (one of the 15 BlackRoad orgs)
- Routing impact assessment
- Affected nodes (lucidia, octavia, aria, alice, shellfish, cecilia, arcadia)
- Checklist: code style, tests, self-review, routing philosophy alignment

## Infrastructure Context

### Budget Constraint: ~$40/month Total

| Layer | Service | Role |
|-------|---------|------|
| Edge/CDN | Cloudflare | DNS, DDoS, Workers |
| CRM | Salesforce (Free) | Customer data, 15K API calls/day |
| Code/CI | GitHub Enterprise | 15 orgs, Actions, deployment |
| Mesh | Tailscale | Private encrypted node network |
| Cloud | DigitalOcean (shellfish) | Public-facing gateway |

### Hardware Cluster (Self-Hosted Runners)

| Node | Hardware | Role |
|------|----------|------|
| lucidia | Pi 5 + Hailo-8 | Salesforce sync, RoadChain |
| octavia | Pi 5 + Hailo-8 | AI routing (26 TOPS), 3D printing |
| aria | Pi 5 | Agent orchestration, Cloudflare Workers |
| alice | Pi 400 | Kubernetes + VPN hub (mesh root) |
| shellfish | DO droplet | Public-facing gateway |
| cecilia | Mac | Dev machine |
| arcadia | iPhone | Edge device |

Workflows tagged with `runs-on: [self-hosted, pi]` execute on this fleet.

## CI/CD Workflows

### Automated Pipelines

- **auto-deploy.yml** — Detects service type (Next.js/Docker/Node/Python/static), deploys to Cloudflare Pages or Railway. Runs health check after deploy.
- **security-scan.yml** — Runs on PRs to main and weekly. Includes Trufflehog secret scanning, hardcoded token grep, npm/pip audit, and CodeQL analysis.
- **test-auto-heal.yml** — Runs tests, and on failure: cleans deps, reinstalls, rebuilds, commits fixes as "BlackRoad Auto-Heal Bot", then re-verifies.
- **self-healing.yml** — Every 30 minutes: checks `/api/health`, auto-rollbacks on failure, runs `npm update` for dependency freshness.
- **self-healing-master.yml** — Every 10 minutes + on any workflow failure: diagnoses, heals, creates issues if unresolvable.
- **bot-issue-triage.yml** — Auto-labels issues by keyword (bug/enhancement/security/agent names/priority).
- **upstream-sync.yml** — Weekly syncs forks: blackbox-n8n, blackbox-prefect, blackbox-temporal, blackbox-activepieces.
- **blackroad-agent.yml** — Loads agent identity from `.agents/{branch}.json`, reports health on Pi runners.

### Dependabot

Configured for npm, pip, and GitHub Actions — weekly Monday updates, auto-labeled, reviewed by `blackboxprogramming`.

## The 15 BlackRoad Organizations

When making changes, identify the correct target org:

| Organization | Focus |
|---|---|
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
| Blackbox-Enterprises | Enterprise solutions (this org) |

## Security Rules

- **Never** commit secrets, API keys, or tokens — secret scanning is active
- Report vulnerabilities to `security@blackroad.io`, not in public issues
- Use GitHub Security Advisories for coordinated disclosure
- All dependencies are audited automatically (CodeQL + Dependabot + Trufflehog)
- Follow the principle of least privilege for all access

## Editing Guidelines for AI Assistants

1. **This is a config/governance repo** — changes are YAML templates, Markdown docs, and workflow files. There is no application code to build or test locally.
2. **Respect the routing philosophy** — never suggest building custom AI models or heavy infrastructure. Route to existing tools.
3. **Cost-conscious** — the entire infra budget is ~$40/month. Don't suggest expensive services.
4. **Proprietary license** — this codebase is proprietary (BlackRoad OS, Inc.). Do not add open-source license headers or assume permissive licensing.
5. **Workflow changes are high-impact** — workflows in `.github/workflows/` run across the entire organization. Test changes carefully and note affected repos/nodes.
6. **Node awareness** — when modifying workflows that target self-hosted runners, understand which Pi node will execute them.
7. **Template changes affect all repos** — issue templates, PR templates, and community health files cascade to every repo in the Blackbox-Enterprises org that doesn't override them.
8. **agent.json** — the primary agent is ALICE. Fleet nodes: octavia-pi5, aria-pi4, cecilia, gematria-do, lucidia-pi5. Gateway: `http://octavia.local:8787`.
