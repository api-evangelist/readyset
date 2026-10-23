---
title: "How Readyset Rewrites Your SQL: Subqueries in HAVING, ORDER BY, JOIN ON"
url: "https://readyset.io/blog/where-a-subquery-can-live"
date: "2026-08-20"
author: "Vassili Zarouba"
feed_url: "https://readyset.io/blog/rss.xml"
---
Readyset used to reject subqueries in HAVING, ORDER BY, and JOIN ON outright, sending the whole query back to the database, uncached. This post extends the rewrite pipeline to decorrelate all four positions, with the soundness argument for the tricky one: LEFT OUTER JOIN, where the obvious move silently returns wrong answers.
