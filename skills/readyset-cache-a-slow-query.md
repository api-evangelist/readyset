---
name: Cache a slow query with Readyset
description: >-
  Find a costly proxied query on a running Readyset instance, confirm it is
  cacheable, and cache it — then verify the cache is serving. Grounded in the
  official Readyset MCP tools.
api: mcp/readyset-mcp.yml
transport: mcp
operations:
  - readyset_status
  - show_proxied_queries
  - show_proxied_supported
  - explain_cache_support
  - create_cache
  - show_caches
---

# Cache a slow query with Readyset

Readyset is a wire-protocol SQL caching engine that sits in front of Postgres or
MySQL. This skill uses the official **Readyset MCP server** (`mcp/readyset-mcp.yml`)
to identify a slow query and cache it without touching application code.

## Prerequisites
- A running Readyset instance with the MCP endpoint enabled
  (`--enable-mcp --mcp-address <host>:6035`) or the `readyset-mcp` stdio binary.
- A bearer token created in SQL with at least `cache_admin` scope:
  `CREATE MCP TOKEN 'agent' WITH SCOPE cache_admin EXPIRES '2027-01-01T00:00:00Z';`
- `create_cache` and `drop_cache` require the `cache_admin` scope; all `show_*`
  and `explain_*` tools work with `read_only`.

## Steps
1. **Check health.** Call `readyset_status` to confirm the adapter is healthy and
   snapshotting/replication is caught up (low replication lag). Do not cache while
   a snapshot is still in progress.
2. **Find candidates.** Call `show_proxied_queries` to list queries currently
   proxied to upstream, then `show_proxied_supported` to narrow to the ones
   Readyset can actually cache. Pick the costliest supported query and note its
   `query_id`.
3. **Confirm cacheability.** Call `explain_cache_support` for that query to verify
   it is supported before creating anything.
4. **Create the cache.** Call `create_cache` with the `query_id` (or the SELECT
   text). This is the only mutating step — it maps to a `CREATE CACHE` statement.
5. **Verify.** Call `show_caches` to confirm the new cache is listed, then
   `show_proxied_queries` again to confirm the query is no longer proxied to
   upstream (it is now served from the cache).

## Rules and cautions
- Only `create_cache`/`drop_cache` mutate state; everything else is read-only —
  prefer the `read_only`-scoped tools for inspection.
- Readyset keeps caches fresh automatically from the database replication stream;
  there is no manual invalidation step.
- If `explain_cache_support` reports a query is unsupported, do not force it —
  report the reason instead of guessing.
