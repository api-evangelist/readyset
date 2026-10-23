---
title: "Caching Supabase with Readyset over IPv6: the AWS and Docker pieces that have to line up"
url: "https://readyset.io/blog/caching-supabase-with-readyset-over-ipv6-the-aws-and-docker-pieces-that-have-to-line-up"
date: "2026-07-18"
author: "Vinicius Grippa"
feed_url: "https://readyset.io/blog/rss.xml"
---
Supabase's direct Postgres endpoint is IPv6-only, and a fresh AWS account has no IPv6 enabled. This walkthrough covers the exact VPC, subnet, and Docker configuration needed to run Readyset in front of Supabase on EC2, with three deployment paths: host network, dual-stack bridge, and Linux package.
