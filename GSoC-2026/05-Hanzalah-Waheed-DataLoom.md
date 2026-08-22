# DataLoom

Hanzalah Waheed - [@hanzalahwaheed](https://github.com/hanzalahwaheed)

Mentor: Oshan Mudannayake - [@ivantha](https://github.com/ivantha)

# Project Abstract

DataLoom is a web GUI for pandas. A user uploads a tabular file, applies transformations through forms instead of writing Python code, and uses checkpoints to save and revert changes. The goal of the project is to make common data preparation tasks accessible without requiring the user to write pandas code.

Every upload keeps the original file unchanged and maintains a working copy where transformations are applied. Each transformation is logged together with its parameters, so a project state can be reconstructed from the original file and the ordered list of transformations. This is also what lets checkpoints and revert work without needing a separate inverse operation for every transformation.

DataLoom already had a solid MVP before GSoC 2026. The goal of this year's project was to build on that foundation and turn it into a more complete data preparation platform: multi-format I/O, data profiling, a data quality engine with remediation, charts, formula columns, reusable pipelines, multi-file projects, PDF reports, a rebuilt workspace interface, and a migration of the frontend to TypeScript.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/PnJGdWrY)

## [GSoC Project Proposal](https://drive.google.com/file/d/17oasy-QceKcxYHO-ZOexrZbBi0wHJrVv/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/dataloom)

## [GitHub Personal Repo](https://github.com/hanzalahwaheed/dataloom)

## [Commits during GSoC 2026](https://github.com/c2siorg/dataloom/commits/main/?author=hanzalahwaheed)

## [Project Demo Video](https://youtu.be/jSJ7cc0Gcr0)

## [Project Wiki](https://github.com/c2siorg/dataloom/blob/main/README.md)

## [GSoC Blog](https://medium.com/@hanzalahwaheed)

# Work Summary

## Pre-GSoC work

I started contributing to DataLoom in February 2026, during the application and community bonding periods. This work helped me understand the codebase before the coding period started.

| **Description** | **PR** | **Merged** |
|------------|----|---------|
| Unified transform endpoint | [#108](https://github.com/c2siorg/dataloom/pull/108) | ✅ |
| Shared form-error component and error hook | [#111](https://github.com/c2siorg/dataloom/pull/111) | ✅ |
| dtype badges on column headers | [#116](https://github.com/c2siorg/dataloom/pull/116) | ✅ |
| Active transform button highlight | [#120](https://github.com/c2siorg/dataloom/pull/120) | ✅ |
| Table bottom padding | [#121](https://github.com/c2siorg/dataloom/pull/121) | ✅ |
| String replace transformation | [#126](https://github.com/c2siorg/dataloom/pull/126) | ✅ |
| Dockerfiles for both services | [#213](https://github.com/c2siorg/dataloom/pull/213) | ✅ |
| Authentication and per-user projects | [#299](https://github.com/c2siorg/dataloom/pull/299) | ✅ |
| Migration docs in `CONTRIBUTING.md` | [#305](https://github.com/c2siorg/dataloom/pull/305) | ✅ |

## Coding-period deliverables

| **Description** | **PR** | **Merged** |
|------------|----|---------|
| Backend operation registry for transformation dispatch and replay | [#324](https://github.com/c2siorg/dataloom/pull/324) | ✅ |
| Multi-format import: TSV, JSON, XLSX, Parquet | [#325](https://github.com/c2siorg/dataloom/pull/325) | ✅ |
| Multi-format export | [#333](https://github.com/c2siorg/dataloom/pull/333) | ✅ |
| Format-specific export options: delimiters, headers, encoding | [#344](https://github.com/c2siorg/dataloom/pull/344) | ✅ |
| Data profiling backend: dataset summary, column profiles, correlation matrix | [#369](https://github.com/c2siorg/dataloom/pull/369) | ✅ |
| Searchable, type-aware column selectors in transformation forms | [#382](https://github.com/c2siorg/dataloom/pull/382) | ✅ |
| Column selectors across the remaining forms | [#389](https://github.com/c2siorg/dataloom/pull/389) | ✅ |
| Rebuilt table: frozen header, serial number column, dtype row | [#394](https://github.com/c2siorg/dataloom/pull/394) | ✅ |
| Data profiling frontend: column stats cards, summary tab, correlation heatmap | [#396](https://github.com/c2siorg/dataloom/pull/396) | ✅ |
| Workspace layout with ribbon, tab strip, docked panel, and frontend feature registry | [#401](https://github.com/c2siorg/dataloom/pull/401) | ✅ |
| Charts: six chart types with dtype-based suggestions | [#407](https://github.com/c2siorg/dataloom/pull/407) | ✅ |
| Multi-file projects: append another file with preview | [#422](https://github.com/c2siorg/dataloom/pull/422) | ✅ |
| TypeScript migration: forms and lint wiring | [#438](https://github.com/c2siorg/dataloom/pull/438) | ✅ |
| Data quality engine with remediation flow | [#444](https://github.com/c2siorg/dataloom/pull/444) | ✅ |
| Formula columns | [#463](https://github.com/c2siorg/dataloom/pull/463) | ✅ |
| Reusable pipelines | [#474](https://github.com/c2siorg/dataloom/pull/474) | ✅ |
| Downloadable PDF reports | [#482](https://github.com/c2siorg/dataloom/pull/482) | ✅ (rebased into `main` as [`a43de30`](https://github.com/c2siorg/dataloom/commit/a43de30)) |
| TypeScript migration: utilities and configuration | [#483](https://github.com/c2siorg/dataloom/pull/483) | ✅ |
| TypeScript migration: remaining files | [#484](https://github.com/c2siorg/dataloom/pull/484) | 🔄 Open |
| TypeScript migration: contexts and hooks | [#485](https://github.com/c2siorg/dataloom/pull/485) | ✅ |

## Community collaboration

A significant part of the GSoC period was spent reviewing and supporting other contributions to the project:

| **Description** | **PR** |
|------------|----|
| Application-wide dark mode | [#432](https://github.com/c2siorg/dataloom/pull/432) |
| Unified settings page | [#397](https://github.com/c2siorg/dataloom/pull/397) |
| Forgot-password and reset flow | [#326](https://github.com/c2siorg/dataloom/pull/326) |
| Project search | [#385](https://github.com/c2siorg/dataloom/pull/385) |
| Pagination improvements | [#391](https://github.com/c2siorg/dataloom/pull/391) |
| Apply step for transformations, suggested during review of [#409](https://github.com/c2siorg/dataloom/pull/409) | [#410](https://github.com/c2siorg/dataloom/pull/410) |

One review led to a feature I did not implement myself. In [#409](https://github.com/c2siorg/dataloom/pull/409), the original issue was that cancelling GroupBy did not properly revert the data. Instead of treating it as only a bug fix, I suggested introducing an explicit Apply step for transformations. That idea was implemented across the application in [#410](https://github.com/c2siorg/dataloom/pull/410), which established the preview-before-persist behaviour now used throughout DataLoom.

I also worked closely with two new contributors who are now active in the repository, including a call to walk through the project structure, and I opened 34 issues during the period, most of them detailed enough for other contributors to pick up.

# What was Covered

## 1. **Groundwork: two registries** 
Adding a transformation previously required changes in an enum, a set of complex operations, several conditional branches, and the replay logic. [#324](https://github.com/c2siorg/dataloom/pull/324) introduced a backend operation registry where each operation defines its handler, its parameter field, how its arguments are built, and whether it can be replayed. Three dispatch locations now read from the same registry, and an import-time check catches missing entries at startup. [#401](https://github.com/c2siorg/dataloom/pull/401) introduced a matching registry for frontend features. Both changes made the later features much cheaper to add.

## 2. **Multi-format import and export** 
TSV, JSON, XLSX, and Parquet are supported. A format registry maps each extension to its reader, writer, and media type, and the working copy stays in its original format instead of being converted to one common format. Export supports format-specific options such as delimiters, headers, and encoding. For JSON, nested object handling is deliberately limited to one level.

## 3. **Data profiling** 
Dataset summaries, per-column profiles, and a correlation matrix. Profiling is built for real-world data, so values such as `N/A`, `null`, `unknown`, and `-` are treated as missing regardless of case. The statistics computed for a column depend on its dtype, and each column receives a distribution label such as `constant`, `binary`, `zero-inflated`, `high-cardinality`, `skewed`, or `normal-ish`, derived from statistics that are already available. Numeric output passes through a helper that converts `NaN` and infinity to `null`, because JSON supports neither. On the frontend, a stats card sits in each column header, alongside a dataset summary tab and a correlation heatmap. Profile data uses a batch endpoint and a frontend cache keyed by a content-version counter, so scrolling and paging do not discard cached profiles.

## 4. **Data quality engine**
Checks cover duplicate rows, missing values, outliers using Tukey fences or z-scores, type mismatches, user-defined pattern rules, and format inconsistencies. These address four of the six common data quality dimensions; accuracy and timeliness were excluded because a single uploaded file cannot establish either. The engine reuses the missing-value handling from the profiling service, so both agree on what counts as missing. Issues carry a severity weight of 10, 5, 2, or 1, combined into a score from 0 to 100, normalised by dataset size for the dataset score and by row count for the column score. When an issue has a safe automatic fix, the suggested fix points at an existing DataLoom transformation and opens that transform with the required options pre-selected, so remediation is logged and checkpointed exactly like a normal user action. Pattern rules run user-provided regular expressions under a five-second time limit.

## 5. **The workspace interface**
The old layout placed transformation forms above the table, so opening a form hid the data being worked on, and the navbar carried a separate boolean flag per feature. [#394](https://github.com/c2siorg/dataloom/pull/394) rebuilt the table with a frozen header, serial number column, and dtype row. [#401](https://github.com/c2siorg/dataloom/pull/401) moved the workspace to a ribbon, tab strip, and right-side panel for forms, and introduced the frontend feature registry: a feature declares its tabs, panels, and menu entries in one place. The quality feature needs seventeen lines of wiring, and the navbar shrank from 662 lines to 219. Free-text column inputs were also replaced with searchable, type-aware selectors across the forms.

## 6. **Charts**
Six chart types with suggestions based on column dtypes. The backend handles aggregation and the frontend handles rendering. Sampling is available for large datasets and is reported to the user instead of being applied silently. This was the first feature built on the frontend feature registry, which validated the approach.

## 7. **Multi-file projects**
A user can append another file and preview the result first, showing matched, new, and missing columns. The file inventory is immutable, which matters for replay because the original files must be readable again when saving or reverting a project.

## 8. **Formula columns**
Implemented as another registered transformation rather than a separate formula system, so formulas inherit the existing logging, checkpoint, and replay infrastructure. Expressions pass an AST allowlist before reaching `df.eval`; function calls, attribute access, subscripts, lambdas, and builtins are rejected, and raw `eval` is never used.

## 9. **Reusable pipelines**
Pipelines reuse the existing storage rather than introducing their own. Compatibility with a target dataset is checked with a dry run instead of static per-operation metadata.

## 10. **PDF reports**
Downloadable reports covering the dataset overview, column profiles, quality information, and provenance. The report preview is the source for the downloaded document, so the file matches what the user saw.

## 11. **TypeScript migration**
Done in reviewable pieces: forms and lint wiring, utilities and configuration, then contexts and hooks. `tsc --noEmit` now runs as part of `npm run lint`, so type errors are caught by the existing lint command and in CI.

# What is left

- **Merge and join for multi-file projects.** Cross-project merge was descoped, and multi-file projects currently support append, where new columns are added into the same table when needed. This covers basic use cases but is not a true join. Proper merge and join operations are needed so users can combine datasets reliably.

- **Finishing the TypeScript migration.** [#484](https://github.com/c2siorg/dataloom/pull/484) is open, split into `chore/ts-common`, `chore/ts-shell`, `chore/ts-screens`, and `chore/ts-tooling`. There are currently 157 TypeScript files and 47 JavaScript files. The remaining work is isolated and can continue incrementally.

- Quality reports currently export to PDF only. Need to add **more formats** such as `docx`, `html` etc.

# Acknowledgements

Thank you to my mentor, *Oshan Mudannayake*, for the steady reviews, quick feedback, and for stepping in when I over-scoped things. It genuinely helped keep the project on track.

Thanks to C2SI for trusting contributors with real ownership over design and architecture decisions, not just isolated tasks.

Big thanks as well to the GSoC organisers and everyone who contributed to DataLoom over the summer. A lot of the progress came from collaborative work, and reviewing others' contributions was just as valuable as writing my own.
