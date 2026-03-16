# Supabase Database Toolkit - OpenClaw Skill

Full Supabase database toolkit - schema explorer, natural language queries, CRUD, pgvector search, RLS policies, migrations, health checks, data export, Warehouse analytics (pg_duckdb), automatic embeddings, queues (pgmq), Realtime, OAuth 2.1, Storage CDN, Edge Functions, and integrations.

## What it does

- **Schema explorer** - list tables, describe columns/types/relationships, view RLS policies and indexes
- **Natural language queries** - describe what you want in plain English, get SQL results
- **CRUD operations** - insert, select, update, upsert, delete with powerful filters
- **Vector search** - similarity search with pgvector embeddings
- **RLS policy helper** - generate Row Level Security policies from natural language descriptions
- **Migration management** - create, apply, and check status of schema migrations
- **Health checks** - connection status, database size, active connections, slow queries, index usage
- **Data export** - export tables as CSV or JSON with filters
- **Warehouse / pg_duckdb** - 600x faster analytics queries, Iceberg-format Analytics Buckets on S3
- **Automatic embeddings** - trigger-based pipeline auto-generates vector embeddings on insert/update
- **Queues / pgmq** - exactly-once message delivery with configurable visibility windows
- **Realtime** - Postgres Changes, Broadcast, Presence, and Broadcast from Database
- **Auth** - OAuth 2.1 server mode, X/Twitter OAuth 2.0
- **Storage** - 14.8x faster listing, Smart CDN, image transformations, resumable uploads, S3 compatibility
- **Edge Functions** - regional invocations, NPM compatibility, WASM support
- **Integrations** - Claude Connector (MCP), Stripe Sync Engine, Log Drains, PrivateLink
- **Infrastructure** - Database Branching, Read Replicas, Supabase Vault

## Quick start

### Install the skill

```bash
git clone https://github.com/mvanhorn/clawdbot-skill-supabase.git ~/.openclaw/skills/supabase
```

### Set up credentials

```bash
export SUPABASE_URL="https://yourproject.supabase.co"
export SUPABASE_SERVICE_KEY="eyJhbGciOiJIUzI1NiIs..."

# Or use the new project-scoped key (March 2026+)
export SUPABASE_API_KEY="sb_secret_..."

# Optional: direct Postgres access (enables migrations, health checks, schema dump)
export SUPABASE_DB_URL="postgresql://postgres:[PASSWORD]@db.[REF].supabase.co:5432/postgres"
```

### Example chat usage

- "Show me all the tables in my database"
- "Describe the schema for the orders table"
- "Query users who signed up in the last 7 days"
- "Insert a new product with name 'Widget' and price 29.99"
- "Search my documents for anything about authentication"
- "Generate an RLS policy so users can only see their own data"
- "Check database health - connections, size, slow queries"
- "Export the orders table as CSV"
- "Create a migration to add a comments table"
- "Run an analytics query on pageviews from the last 30 days"
- "Set up automatic embeddings on my documents table"
- "Send a message to my task queue"
- "Show me who is online via Realtime Presence"

## Commands

| Command | What it does |
|---------|-------------|
| `query` | Run raw SQL (including Warehouse/pg_duckdb queries) |
| `select` | Query with filters (--eq, --gt, --lt, --like, --limit, --order, etc.) |
| `insert` | Insert one or more rows |
| `update` | Update rows matching filters |
| `upsert` | Insert or update |
| `delete` | Delete rows matching filters |
| `vector-search` | Similarity search via pgvector |
| `tables` | List all tables with row counts |
| `describe` | Show table schema (columns, types, constraints) |
| `schema` | Full schema dump (requires SUPABASE_DB_URL) |
| `rpc` | Call a stored procedure |
| `health` | Database health check |
| `export` | Export data as CSV or JSON |
| `migration` | Create, apply, or check migration status |

## How it works

Wraps the Supabase REST API (PostgREST) with a shell script CLI. Uses the service role key for full access (bypasses RLS). Direct Postgres features (migrations, health, schema dump) require `SUPABASE_DB_URL`. Vector search requires pgvector extension and `OPENAI_API_KEY` for embedding generation. Warehouse queries run through pg_duckdb for columnar analytics acceleration.

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `SUPABASE_URL` | Yes | Project URL |
| `SUPABASE_SERVICE_KEY` | Yes* | Service role key (legacy) |
| `SUPABASE_API_KEY` | No* | Project-scoped key (new, March 2026+) |
| `SUPABASE_DB_URL` | No | Direct Postgres connection string |
| `OPENAI_API_KEY` | No | For generating embeddings |
| `SUPABASE_ACCESS_TOKEN` | No | Management API token |

*Either `SUPABASE_SERVICE_KEY` or `SUPABASE_API_KEY` required.

## What's new in v3.0.0

- **Warehouse / pg_duckdb** - 600x analytics acceleration, Iceberg Analytics Buckets on S3
- **Automatic embeddings** - trigger-based pipeline with pgmq + pg_cron + Edge Functions
- **Queues / pgmq** - exactly-once delivery, pgmq_public for client consumers, worker patterns
- **Realtime** - Postgres Changes, Broadcast, Presence, Broadcast from Database (beta)
- **OAuth 2.1 Server** - Supabase as identity provider (Nov 2025 beta)
- **X/Twitter OAuth 2.0** - replacing legacy 1.0a flow (Feb 2026)
- **Storage improvements** - 14.8x faster listing, Smart CDN, image transforms, resumable uploads, S3 compat
- **Edge Functions** - regional invocations, rate limiting, NPM/WASM support
- **Claude Connector** - 32 MCP tools for Supabase
- **Stripe Sync Engine** - query Stripe data via SQL
- **Log Drains** - Datadog, Grafana, Sentry, Axiom, S3 (Pro plan)
- **PrivateLink** - AWS VPC connectivity (Jan 2026)
- **Database Branching** - preview environments with isolated schema copies
- **Read Replicas** - regional read-only replicas for lower latency
- **Supabase Vault** - encrypted secrets storage in Postgres
- **Project-scoped API keys** - `sb_publishable_` / `sb_secret_` format
- **OpenAPI spec restricted** - service_role keys only (March 11, 2026)

## API key migration (March 2026)

Supabase is deprecating legacy JWT-format keys. New project-scoped keys use `sb_publishable_` and `sb_secret_` prefixes. Both formats work during the transition (through late 2026). See SKILL.md for the full migration guide.

## License

MIT
