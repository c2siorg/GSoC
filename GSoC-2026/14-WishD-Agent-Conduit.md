# Agent Conduit

# Project Abstract

Agent Conduit is a lightweight, self-hosted, unified gateway for AI agents. It gives every agent a
cryptographic identity (AAP-compliant), stores and governs the credentials agents use to call external
platforms (Slack, GitHub, Google, any REST/GraphQL API), serves tool schemas on demand, and records every
action in a per-agent audit log. Credentials are encrypted at rest and injected server-side, so agents never
hold a raw token.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/9YbM89YA)

## [GSoC Project Proposal](https://drive.google.com/file/d/18CqTxangVGsC_c0K7BpGcpczwC-dxAXr/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/Agent-Conduit)

## [GitHub Personal Repo](https://github.com/wwishd/Agent-Conduit)

## Pull Requests during GSoC 2026

- [PR #1](https://github.com/c2siorg/Agent-Conduit/pull/1)
- [PR #2](https://github.com/c2siorg/Agent-Conduit/pull/2)
- [PR #3](https://github.com/c2siorg/Agent-Conduit/pull/3)
- [PR #4](https://github.com/c2siorg/Agent-Conduit/pull/4)
- [PR #5](https://github.com/c2siorg/Agent-Conduit/pull/5)
- [PR #6](https://github.com/c2siorg/Agent-Conduit/pull/6)
- [PR #7](https://github.com/c2siorg/Agent-Conduit/pull/7)
- [PR #8](https://github.com/c2siorg/Agent-Conduit/pull/8)

# Work Summary

Built Agent Conduit end to end around four pillars that share a single agent JWT:

1. Identity Server — per-agent Ed25519 identity, JWT issuance, and full lifecycle, with a 5-stage JWT
   verification pipeline (type, signature, claims/replay, state, capability + constraints).
2. Connection Registry — encrypted credential store (AES-256-GCM) with pluggable platform connectors;
   credentials are injected server-side and never returned to the agent.
3. Token Router — on-demand, identity-scoped tool-schema serving.
4. Observability & Audit — per-agent audit log and security event stream.

Also delivered the admin dashboard, the `conduit` CLI (including `conduit run`), the `conduit-client` SDK,
PostgreSQL storage behind a pluggable StorageDriver, Docker deployment, and runnable examples.

# What Covered

- AAP identity model (host/agent), Ed25519 JWTs, lifecycle, key rotation, jti replay protection.
- 5-stage JWT security pipeline and constraint engine.
- Connection Registry with 45+ platform connectors + generic REST/GraphQL; AES-256-GCM credential encryption.
- Capability grants with constraints, connection grants (access wiring), and a declarative execution policy
  (allow / deny / require-approval).
- Per-project credential isolation (Projects).
- Token Router with per-tool schema cache.
- Audit log + security event stream; denials audited with hashed args.
- Admin dashboard: agents, projects, connections, access wiring, execution policy, tools, audit, per-agent
  detail view, and a password login gate.
- `conduit` CLI (transparent `conduit run` identity proxy + admin commands) and `conduit-client` SDK, both
  published as self-contained npm packages.
- PostgreSQL storage driver + migrations, Docker Compose deployment, CI, and example agents (Slack copilot,
  terminal Claude agent).

# What Left

- MySQL storage driver (currently a stub proving the abstraction).
- Transparent network-layer egress interception for `conduit run` (govern unmodified agents).
- MCP server (`conduit-mcp`) to plug Conduit into editor agents (Cursor, Claude Code, Codex).
- Remaining AAP conformance items (host linking/claiming, CIBA approvals, full error envelope).
