# Production Keys Reference — Blackbox-Enterprises

> Cross-reference for the Blackbox-Enterprises organization.
> Canonical source: [BlackRoad-OS-Inc/blackroad-operator/PRODUCTION_KEYS.md](https://github.com/BlackRoad-OS-Inc/blackroad-operator/blob/master/PRODUCTION_KEYS.md)

---

## Stripe Products (Live)

| Product | Stripe ID | Status |
|---------|-----------|--------|
| BlackRoad OS - Free | `prod_U44z9MYb3qlT4J` | ACTIVE |
| BlackRoad OS - Pro | `prod_U44zFTKhJ5pJNR` | ACTIVE |
| BlackRoad OS - Enterprise | `prod_U44zceSnDMaEmX` | ACTIVE |

## Stripe Prices (Live)

| Tier | Interval | Amount | Price ID |
|------|----------|--------|----------|
| Pro | Monthly | $29 | `price_1T5wq63e5FMFdlFwHhMAtyNi` |
| Pro | Yearly | $290 | `price_1T5wq73e5FMFdlFw5ELr89dX` |
| Enterprise | Monthly | $199 | `price_1T5wq83e5FMFdlFwt53jdGqX` |
| Enterprise | Yearly | $1,990 | `price_1T5wq83e5FMFdlFw6Bsae4dK` |

## Payment Links (Live)

| Tier | Link |
|------|------|
| Pro Monthly | https://buy.stripe.com/5kQbIUd3y8xT8SD3s04Vy00 |
| Pro Yearly | https://buy.stripe.com/7sY28k0gM9BX2uf7Ig4Vy01 |
| Enterprise Monthly | https://buy.stripe.com/bJe9AM7Je29v9WH2nW4Vy02 |
| Enterprise Yearly | https://buy.stripe.com/fZu14ge7CcO9fh17Ig4Vy03 |

## Required Secrets for Workflows

These secrets must be set at the **organization level** in Blackbox-Enterprises:

```
CLOUDFLARE_API_TOKEN          # Cloudflare scoped API token
CLOUDFLARE_ACCOUNT_ID         # 848cf0b18d51e0170e0d1537aec3505a
RAILWAY_TOKEN                 # Railway deployment token
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY  # Clerk public key
DEPLOY_URL                    # Health check endpoint
```

## Enterprise Automation Stack

| Service | Repo | Role |
|---------|------|------|
| n8n | `blackbox-n8n` | Workflow automation (Stripe, Google, 400+ integrations) |
| Airbyte | `blackbox-airbyte` | Data integration (Google Drive, Sheets, 300+ connectors) |
| Prefect | `blackbox-prefect` | Workflow orchestration |
| Temporal | `blackbox-temporal` | Durable execution |
| ActivePieces | `blackbox-activepieces` | No-code automation (Google Drive, Stripe actions) |

## Google Drive Integration

Configured via enterprise automation stack:
- **n8n:** Full Google Drive, Sheets, Calendar, Docs, Contacts nodes
- **Airbyte:** source-google-drive, source-google-sheets connectors
- **ActivePieces:** Google Drive actions (create/upload/read/list/move/delete)
- **OAuth2:** `accounts.google.com/o/oauth2/auth` + `oauth2.googleapis.com/token`
- **Scope:** `https://www.googleapis.com/auth/drive`

---

*Last updated: 2026-02-28*
