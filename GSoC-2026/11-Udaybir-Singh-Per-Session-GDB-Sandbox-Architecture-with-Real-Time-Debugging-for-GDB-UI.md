# GDB-UI

Udaybir Singh - [@Uday9909](https://github.com/Uday9909)

Mentor: Shubh Mehta - [@Shubh942](https://github.com/Shubh942)

# Project Abstract

GDB-UI is a browser-based interface for GDB that lets developers debug C/C++ programs visually instead of through the command line, setting breakpoints, inspecting variables, and stepping through execution from a web app.

Before GSoC 2026, GDB-UI supported only one user at a time. The backend held a single global GDB controller shared across every request, so a second user's request would silently kill the first user's debugging session. The goal of this year's project was to fix that at the architecture level and build the infrastructure that a real multi-user tool needs on top of it: per-session isolation, real-time output streaming over WebSockets, and sandboxed execution so untrusted code never touches the host.

## [GSoC Project Page](https://summerofcode.withgoogle.com/myprojects/details/6Avhxr1h)

## [GSoC Project Proposal](https://docs.google.com/document/d/1l1DPFntJETThfnQPHuxcohKt0_HLPpEw/edit?usp=sharing&ouid=111056193281989022097&rtpof=true&sd=true)

## [GitHub Organization Repo](https://github.com/c2siorg/GDB-UI)

## [GitHub Personal Repo](https://github.com/Uday9909/GDB-UI/tree/main)

## [Commits during GSoC 2026](https://github.com/c2siorg/GDB-UI/commits/main/?author=Uday9909)

## [Project Wiki](https://github.com/c2siorg/GDB-UI/blob/main/README.md)

## [GSoC Blog](https://medium.com/@udaybir/google-summer-of-code26-with-c2siorg-e05c6091dd44?sharedUserId=udaybir)

# Work Summary

## Milestone 1 — Per-session isolation

| **Description** | **PR** | **Merged** |
|------------|----|---------|
| Home and Login pages with routing | [#95](https://github.com/c2siorg/GDB-UI/pull/95) | ✅ |
| React 18 migration, `ReactDOM.render` → `createRoot` | [#96](https://github.com/c2siorg/GDB-UI/pull/96) | ✅ |
| Connected Threads API to the backend | [#118](https://github.com/c2siorg/GDB-UI/pull/118) | ✅ |
| Replaced global `gdb_controller` with per-session `SessionManager` | [#131](https://github.com/c2siorg/GDB-UI/pull/131) | ✅ |
| Addressed review feedback: DRY'd up 10 GDB routes, fixed `info locals` | [#205](https://github.com/c2siorg/GDB-UI/pull/205) | ✅ |

## Milestone 2 — Real-time output streaming

| **Description** | **PR** | **Merged** |
|------------|----|---------|
| WebSocket foundation: Flask-SocketIO, `/ws/debug` namespace, `ws_token` auth | [#207](https://github.com/c2siorg/GDB-UI/pull/207) | ✅ |
| Per-session reader greenlet streaming GDB output | [#208](https://github.com/c2siorg/GDB-UI/pull/208) | ✅ |
| Socket.IO client hook (`useStreamingOutput`), 1000-line buffer cap | [#209](https://github.com/c2siorg/GDB-UI/pull/209) | ✅ |
| WebSocket integration tests via in-process `SocketIOTestClient` | [#210](https://github.com/c2siorg/GDB-UI/pull/210) | ✅ |

## Milestone 3 — Docker sandbox

| **Description** | **PR** | **Merged** |
|------------|----|---------|
| Docker sandbox infrastructure: read-only, no network, non-exec tmpfs | [#211](https://github.com/c2siorg/GDB-UI/pull/211) | ✅ |
| Wired sandbox containers into session lifecycle (GDB via `docker exec`) | [#212](https://github.com/c2siorg/GDB-UI/pull/212) | ✅ |
| Compilation inside the sandbox, idempotent container start, fail-closed | [#213](https://github.com/c2siorg/GDB-UI/pull/213) | ✅ |

# What Covered

## 1. **Per-session isolation**
Replaced the single global `gdb_controller` with a `SessionManager` mapping each session to its own GDB controller and token. This was the architectural fix everything else depended on. Locking is split between a global lock for dictionary mutations and a per-session `RLock` for GDB I/O, with `controller.write()` never held under the global lock, so one session's slow call can't block another session.

## 2. **Real-time output streaming**
Replaced polling with Flask-SocketIO. A background greenlet per session reads GDB's output and emits it to the browser over a dedicated `/ws/debug` namespace. The main implementation issue was that gevent's monkey-patching interferes with pygdbmi's subprocess pipes; patching everything hangs GDB I/O outright, so patching is selective (`subprocess`, `select`, and `os` left unpatched). Tests run through an in-process `SocketIOTestClient`, which exercises the real dispatch path without a live server.

## 3. **Sandboxed execution**
The session/command-blocklist model still left a gap: GDB's own expression evaluator can run `call system("...")`, which walks past a command-level blocklist entirely. Docker sandboxing closes that gap. GDB and compilation both now run inside a locked-down container (`--read-only`, `--network none`, non-executable tmpfs) via `docker exec`, with idempotent container startup and a fail-closed response if compilation fails.

## 4. **Session security**
Timing-safe `ws_token` comparison (`secrets.compare_digest`), a blocklist for shell-adjacent GDB commands, UUID4 session and token generation, and automatic session expiry on a fixed TTL with a background sweep.

# What is left

- **CI gates and coverage enforcement aren't live yet.** #215 (lint/build CI, ruff job) and #216 (80% coverage threshold) are open. The frontend test suite and coverage numbers exist, but they aren't enforced as a merge gate on `main` until these land.
- **UI polish is unmerged.** #214 fixes a handful of small issues (a typo, stray console.logs, missing aria-labels) that are cosmetic but still open on `main`.
- **README is stale on sandbox mode.** It still describes Docker sandboxing as a future phase rather than a shipped feature; needs an update to match #211–#213.
- **Sandbox mode is opt-in, not default.** `GDBUI_DOCKER` defaults to `false`, so a fresh deployment still runs GDB directly on the host unless explicitly configured into sandboxed mode.

# Acknowledgements

Thank you to my mentor, Shubh Mehta, for the guidance and feedback throughout the summer.

Thanks to C2SI for the opportunity to work on infrastructure that had to hold up under real concurrent use, not just a single-user prototype.