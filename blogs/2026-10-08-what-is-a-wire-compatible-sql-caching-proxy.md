---
title: "What Is a Wire-Compatible SQL Caching Proxy?"
url: "https://readyset.io/blog/what-is-a-wire-compatible-sql-caching-proxy"
date: "2026-10-08"
author: "Readyset Team"
feed_url: "https://readyset.io/blog/rss.xml"
---
A wire-compatible SQL caching proxy sits between your app and database, speaking the database's own protocol so you cache repeated queries by swapping a hostname, no cache keys, no invalidation logic, no application code changes. Here's how it works, how it differs from Redis, and how Readyset implements it for MySQL and Postgres.
