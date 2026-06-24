# DataAssist-IO MCP Server

> Connect your databases, files, and warehouses to Claude, ChatGPT, and any MCP-compatible client — and let your team query them in plain language, safely and read-only.

[![Website](https://img.shields.io/badge/website-dataassist.io-2563eb)](https://dataassist.io)
[![MCP Registry](https://img.shields.io/badge/MCP-Registry-6366f1)](https://registry.modelcontextprotocol.io)
[![Endpoint](https://img.shields.io/badge/transport-Streamable%20HTTP-22c55e)](https://app.dataassist.io/mcp)
[![ChatGPT App](https://img.shields.io/badge/ChatGPT-Open%20App-10a37f)](https://chatgpt.com/apps/dataassist-io/asdk_app_6a26ec50353c8191b5774172b9a972cb)

**DataAssist-IO** is a hosted, multi-tenant [Model Context Protocol](https://modelcontextprotocol.io) server. Your organization signs up, connects its data sources, and your users query that data through natural language in their favorite LLM client. No SQL knowledge required for end users; no data copied or exposed beyond what you explicitly grant.

This is a **remote MCP server** — there is nothing to install or run yourself. You connect to it over an authenticated URL.

---

## Connection

| | |
|---|---|
| **Endpoint** | `https://app.dataassist.io/mcp` |
| **Transport** | Streamable HTTP |
| **Auth** | OAuth 2.1 (Dynamic Client Registration) |

You'll need a DataAssist-IO account and at least one connected data source. [Sign up at dataassist.io →](https://dataassist.io)

### Connect from Claude

In Claude (Desktop or web), add a custom connector pointing at:

```
https://app.dataassist.io/mcp
```

Claude will walk you through the OAuth sign-in. After you authorize, your org's tables appear as queryable tools.

### Connect from ChatGPT

DataAssist-IO is available as a published ChatGPT app — no manual setup required:

**[Open the DataAssist-IO app in ChatGPT →](https://chatgpt.com/apps/dataassist-io/asdk_app_6a26ec50353c8191b5774172b9a972cb)**

Launch it, sign in when prompted, and start querying your data.

### Connect from any MCP client

Point any client that supports the Streamable HTTP transport with OAuth at the endpoint above. The server implements OAuth discovery (`/.well-known/oauth-protected-resource`), so compliant clients negotiate authentication automatically.

---

## What you can do

Once connected, the assistant can use these **read-only** tools against the tables your admin has exposed to you:

| Tool | Purpose |
|------|---------|
| `list_tables` | Discover the tables available to you |
| `describe_table` | Inspect a table's columns and types |
| `get_table_metadata` | Read curated descriptions, tags, and per-column docs |
| `get_sample_data` | Preview a handful of rows |
| `query_data` | Run a read-only SQL `SELECT` (MySQL, Postgres, BigQuery, Redshift) |
| `query_collection` | Run a read-only aggregation pipeline (MongoDB, AWS DocumentDB) |

Every tool is **read-only by construction** — queries are validated as `SELECT`-only and run against read-only database sessions. Nothing your assistant does can modify or delete your data.

## Supported data sources

- **Files:** CSV, Excel, SFTP-delivered CSV
- **Databases:** MySQL, PostgreSQL, MongoDB, AWS DocumentDB
- **Warehouses:** Google BigQuery, Amazon Redshift

File-based sources are imported and stored as Apache Iceberg tables on your behalf; live databases and warehouses are queried in place — your data is never copied.

## Security & governance

- **Per-organization isolation** — every query is scoped to your org; tenants never see each other's data.
- **OAuth-authenticated** — no shared API keys; identity is established per user.
- **Team-level table grants** — admins control exactly which tables each team can reach.
- **Full audit trail** — every tool call is logged, with optional SOC2-grade request/response capture.
- **Read-only enforcement** — validated SELECT-only access plus read-only DB sessions, defense in depth.

---

## Getting started

1. **[Create an account](https://dataassist.io)** and your organization.
2. **Connect a data source** — upload a CSV or connect a database/warehouse from the dashboard.
3. **Expose tables** to your team and add curated metadata (optional but improves answer quality).
4. **Add the connector** in your LLM client using the endpoint above and sign in.
5. **Ask questions** about your data in plain language.

## Links

- 🌐 Website: <https://dataassist.io>
- 🔌 MCP endpoint: `https://app.dataassist.io/mcp`
- 📖 Model Context Protocol: <https://modelcontextprotocol.io>

## About this repository

This repository is the public home for the DataAssist-IO MCP server's registry listing. DataAssist-IO is a hosted service — the server runs in DataAssist-IO's infrastructure, so there is no code to clone or deploy here. For product questions or support, visit [dataassist.io](https://dataassist.io).
