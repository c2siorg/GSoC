# B0Bot

# Project Abstract

B0Bot is a Flask-based cybersecurity news platform rebuilt during GSoC 2026 with C2SI. The legacy codebase relied on Pinecone, manual sync scripts, hardcoded scrapers, and a single monolith that could not scale ingestion separately from the API. Our GSoC goal was to replace that with a three-service architecture, PostgreSQL with pgvector for vector search, RSS-driven ingestion, email subscriptions, and a modern UI. Vishak Baddur worked on the LangGraph agent pipeline and frontend. I owned the backend infrastructure: Docker Compose, database schema, ingestion-service, notification-service, BullMQ queues, and the data pipeline end to end.

The system today runs fully on Docker Compose with no mandatory cloud dependencies. PostgreSQL stores articles, subscribers, RSS sources, digest delivery logs, and 384-dimensional embeddings from sentence-transformers/all-MiniLM-L6-v2. Redis hosts BullMQ queues and api-service cache. The ingestion-service polls cybersecurity RSS feeds every 15 minutes, deduplicates by SHA-256 url hash, enqueues article.discovered jobs, generates embeddings, extracts CVE and severity metadata, and upserts into pgvector. The notification-service schedules daily and weekly SMTP digests with unsubscribe links. The api-service serves landing, dashboard, chat, sources, and subscribe pages on top of the same Postgres data.

Services never import each other. They communicate only through Postgres rows and Redis queue payloads. Every queue job carries idempotency_key, event_type, and trace_id. Consumers check processed_jobs before side effects so duplicate polls or retries do not create duplicate articles or emails.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/7sf7V0bk)

## [GSoC Project Proposal](https://drive.google.com/file/d/1JIQWcUD9dQvTYz32AbCyb6QNHEkpgEv_/view?usp=sharing)

## [GSo Final Merged Proposal](https://drive.google.com/file/d/14Qe_kyJ-M0YhsAlZnCqU9kn7HqNj2uCt/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/b0bot)

## [GitHub Personal Repo](https://github.com/AQIB-NAWAB/b0bot)

## [Commits during GSoC 2026](https://github.com/c2siorg/b0bot/commits/main?author=AQIB-NAWAB)

## [Project Demo Video](https://docs.google.com/videos/d/14BHl_0-nkTLrMEZ6rMEe5W9WhAXpAplktn5C3QGMo1c/play?usp=sharing)

## [Project Wiki](https://github.com/c2siorg/b0bot/blob/main/README.md)

## [GSoC Blog](https://medium.com/@aqibnawab1100)

I maintained a weekly blog series on Medium rather than one single long post. All posts live under my profile at [medium.com/@aqibnawab1100](https://medium.com/@aqibnawab1100). The series documents architecture decisions, weekly progress, and technical lessons from the coding period.


| Blog                          | Topic                                                               |
| ----------------------------- | ------------------------------------------------------------------- |
| Choosing B0Bot's Architecture | Three services, BullMQ, and Postgres decision before coding started |
| GSoC 2026 Week 1-2            | Folder structure, Docker, PostgreSQL and pgvector foundation        |
| Week 3 and Week 4             | BullMQ queue, RSS polling, embedding backbone                       |
| Week 5-6                      | Full ingestion pipeline and first digest emails                     |
| Week 7-8                      | Email polish, config cleanup, service boundaries with Vishak        |
| Week 9                        | CISA feed fix, unsubscribe link, observability                      |
| Week 10                       | Config modules, CVE, severity, and topic tags at ingest             |


# Technical Overview

The repo layout follows a flat three-service structure at the root: api-service, ingestion-service, and notification-service, plus docker-compose.yml and docker/postgres/init.sql for schema bootstrap.

Postgres tables I worked with directly include articles (with url_hash, embedding vector, cve_id, severity, affected_system, topic_tags, embedding_status), sources (name, url, status pending or active), subscribers, digest_deliveries, and processed_jobs for queue idempotency. The articles table uses an HNSW index on the embedding column for similarity search that api-service uses in chat and dashboard flows.

RSS sources started as eight curated feeds in feeds.py (The Hacker News, BleepingComputer, CISA Alerts, Dark Reading, KrebsOnSecurity, Google Security Blog, SANS ISC, SecurityWeek). Later the poller reads active rows from the sources table so new feeds can be added from the UI without redeploying code. URL normalization strips tracking params and lowercases domains before hashing so dedup stays stable.

Metadata at ingest uses a two-layer approach. Regex and keyword heuristics in metadata.py extract CVE IDs, CVSS-based severity, affected systems, and topic tags like malware, ransomware, cve, data breach, and vulnerability. An optional HuggingFace Cohere call in llm_metadata.py can enrich severity and affected_system when a token is set. If the LLM fails or credits run out, ingest continues on regex alone and articles still land in Postgres.

The notification worker checks subscribers on a schedule, selects articles inside daily or weekly windows, renders an HTML digest template, sends via SMTP, and records each send in digest_deliveries with an idempotency key so the same subscriber does not get duplicate digests for the same window.

# Work Summary

Week 1-2 was foundation work. I scaffolded ingestion-service and notification-service, wrote docker/postgres/init.sql with pgvector extension and seed data, and raised PR #202 with Docker Compose for Postgres, Redis, and all three services. That unblocked Vishak to move LangGraph code into api-service.

Week 3-4 focused on the queue and ingest core. PR #206 added BullMQ worker skeleton and the article.discovered event contract. PR #210 wired RSS polling, url_hash dedup, MiniLM embeddings, and pgvector upsert. I added pytest baselines for ingestion-service so regressions were visible early.

Week 5-6 closed the loop from feed to inbox. PR #217 connected notification-service digest delivery with real SMTP, subscriber reads from Postgres, and digest window logic. The stack could ingest live news and email a digest without manual scripts.

Week 7-8 and 9 were about trust and polish. I improved the digest email template, added unsubscribe links that hit api-service and update subscribers in Postgres, fixed a broken CISA RSS URL, and added structured logging across ingestion and notification so Docker logs show feed timeouts, skip counts, and delivery results. Config modules in ingestion-service and notification-service centralised env vars and queue constants.

Week 10 added metadata enrichment (PR #234) and config refactor (PR #225). Articles now carry cve_id, severity, affected_system, and topic_tags at ingest time, which feeds Vishak's dashboard filters and CVE watchlist.

Week 11 shipped dynamic sources (PR #243). The poller loads active feeds from Postgres with a hardcoded fallback for dev. I also pre-downloaded the embedding model in the api-service Dockerfile so /chat does not hang on first request.

Week 12 was quality and CI. PR #246 added Ruff linting across all three services and removed legacy monolith test files that hit wrong routes. A separate PR added GitHub Actions to run Ruff and pytest on every push and pull request to main, plus scripts/run-ci.sh for the same checks locally.

Throughout the period I kept PRs small, linked open issues as mentors required, and coordinated with Vishak on shared schema (sources table, article columns) without crossing service import boundaries.

# What Covered

Everything in my GSoC proposal timeline for backend and infrastructure scope is done or merged. The table below lists my main pull requests to c2siorg/b0bot.


| PR                                                | Description                                                   | Status |
| ------------------------------------------------- | ------------------------------------------------------------- | ------ |
| [#202](https://github.com/c2siorg/b0bot/pull/202) | Postgres + pgvector schema, Docker Compose, service scaffolds | Merged |
| [#206](https://github.com/c2siorg/b0bot/pull/206) | BullMQ queue setup and ingestion worker skeleton              | Merged |
| [#210](https://github.com/c2siorg/b0bot/pull/210) | RSS polling, BullMQ ingestion, embedding pipeline             | Merged |
| [#217](https://github.com/c2siorg/b0bot/pull/217) | Ingestion pipeline + email digest delivery (Week 6)           | Merged |
| [#225](https://github.com/c2siorg/b0bot/pull/225) | Config modules and architecture documentation                 | Merged |
| [#231](https://github.com/c2siorg/b0bot/pull/231) | CISA feed fix, digest unsubscribe link, observability         | Merged |
| [#234](https://github.com/c2siorg/b0bot/pull/234) | CVE, severity, and topic tags at ingest time                  | Merged |
| [#243](https://github.com/c2siorg/b0bot/pull/243) | Dynamic RSS sources from Postgres, chat model preload         | Merged |
| [#246](https://github.com/c2siorg/b0bot/pull/246) | Ruff linter and removal of legacy monolith tests              | Open   |
| CI workflow PR                                    | GitHub Actions for lint and pytest on every PR                | Open   |


Ingestion-service now covers the full path from RSS poll to indexed row. The poller fetches feeds with a configurable timeout and user agent, parses entries, normalizes URLs, skips already processed url hashes, and enqueues jobs with schema_version and trace_id. The worker generates embeddings, enriches metadata, upserts articles with ON CONFLICT handling for embeddings and tags, and marks jobs in processed_jobs.

Notification-service covers subscriber digests end to end. It reads active subscribers from Postgres, queries recent articles inside daily or weekly windows, caps article count per digest, renders HTML email with frontend unsubscribe URLs, sends through SMTP with TLS, and logs sent or failed status in digest_deliveries.

Testing and quality work is in place. Ingestion-service has roughly 28 unit tests plus one optional live RSS integration test gated on RUN_FEED_INTEGRATION=1. Notification-service has 9 unit tests. Api-service grew to roughly 148 tests after Vishak's dashboard and route work. Ruff lint passes on all three service directories. The local run-ci.sh script mirrors the GitHub Actions workflow.

Vishak's merged work on the same repo completes the product: LangGraph agents (Planner, Scraper, Analyzer, Responder, Notification), Redis chat sessions, landing page, dashboard with CVE watchlist and filters, chat UI, sources page, and subscribe/unsubscribe flows. My report focuses on pipeline and infra; his report covers the agentic and frontend side.

The demo video linked above includes architecture slides and a short live run of docker compose up, the dashboard, and the ingestion flow.

# What left

For the GSoC 2026 scope we agreed with mentors, the timeline items on my side are covered. A few PRs were still open at final submission: Ruff linting in #246 and GitHub Actions CI. Vishak also had README and screenshot updates in progress. Those are polish items, not missing core features.

The project runs end to end for local demo and development. It is a solid foundation rather than a production-hardened platform. If C2SI continues B0Bot after GSoC, natural improvements would include moving high-volume event streaming from BullMQ on Redis to Kafka for better throughput and replay, adding metrics and distributed tracing, rate limiting on public API routes, and completing the README refresh with up to date screenshots once Vishak's docs PR merges.

Optional LLM enrichment through HuggingFace Inference can hit free tier credit limits. The code already falls back to regex metadata and local summarization, but a self-hosted model or paid credits would make Cohere-based severity and summaries more consistent during heavy ingest.

None of that was in the original GSoC must-have list. The core deliverable was three services, Postgres pgvector ingestion, digest notifications, metadata at ingest, dynamic sources, unit tests, and CI setup. That is what I set out to build, and that is what shipped.

# Contributor Details

**Name:** Aqib Nawab

**Email:** [aqibnawab1100@mail.com](mailto:aqibnawab1100@mail.com)

**GitHub:** [github.com/AQIB-NAWAB](https://github.com/AQIB-NAWAB/)

**LinkedIn:** [linkedin.com/in/m-aqib-nawab](https://www.linkedin.com/in/m-aqib-nawab/)

**Portfolio:** [aqibnawab.vercel.app](https://aqibnawab.vercel.app?utm_source=gsoc_final_report)

**Organization:** C2SI (Google Summer of Code 2026)

**Project:** B0Bot - Cybersecurity News API

**Mentors:** Hardik, Nipuna