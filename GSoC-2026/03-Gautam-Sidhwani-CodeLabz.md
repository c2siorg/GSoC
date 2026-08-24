# CodeLabz GSoC 2026

# Project Abstract

CodeLabz is an interactive, cloud-based learning platform built on React and Firebase. My GSoC project focused on hardening the platform for production use: adding role-based access control for organization settings, a real-time notifications system, a Dockerized local development environment, and a wave of bug fixes across authentication, tutorials, comments, and organization management. Given the size of the existing codebase, the originally planned TypeScript migration and UI/UX redesign were pushed out of scope mid-project, and the effort concentrated on correctness, access control, and developer experience instead.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/vfO7BcDX)

## [GSoC Project Proposal](https://drive.google.com/file/d/1aYWVuFd-0Ivg-33cXQbXnFqrq-5Ndbu5/view)

## [GitHub Organization Repo](https://github.com/c2siorg/Codelabz)

## [GitHub Personal Repo](https://github.com/gautamsidhwani29/Codelabz)

## [Commits during GSoC 2026](https://github.com/c2siorg/Codelabz/commits/develop/?author=gautamsidhwani29)

# Work Summary

The bulk of the project was three larger features plus a long tail of correctness fixes found while building and testing them.

**Role-based access control and admin dashboard** (PR [#421](https://github.com/c2siorg/Codelabz/pull/421)) added RBAC for organization settings, letting organization owners restrict who can edit org configuration instead of leaving it open to every member. The same PR added a platform-wide Admin Dashboard: live analytics widgets (user, org, and tutorial counts from Firestore), an audit log viewer scoped to an organization and its RBAC roles, and an org management table with search, pagination, and a force-unpublish control.

**Real-time notifications** (PR [#436](https://github.com/c2siorg/Codelabz/pull/436)) added a live notifications system so users see updates (comments, org activity) as they happen rather than on next page load.

**Local development infrastructure** (PR [#419](https://github.com/c2siorg/Codelabz/pull/419)) containerized the app and Firebase emulators with Docker, so contributors no longer need to hand-configure a local Firebase project to run the app.

**Collaborative editor migration** (PR [#454](https://github.com/c2siorg/Codelabz/pull/454)) replaced Quill with Tiptap for the tutorial editor and fixed the Yjs/Firestore emulator configuration backing real-time collaborative editing.

Alongside these, a series of bug fixes went in: dashboard validation and accessibility, organization delete cascade cleanup (orphaned users, stale Redux state), tutorial feed filtering and oversized Firestore query bounds, on-demand tutorial search indexing, auth reliability and emulator configuration, notification state initialization, and several small null-guard and callback-wiring fixes surfaced during review.

Toward the end of the project the codebase's MUI dependency was upgraded from v5 to v6 (PR [#452](https://github.com/c2siorg/Codelabz/pull/452)), missing dependencies were declared with the Node engine pinned and ESLint added (PR [#448](https://github.com/c2siorg/Codelabz/pull/448)), the Cloud Functions codebase was migrated to firebase-functions v2/gen2 (PR [#444](https://github.com/c2siorg/Codelabz/pull/444)), and dependency hygiene was closed out with non-breaking npm audit fixes (PR [#446](https://github.com/c2siorg/Codelabz/pull/446)) and removal of unused dependencies (PR [#450](https://github.com/c2siorg/Codelabz/pull/450)). A final docs pass (PR [#455](https://github.com/c2siorg/Codelabz/pull/455)) corrected stale Node and Java version requirements and Docker troubleshooting guidance left over from the earlier changes.

## Merged work

| PR                                                   | Work                                                                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [#416](https://github.com/c2siorg/Codelabz/pull/416) | Improved auth reliability and fixed emulator config                                                          |
| [#419](https://github.com/c2siorg/Codelabz/pull/419) | Containerized app and Firebase emulators for local development                                               |
| [#421](https://github.com/c2siorg/Codelabz/pull/421) | Implemented RBAC for org settings and a platform-wide admin dashboard (analytics, audit log, org management) |
| [#422](https://github.com/c2siorg/Codelabz/pull/422) | Improved dashboard validation logic and accessibility                                                        |
| [#424](https://github.com/c2siorg/Codelabz/pull/424) | Guarded `previewCanvasRef.current` before calling `getContext`                                               |
| [#426](https://github.com/c2siorg/Codelabz/pull/426) | Passed `handleCancel` to Dialog `onClose` instead of `!handleCancel`                                         |
| [#428](https://github.com/c2siorg/Codelabz/pull/428) | Initialized notification state with an empty array fallback                                                  |
| [#430](https://github.com/c2siorg/Codelabz/pull/430) | Cleaned up orphaned users and synced Redux state on org delete                                               |
| [#432](https://github.com/c2siorg/Codelabz/pull/432) | Returned `docref.id` from the addComment action                                                              |
| [#434](https://github.com/c2siorg/Codelabz/pull/434) | Used `docs.map` instead of `forEach` in a ViewOrganization query snapshot                                    |
| [#436](https://github.com/c2siorg/Codelabz/pull/436) | Implemented the real-time notifications system                                                               |
| [#442](https://github.com/c2siorg/Codelabz/pull/442) | Repaired the tutorial feed filter and bounded oversized Firestore queries                                    |
| [#443](https://github.com/c2siorg/Codelabz/pull/443) | Built the tutorial search index on demand instead of at app start                                            |
| [#448](https://github.com/c2siorg/Codelabz/pull/448) | Declared missing dependencies, pinned Node engine, added ESLint                                              |
| [#452](https://github.com/c2siorg/Codelabz/pull/452) | Upgraded MUI to v6 and fixed theme resolution                                                                |
| [#444](https://github.com/c2siorg/Codelabz/pull/444) | Migrated Cloud Functions to firebase-functions v2 (gen2)                                                     |
| [#446](https://github.com/c2siorg/Codelabz/pull/446) | Non-breaking npm audit fixes                                                                                 |
| [#450](https://github.com/c2siorg/Codelabz/pull/450) | Removed unused dependencies                                                                                  |
| [#454](https://github.com/c2siorg/Codelabz/pull/454) | Replaced Quill with Tiptap for the collaborative tutorial editor, fixed Yjs emulator config                  |
| [#455](https://github.com/c2siorg/Codelabz/pull/455) | Corrected stale Node/Java version requirements and Docker troubleshooting guidance in the docs               |

# What Covered

Mapped against the deliverables from the proposal:

- **Enhanced data security and privacy** - role-based access control for organization settings, restricting sensitive org configuration to authorized users (PR [#421](https://github.com/c2siorg/Codelabz/pull/421))
- **Improved admin functionality** - a platform-wide Admin Dashboard with live analytics widgets (user, org, and tutorial counts), an RBAC-aware audit log viewer per organization, and an org management table with search, pagination, and a force-unpublish control (PR [#421](https://github.com/c2siorg/Codelabz/pull/421))
- **Real-time backend** - real-time notifications system (PR [#436](https://github.com/c2siorg/Codelabz/pull/436)), plus Yjs-backed real-time sync for the collaborative tutorial editor (PR [#454](https://github.com/c2siorg/Codelabz/pull/454))
- **Refined Local Environment**, more consistent and reproducible environments - Dockerized app and Firebase emulator setup for local development (PR [#419](https://github.com/c2siorg/Codelabz/pull/419)), CI Node engine bumped from 18 to 22 (PRs [#444](https://github.com/c2siorg/Codelabz/pull/444), [#446](https://github.com/c2siorg/Codelabz/pull/446))
- **Optimized data retrieval** (part of the API performance goal) - bounded oversized Firestore queries and repaired the tutorial feed filter (PR [#442](https://github.com/c2siorg/Codelabz/pull/442)), tutorial search index built on demand instead of at app start (PR [#443](https://github.com/c2siorg/Codelabz/pull/443))
- **Codebase updates** (partial progress toward a fully consistent codebase) - MUI v5 to v6 upgrade (PR [#452](https://github.com/c2siorg/Codelabz/pull/452)), Cloud Functions migrated to firebase-functions v2/gen2 (PR [#444](https://github.com/c2siorg/Codelabz/pull/444)), dependency hygiene: missing deps declared, ESLint added, npm audit fixes, unused dependencies removed (PRs [#448](https://github.com/c2siorg/Codelabz/pull/448), [#446](https://github.com/c2siorg/Codelabz/pull/446), [#450](https://github.com/c2siorg/Codelabz/pull/450))

# What left

- **Better-looking, responsive UI/UX** - not delivered; pushed out of scope mid-project given the size of the existing codebase
- **Fully migrated, consistent codebase** - only partial: the TypeScript migration didn't happen, and deprecated `@mui/styles` usage remains across the codebase after the v6 upgrade
- Broader API-level performance work beyond the Firestore query fixes already covered (caching, response time monitoring, server load reduction)
