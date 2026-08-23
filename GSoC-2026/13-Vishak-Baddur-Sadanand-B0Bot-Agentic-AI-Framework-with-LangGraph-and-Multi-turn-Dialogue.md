# Project Name
B0Bot - Agentic AI Framework with LangGraph and Multi-turn Dialogue
# Project Abstract
b0bot is a cybersecurity news intelligence platform. This project rebuilt its AI layer around a LangGraph multi-agent pipeline (PlannerAgent, ScraperAgent, ResponderAgent, AnalyzerAgent, NotificationAgent) with multi-turn dialogue and session memory, replaced Pinecone with PostgreSQL + pgvector, and added a dashboard home page, sources management, and email digest subscriptions. Built jointly with co-contributor Aqib Nawab, who owned the PostgreSQL migration, ingestion-service, and notification-service.
## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/GEyrYg7x)

## [GSoC Project Proposal](https://github.com/user-attachments/files/31336235/b0bot_proposal.pdf)

## [GitHub Organization Repo](https://github.com/c2siorg/b0bot)

## [GitHub Personal Repo](https://github.com/VishakBaddur/b0bot)

## [Commits during GSoC 2026](https://github.com/c2siorg/b0bot/commits/main/?author=VishakBaddur)

## [Project Demo Video](http://LinkToDemoVideo)

## [Project Wiki](https://github.com/c2siorg/b0bot/blob/main/README.md)
N/A - no separate wiki. Project documentation lives in the README
## [GSoC Blog](https://medium.com/@vishakbaddurs/c2si-google-summer-of-code-2026-agentic-ai-framework-with-langgraph-multi-turn-dialogue-and-2686a388b80f)

# Work Summary
Rebuilt b0bot's AI layer around a five-agent LangGraph pipeline (Planner, Scraper, Responder, Analyzer, and Notification), with multi-turn dialogue and Redis-backed session memory. I also built hybrid keyword/vector search on top of the PostgreSQL + pgvector data layer (migrated from Pinecone by my co-contributor Aqib). On top of that, I added article summaries with a local fallback model, per-article sentiment analysis with DistilBERT, the dashboard (CVE Watchlist, Top News, filterable feed, and single-turn Ask AI), the sources management page, and the subscribe/unsubscribe flow with interest tags and daily/weekly digests.

Along the way, I found and fixed a real Ask AI accuracy bug after the feature had already been merged: get_article_by_id() wasn't selecting the article content, so Ask AI was silently grounding on the shorter summary instead. I also removed three pockets of old pre-restructure code, updated the README based on the current behavior, and fixed a missing test dependency that meant the suite had only been running in local development and not inside the project's Docker image.

# What Covered
- LangGraph agentic framework: PlannerAgent, ScraperAgent, ResponderAgent, AnalyzerAgent, NotificationAgent
- Multi-turn dialogue with Redis-backed session memory
- Hybrid keyword + vector search, built on the PostgreSQL + pgvector data layer (migrated from Pinecone by co-contributor Aqib)
- Redis TTL caching for LLM responses
- LLM-generated article summaries (Cohere with local DistilBART fallback)
- Per-article sentiment analysis via DistilBERT
- Dashboard home page: CVE Watchlist, Top News, filterable feed, Ask AI (single-turn, grounded per-article Q&A)
- Public landing page
- Sources management page (DB-backed, Redis-cached)
- Subscribe/unsubscribe routes and UI, with interest tags and daily/weekly digests (Aqib later contributed fixes to the unsubscribe flow)
- `/chat` and `/subscribe` UI, matching the approved Figma design
- 148 passing tests, verified running inside the actual Docker image (not just local dev environment)
- Fixed a real post-merge accuracy bug (Ask AI grounding on summary instead of content)
- Removed three layers of legacy pre-restructure code from the codebase
- Rewrote the README against verified current behavior, replaced all screenshots

# What left
As of this writing:
- PR #247 (legacy code cleanup) and PR #248 (README rewrite, further legacy removal, test/dependency fixes) are both open, pending mentor review
- No live-hosted demo: evaluated Vercel (architecturally incompatible - two of three services are long-running background workers, not serverless-compatible), then Neon + Render (workable, but api-service's combined ML model memory footprint exceeds free-tier RAM limits; the paid tier needed to fix this reliably was not pursued). Project runs fully via docker compose up locally instead, documented in the README.
- Final project demo video, in progress
- OTP verification for subscription signup was in the original proposal scope but descoped by mentor decision during the project
- CI/CD (GitHub Actions lint + test workflow) is Aqib's ownership area, in progress