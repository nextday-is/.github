# Naming & structure — Nextday standard

**Naming and structure are a top priority at Nextday.** A name is an interface: people,
scripts, Claude and clients all depend on it. Every new repo, Worker, database, folder,
file, binding and URL follows this page. If something doesn't fit, fix the name or update
this page in the same change — never leave a one-off.

## Core rules

1. **lowercase-kebab-case** for everything people type: repos, Workers, D1, R2, queues,
   folders, files, URL paths, branch names.
2. **Name things after what they are, not their history.** No `demo`, `new`, `v2`, `old`,
   `test`, `final`, `homepage` on something that is none of those.
3. **No redundant prefixes inside a scope.** In the `innbak` repo a file is
   `tests/access.test.mjs`, not `tests/innbak-access.test.mjs`.
4. **One name per thing, everywhere.** Repo, local folder, `package.json` name and docs use
   the same slug.
5. **Public URLs are contracts.** Never rename a live URL path or MCP endpoint without a
   redirect and telling the client.

## The pattern

| Thing | Pattern | Examples |
|---|---|---|
| Client / product slug | short brand name, one word if possible | `innbak`, `vokbaths`, `klaustur` |
| GitHub repo (client system) | `<client>` | `nextday-is/innbak` |
| GitHub repo (Nextday's own) | `nextday-<thing>` | `nextday-is/nextday-web`, `nextday-is/nextday-clients`, `nextday-is/nextday-platform` |
| Client registry entry | `clients/<slug>/client.json` in `nextday-clients` | `clients/innbak/client.json` |
| GitHub deploy environment | `<slug>-production` (INNBAK: `production`, legacy) | `acme-production` |
| Local clone | `C:\nextday\repos\<repo>` | `C:\nextday\repos\innbak` |
| Cloudflare Worker | `<slug>-<component>` | `nextday-web`, `innbak-portal`, `innbak-warehouse-ingest` |
| D1 database | `<slug>-<purpose>` | `innbak-warehouse` |
| R2 bucket | `<slug>-<purpose>-<content>` | `innbak-warehouse-evidence` |
| Queue | `<slug>-<purpose>-<job>`, DLQ ends `-dlq` | `innbak-warehouse-ingest`, `innbak-warehouse-dlq` |
| Binding (code) | `SCREAMING_SNAKE`, slug first | `INNBAK_WAREHOUSE`, `INNBAK`, `ASSETS` |
| Secret | `<SYSTEM>_<KIND>` | `DK_API_KEY`, `CLOUDFLARE_API_TOKEN` |
| API token | `<slug>-<where>-<purpose>` | `innbak-github-deploy` |
| Public URL path | `/<slug>/` | `/innbak/`, `/vokbaths/` |
| MCP endpoint | `/<slug>/mcp` | `/innbak/mcp` |
| Branch | from a Linear issue: `nex-<n>-<short-title>` (Linear's "copy branch name", format identifier-title); no issue: `feat/…`, `fix/…`, `chore/…`, `docs/…` | `nex-12-empty-invoice-page`, `docs/readme-monitoring` |
| Company handle (every SaaS) | `nextday-is` | `github.com/nextday-is`, `linear.app/nextday-is`, `nextday-is.sentry.io` |
| Linear team / issue key | team `Nextday`, key `NEX` | `NEX-12` |
| Linear project | same as the repo or client slug | `innbak`, `nextday-web`, `nextday-platform`, `nextday-clients` |
| Linear client label | group `client` → `<slug>` | `client/innbak` |
| Sentry project | same as the Worker | `innbak-portal`, `nextday-web` |
| Entra app registration | `nextday-<purpose>` (one app per purpose) | `nextday-access` |
| App secret description | `<where>-<purpose>` | `cloudflare-access` |
| Person / mailbox | `<firstname>@nextday.is` | `baldvin@nextday.is` |
| Exchange migration | endpoint `<source>-<protocol>`, batch `<source>-<mailbox>` | `hostinger-imap`, `hostinger-baldvin` |
| Commit | Conventional Commits | `fix: handle empty invoice page` |


## Repo layout

```
<repo>/
├── README.md            what it is, where it runs, how to deploy
├── CLAUDE.md            points here; repo-specific rules
├── src/                 Worker code (src/worker.ts is the entry)
├── public/<path>/       static assets, folder = public URL path
├── db/migrations/       D1 migrations (+ db/*.sql seeds)
├── docs/                design and operations records
├── scripts/             build/seed helpers
├── tools/               owner-run tools (no "<client>-" prefix)
├── tests/               *.test.mjs (unit), *.mjs (runnable checks)
├── wrangler.jsonc       main Worker;  wrangler.<component>.jsonc for others
└── .github/workflows/   ci.yml, deploy.yml
```

## Current map

| Product | Repo | Workers | Data | URL |
|---|---|---|---|---|
| Nextday website + demos | `nextday-web` | `nextday-web` | — | `/`, `/vokbaths/`, `/klaustur/` |
| Client registry | `nextday-clients` | — | — | — |
| INNBAK | `innbak` | `innbak-portal`, `innbak-warehouse-ingest` | D1 `innbak-warehouse`, R2 `innbak-warehouse-evidence`, queues `innbak-warehouse-ingest`, `innbak-warehouse-dlq` | `/innbak/` |
