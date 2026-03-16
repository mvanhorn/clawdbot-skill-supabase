# Supabase Database Toolkit - OpenClaw Skill

Full Supabase database toolkit - schema explorer, natural language queries, migration management, RLS policy helper, pgvector search, data export, health monitoring.

## What it does

- **Schema explorer** - list tables, describe columns/types/relationships, view RLS policies and indexes
- **Natural language queries** - describe what you want in plain English, get SQL results
- **CRUD operations** - insert, select, update, upsert, delete with powerful filters
- **Vector search** - similarity search with pgvector embeddings
- **RLS policy helper** - generate Row Level Security policies from natural language descriptions
- **Migration management** - create, apply, and check status of schema migrations
- **Health checks** - connection status, database size, active connections, slow queries, index usage
- **Data export** - export tables as CSV or JSON with filters

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
export SUPABASE_API_KEY="sbp_..."

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
- "Show me tables that don't have RLS enabled"

## Commands

| Command | What it does |
|---------|-------------|
| `query` | Run raw SQL |
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

Wraps the Supabase REST API (PostgREST) with a shell script CLI. Uses the service role key for full access (bypasses RLS). Direct Postgres features (migrations, health, schema dump) require `SUPABASE_DB_URL`. Vector search requires pgvector extension and `OPENAI_API_KEY` for embedding generation.

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

## API key migration (March 2026)

Supabase is deprecating legacy JWT-format keys. New project-scoped keys use the `sbp_` prefix. Both formats work during the transition (through late 2026). See SKILL.md for the full migration guide.

## License

MIT
