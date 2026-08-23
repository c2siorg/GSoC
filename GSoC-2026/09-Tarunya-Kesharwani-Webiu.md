# Project Name
Webiu 2.0 & Webiu CLI (`create-webiu`) - Open Source Project Intelligence Platform & Community Portal Scaffolding Engine

## Contributor Info
- **Name**: Tarunya Kesharwani (Tarunya Kesh)
- **GitHub Profile**: [https://github.com/TarunyaProgrammer](https://github.com/TarunyaProgrammer)
- **NPM Package**: [https://www.npmjs.com/package/create-webiu](https://www.npmjs.com/package/create-webiu)
- **Medium**: [https://tarunyakesh.medium.com/](https://tarunyakesh.medium.com/)
- **LinkedIn**: [https://www.linkedin.com/in/tarunyakesharwani/](https://www.linkedin.com/in/tarunyakesharwani/)

# Project Abstract

**Webiu 2.0** is an open-source community portal and repository intelligence platform developed for the **Ceylon Computer Science Institute (C2SI)** and **SCoRe Lab**. The platform provides open-source organizations with real-time project metrics (stars, forks, open issues, pull requests, tech stack distribution), dynamic contributor showcases, GSoC project idea management, community publication archives, and an administrative governance dashboard.

During **Google Summer of Code 2026**, the project achieved two major engineering breakthroughs:
1. **Fullstack Architecture & Synchronization Engine (`webiu-server` & `webiu-ui`)**: Migrated Webiu from on-demand client-side API requests into an enterprise-grade full-stack architecture built with **NestJS**, **PostgreSQL**, and **TypeORM**. Designed a hybrid synchronization pipeline utilizing real-time **GitHub Webhooks** (`X-Hub-Signature-256` validated) combined with background **reconciliation cron workers** to eliminate API rate-limiting and data drift. Implemented an Admin Suite featuring JWT/Session security, rate-limiting, audit logging, GSoC Ideas CMS, and contributor intelligence analytics.
2. **Official Scaffolding CLI (`create-webiu` on npm)**: Architected and published a standalone TypeScript CLI tool enabling community organizations to scaffold, configure, containerize, and deploy their own customized Webiu portals in under five minutes with interactive theming, navbar module selection, automated Docker PostgreSQL configuration, and diagnostic doctor utilities.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/zuLPFjoe)

## [GSoC Project Proposal](https://drive.google.com/file/d/1kN956mpM9PQ5Lof8wJPBcU06vadIuFAl/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/Webiu)

## [GitHub Personal Repo](https://github.com/TarunyaProgrammer/Webiu)

## [Commits during GSoC 2026](https://github.com/c2siorg/Webiu/commits?author=TarunyaProgrammer)

## [Project Demo Video](https://youtu.be/JrcEcwNaZ98)

## [Project Wiki](https://github.com/c2siorg/Webiu/wiki)

## [GSoC Blog](https://tarunyakesh.medium.com/)

# Work Summary

### Pull Requests Merged during GSoC 2026

| **PR** | **Description** | **Date Merged** |
| :--- | :--- | :--- |
| [#733](https://github.com/c2siorg/Webiu/pull/733) | `fix(cli)`: CLI security audit, parallelized npm installs, Homebrew-style doctor diagnostics, background update checks | ✅ Aug 05, 2026 |
| [#731](https://github.com/c2siorg/Webiu/pull/731) | `feat(cli)`: Complete CLI scaffolding overhaul with dynamic theme engine, navbar toggles, terminal UI & preview assets | ✅ Jul 31, 2026 |
| [#722](https://github.com/c2siorg/Webiu/pull/722) | `feat(cli)`: Published `create-webiu` CLI scaffolding package, init/dev/docker commands, subcommands manual | ✅ Jul 30, 2026 |
| [#719](https://github.com/c2siorg/Webiu/pull/719) | `feat(ui)`: Redesign footer with interactive garden animations and full-width card layout | ✅ Jul 19, 2026 |
| [#713](https://github.com/c2siorg/Webiu/pull/713) | `feat(admin)`: Redesign sidebar navigation, nested admin layout, opportunities module, and audit log UI | ✅ Jul 03, 2026 |
| [#711](https://github.com/c2siorg/Webiu/pull/711) | `refactor`: Address visual contrast, WCAG AA a11y, NG8107 template nullability, architecture & UX improvements | ✅ Jul 03, 2026 |
| [#709](https://github.com/c2siorg/Webiu/pull/709) | `fix`: Resolve memory leaks and unhandled subscription leaks in search, admin dashboard, and animation directives | ✅ Jul 01, 2026 |
| [#707](https://github.com/c2siorg/Webiu/pull/707) | `perf`: Optimize Three.js animation cycles, bulk fetch PR counts via GraphQL, and lazy-load contributor statistics | ✅ Jul 01, 2026 |
| [#705](https://github.com/c2siorg/Webiu/pull/705) | `security`: Enforce strict rate limits on admin routes, sanitize GSoC details HTML, and resolve contrast bugs | ✅ Jul 01, 2026 |
| [#703](https://github.com/c2siorg/Webiu/pull/703) | `refactor`: Resolve critical logic bugs, security vulnerabilities, and startup performance bottlenecks | ✅ Jul 01, 2026 |
| [#694](https://github.com/c2siorg/Webiu/pull/694) | `feat`: Frontend performance optimization, CLS/LCP Lighthouse audit score improvements, and leaner bundles | ✅ Jun 30, 2026 |
| [#691](https://github.com/c2siorg/Webiu/pull/691) | `feat(analytics)`: Implement repository intelligence dashboard and real-time synchronization updates | ✅ Jun 29, 2026 |
| [#689](https://github.com/c2siorg/Webiu/pull/689) | `feat`: Implement admin contributor intelligence dashboard with chart visualizations (ng2-charts Angular 17) | ✅ Jun 29, 2026 |
| [#686](https://github.com/c2siorg/Webiu/pull/686) | `feat(admin-dashboard)`: Implement aggregated dashboard service and redesigned operational control panel | ✅ Jun 29, 2026 |
| [#684](https://github.com/c2siorg/Webiu/pull/684) | `feat(project-details)`: Replace heavy Three.js 3D orbit model with high-performance responsive SVG dashboard | ✅ Jun 29, 2026 |
| [#681](https://github.com/c2siorg/Webiu/pull/681) | `fix(project)`: Optimize login writes, handle username uniqueness exceptions, and add PR description checklist | ✅ Jun 28, 2026 |
| [#680](https://github.com/c2siorg/Webiu/pull/680) | `fix(project)`: Implement frontend caching service, build-time API environment configuration, and CORS docs | ✅ Jun 28, 2026 |
| [#679](https://github.com/c2siorg/Webiu/pull/679) | `fix(server)`: Implement backend enforcement for maintenance mode with `MaintenanceGuard` | ✅ Jun 28, 2026 |
| [#678](https://github.com/c2siorg/Webiu/pull/678) | `fix(server)`: Resolve GitHub API rate limits, backoff retry handling, and repository sync race conditions | ✅ Jun 28, 2026 |
| [#677](https://github.com/c2siorg/Webiu/pull/677) | `fix(server)`: Resolve deployment database migrations, SSL configurations, and environment startup validations | ✅ Jun 28, 2026 |
| [#676](https://github.com/c2siorg/Webiu/pull/676) | `feat(auth)`: Enable reverse proxy trust, timing attack protection on authentication, and dedicated rate limits | ✅ Jun 28, 2026 |
| [#675](https://github.com/c2siorg/Webiu/pull/675) | `feat(auth)`: JWT lifecycle security, refresh token rotation, and cookie revocation handling | ✅ Jun 27, 2026 |
| [#674](https://github.com/c2siorg/Webiu/pull/674) | `feat(auth)`: Secure HTTP-only session cookie configuration with SameSite attributes | ✅ Jun 26, 2026 |
| [#673](https://github.com/c2siorg/Webiu/pull/673) | `feat(ui)`: V2 premium redesign with 3D elements, glassmorphism tokens, and responsive mobile drawers | ✅ Jun 26, 2026 |
| [#672](https://github.com/c2siorg/Webiu/pull/672) | `feat(ui)`: Webiu visual overhaul (Hero section, typography, community highlights, and brand identity) | ✅ Jun 23, 2026 |
| [#662](https://github.com/c2siorg/Webiu/pull/662) | `feat(audit)`: Enterprise audit logging module capturing administrator modifications, timestamps, and IP origins | ✅ Jun 23, 2026 |
| [#660](https://github.com/c2siorg/Webiu/pull/660) | `feat(admin)`: Admin profile management, avatar updates, credential changes, and session invalidation | ✅ Jun 21, 2026 |
| [#658](https://github.com/c2siorg/Webiu/pull/658) | `docs`: GSoC CMS architectural documentation, database ER diagrams, and REST/GraphQL API specifications | ✅ Jun 20, 2026 |
| [#657](https://github.com/c2siorg/Webiu/pull/657) | `feat(gsoc)`: GSoC Ideas CMS module allowing administrators to manage project ideas, tech tags, and mentor details | ✅ Jun 19, 2026 |
| [#654](https://github.com/c2siorg/Webiu/pull/654) | `feat(settings)`: System settings module for organization metadata, theme colors, and portal maintenance flags | ✅ Jun 17, 2026 |
| [#653](https://github.com/c2siorg/Webiu/pull/653) | `feat(contributors)`: Contributor persistence layer, GitHub GraphQL metrics aggregation, and avatar caching | ✅ Jun 16, 2026 |
| [#652](https://github.com/c2siorg/Webiu/pull/652) | `feat(contributors)`: Database schema definitions and relations for contributor statistics and commit tracking | ✅ Jun 16, 2026 |
| [#650](https://github.com/c2siorg/Webiu/pull/650) | `feat(sync)`: Resilient background repository reconciliation cron engine with idempotency keys | ✅ Jun 16, 2026 |
| [#648](https://github.com/c2siorg/Webiu/pull/648) | `feat(webhook)`: GitHub Webhook ingestion controller with HMAC SHA-256 signature verification | ✅ Jun 15, 2026 |
| [#646](https://github.com/c2siorg/Webiu/pull/646) | `feat(projects)`: Repository metadata persistence service for tracking stars, forks, languages, and open issues | ✅ Jun 15, 2026 |
| [#644](https://github.com/c2siorg/Webiu/pull/644) | `feat(database)`: PostgreSQL + TypeORM foundation with automatic migration runners and environment schemas | ✅ Jun 13, 2026 |
| [#642](https://github.com/c2siorg/Webiu/pull/642) | `feat(auth)`: Admin authentication foundation (JWT Strategy, Passport, Bcrypt password hashing, Guards) | ✅ Jun 11, 2026 |
| [#640](https://github.com/c2siorg/Webiu/pull/640) | `chore(deploy)`: Render deployment blueprints (`render.yaml`), multi-stage Dockerfiles, and environment templates | ✅ Jun 10, 2026 |
| [#638](https://github.com/c2siorg/Webiu/pull/638) | `chore`: Monorepo hygiene, dependency alignment, ESLint configuration, and TypeScript strict mode fixes | ✅ Jun 06, 2026 |
| [#634](https://github.com/c2siorg/Webiu/pull/634) | `chore`: Extracted hardcoded static projects JSON into structured relational database seeds | ✅ Jun 04, 2026 |
| [#633](https://github.com/c2siorg/Webiu/pull/633) | `chore`: Removed legacy SSR static deployment blockers to establish clean Angular client-side build pipeline | ✅ Jun 04, 2026 |

---

### Pre-GSoC Community Bonding & Core Contributions

| **PR** | **Description** | **Date Merged** |
| :--- | :--- | :--- |
| [#456](https://github.com/c2siorg/Webiu/pull/456) | `feat`: Project details page contributor integration and real-time metric display | ✅ Feb 27, 2026 |
| [#443](https://github.com/c2siorg/Webiu/pull/443) | `refactor`: Restructure and expose Opportunities and GSoC program navigation | ✅ Feb 27, 2026 |
| [#453](https://github.com/c2siorg/Webiu/pull/453) | `fix`: Publication page card layout, responsive grids, and link handling | ✅ Feb 26, 2026 |
| [#375](https://github.com/c2siorg/Webiu/pull/375) | `fix`: Angular RxJS subscription cleanup using `takeUntilDestroyed` to prevent leaks | ✅ Feb 26, 2026 |
| [#432](https://github.com/c2siorg/Webiu/pull/432) | `feat`: Project details insights panel and repository metadata charts | ✅ Feb 25, 2026 |
| [#401](https://github.com/c2siorg/Webiu/pull/401) | `feat`: Project details base view and responsive layout scaffolding | ✅ Feb 24, 2026 |
| [#377](https://github.com/c2siorg/Webiu/pull/377) | `feat`: Dynamic routing and parameter resolution for individual project pages | ✅ Feb 22, 2026 |
| [#372](https://github.com/c2siorg/Webiu/pull/372) | `bug`: Resolved community Slack and Discord dynamic URL redirection bugs | ✅ Feb 22, 2026 |
| [#259](https://github.com/c2siorg/Webiu/pull/259) | `refactor`: Overhauled community page layout, member cards, and social links | ✅ Feb 21, 2026 |
| [#285](https://github.com/c2siorg/Webiu/pull/285) | `feat`: Created interactive 404 error page with mascot and quick navigation | ✅ Feb 21, 2026 |
| [#287](https://github.com/c2siorg/Webiu/pull/287) | `chore`: Established standardized GitHub issue templates and PR checklists | ✅ Feb 21, 2026 |
| [#224](https://github.com/c2siorg/Webiu/pull/224) | `bug`: Fixed mobile navigation drawer backdrop and focus traps | ✅ Feb 21, 2026 |
| [#241](https://github.com/c2siorg/Webiu/pull/241) | `feat`: Added responsive organization footer with links and copyright notice | ✅ Feb 20, 2026 |
| [#240](https://github.com/c2siorg/Webiu/pull/240) | `feat`: Updated GSoC ideas portal with project tracks and application criteria | ✅ Feb 20, 2026 |
| [#219](https://github.com/c2siorg/Webiu/pull/219) | `feat`: Improved repository filter search by tech stack and category | ✅ Feb 19, 2026 |

---

# What Covered

### 1. `create-webiu` NPM Scaffolding CLI Engine
- **Global NPM Package**: Published [`create-webiu`](https://www.npmjs.com/package/create-webiu) (v2.2.0) with multi-binary alias (`webiu` and `create-webiu`).
- **Interactive Wizard (`webiu init`)**: Complete CLI prompt engine supporting Organization Types, GitHub handle ingestion, automated Docker PostgreSQL container bootstrapping, 6 dynamic theme color swatches, and selective navbar module toggling.
- **Developer Orchestrator (`webiu dev`)**: Multi-process orchestration launching Angular frontend and NestJS backend concurrently with unified logs.
- **Diagnostic Health Checker (`webiu doctor`)**: Homebrew-style system diagnostic tool verifying Node.js, npm, Docker, Git, and network port availability.
- **Containerization & Deployment (`webiu docker` & `webiu deploy`)**: Automated generation of `docker-compose.yml`, environment configurations, and build pipelines.

### 2. Backend Architecture (`webiu-server`)
- **Persistence Layer**: Implemented PostgreSQL database integration with TypeORM migrations, entity relations, and connection pooling.
- **Hybrid Data Synchronization**: Built a dual-layer GitHub synchronization architecture combining real-time Webhook event ingestion (`X-Hub-Signature-256`) with background reconciliation cron jobs using idempotency keys.
- **Security & Authentication**: Enforced JWT lifecycle management, HTTP-only SameSite cookies, Bcrypt password hashing, reverse proxy trust headers, rate-limiting guards (`ThrottlerGuard`), and timing-attack protections.
- **Governance Modules**: Built an Audit Logging system tracking administrative activities, System Settings service for portal customizability, GSoC Ideas CMS, and Contributor Analytics.

### 3. Frontend Architecture (`webiu-ui`)
- **Angular 17+ Modernization**: Built scalable standalone component architecture with SCSS tokens, signals, and dynamic theme switching.
- **High-Performance Project & Contributor Dashboards**: Replaced CPU-heavy 3D canvas models with optimized responsive SVG visualizations and integrated `ng2-charts` analytics.
- **Accessibility & UX Polish**: Achieved WCAG 2.1 AA compliance, resolved subscription memory leaks using Angular lifecycle destroy hooks, standardized dark/light mode CSS custom properties, and boosted Lighthouse performance scores.

---

# What left

- **Omission of Redis & BullMQ (Deliberate Architectural Decision)**: While initially evaluated for asynchronous message queuing and caching, external Redis and BullMQ infrastructure were deliberately omitted. For the current organizational scale, leveraging NestJS in-memory cron scheduling and PostgreSQL indexing provides sub-millisecond response times without the unnecessary operational complexity, memory overhead, and hosting costs of managing a dedicated Redis cluster.
