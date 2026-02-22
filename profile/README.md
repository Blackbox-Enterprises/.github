<div align="center">

# Blackbox Enterprises

**No-code, low-code, and automation tools for enterprise AI workflows.**

[![Repos](https://img.shields.io/badge/repos-20+-black?style=flat-square)](https://github.com/orgs/Blackbox-Enterprises/repositories)
[![Stack](https://img.shields.io/badge/stack-TypeScript%20·%20Python%20·%20Go-FF1D6C?style=flat-square)](https://blackroad.ai)

</div>

---

## 🏭 What We Build

Blackbox Enterprises is the enterprise automation arm of BlackRoad OS — curating, deploying, and extending best-in-class open-source tools for AI-first workflows.

**Focus areas:**
- 🔄 **Workflow Automation** — n8n, Windmill, Automatisch
- 🗄️ **No-Code Databases** — NocoDB, Baserow, Directus
- 🛠️ **Low-Code Platforms** — Appsmith, Budibase, Tooljet
- 📝 **Forms & Surveys** — Formbricks, Typebot
- 🤝 **CRM/ERP** — Frappe/ERPNext
- 🌐 **API Testing** — Hoppscotch

---

## 📦 Repositories

### Workflow Automation

| Repo | Upstream | Purpose |
|------|----------|---------|
| [`blackbox-n8n`](https://github.com/Blackbox-Enterprises/blackbox-n8n) | n8n-io/n8n | Visual workflow builder, 400+ integrations |
| [`blackbox-windmill`](https://github.com/Blackbox-Enterprises/blackbox-windmill) | windmill-labs/windmill | Scripts → webhooks → workflows |
| [`blackbox-automatisch`](https://github.com/Blackbox-Enterprises/blackbox-automatisch) | automatisch/automatisch | Open-source Zapier alternative |
| [`blackbox-temporal`](https://github.com/Blackbox-Enterprises/blackbox-temporal) | temporalio/temporal | Durable workflow execution |
| [`blackbox-prefect`](https://github.com/Blackbox-Enterprises/blackbox-prefect) | PrefectHQ/prefect | Python data orchestration |
| [`blackbox-kestra`](https://github.com/Blackbox-Enterprises/blackbox-kestra) | kestra-io/kestra | YAML event-driven workflows |
| [`blackbox-huginn`](https://github.com/Blackbox-Enterprises/blackbox-huginn) | huginn/huginn | Agent-based automation |
| [`blackbox-dolphinscheduler`](https://github.com/Blackbox-Enterprises/blackbox-dolphinscheduler) | apache/dolphinscheduler | Big data task scheduling |
| [`blackbox-activepieces`](https://github.com/Blackbox-Enterprises/blackbox-activepieces) | activepieces/activepieces | Open-source Make alternative |
| [`blackbox-airbyte`](https://github.com/Blackbox-Enterprises/blackbox-airbyte) | airbytehq/airbyte | ELT data integration, 300+ connectors |

### No-Code / Low-Code Platforms

| Repo | Upstream | Purpose |
|------|----------|---------|
| [`blackbox-nocodb`](https://github.com/Blackbox-Enterprises/blackbox-nocodb) | nocodb/nocodb | Airtable alternative |
| [`blackbox-baserow`](https://github.com/Blackbox-Enterprises/blackbox-baserow) | baserow/baserow | Open-source database |
| [`blackbox-directus`](https://github.com/Blackbox-Enterprises/blackbox-directus) | directus/directus | Headless CMS + data platform |
| [`blackbox-appsmith`](https://github.com/Blackbox-Enterprises/blackbox-appsmith) | appsmithorg/appsmith | Internal tool builder |
| [`blackbox-budibase`](https://github.com/Blackbox-Enterprises/blackbox-budibase) | Budibase/budibase | Low-code platform |
| [`blackbox-tooljet`](https://github.com/Blackbox-Enterprises/blackbox-tooljet) | ToolJet/ToolJet | Open-source Retool |

### Forms, APIs & CRM

| Repo | Upstream | Purpose |
|------|----------|---------|
| [`blackbox-formbricks`](https://github.com/Blackbox-Enterprises/blackbox-formbricks) | formbricks/formbricks | Open-source Typeform |
| [`blackbox-typebot.io`](https://github.com/Blackbox-Enterprises/blackbox-typebot.io) | baptisteArno/typebot.io | Chatbot form builder |
| [`blackbox-hoppscotch`](https://github.com/Blackbox-Enterprises/blackbox-hoppscotch) | hoppscotch/hoppscotch | Open-source Postman |
| [`blackbox-frappe`](https://github.com/Blackbox-Enterprises/blackbox-frappe) | frappe/frappe | ERPNext framework |

---

## 🔌 Integration with BlackRoad OS

All Blackbox tools connect to the BlackRoad ecosystem:
- **Auth**: Single sign-on via BlackRoad identity
- **Memory**: PS-SHA∞ audit logs for all workflow executions
- **Agents**: Trigger any BlackRoad agent from n8n/Windmill
- **Gateway**: AI capabilities injected into forms and workflows

```bash
# Example: Trigger a BlackRoad agent from n8n
curl -X POST https://api.blackroad.ai/v1/agents/run \
  -H "Authorization: Bearer $BLACKROAD_TOKEN" \
  -d '{"agent": "alice", "task": "Deploy latest build"}'
```

---

> Part of the [BlackRoad OS](https://github.com/BlackRoad-OS-Inc) ecosystem — 17 orgs, 1,825+ repos.
> © BlackRoad OS, Inc. All rights reserved.
