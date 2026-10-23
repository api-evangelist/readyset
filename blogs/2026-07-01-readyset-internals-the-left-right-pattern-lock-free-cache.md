---
title: "Readyset Internals: The left-right pattern: lock-free cache"
url: "https://readyset.io/blog/lock-free-cache-reads-left-right"
date: "2026-07-01"
author: "Vinicius Grippa"
feed_url: "https://readyset.io/blog/rss.xml"
---
How does Readyset serve cached reads without ever taking a lock? Explore the mechanics and real-world benchmarks of the left-right pattern and its 1.2-nanosecond atomic pointer swap.
