# RustCloud: Multi-Cloud GenAI Provider Integrations and BigQuery Support

**Contributor:** Atharva Nagane   
**GitHub:** [atharva-nagane](https://github.com/atharva-nagane)  
**Email:** atharvatnagane37@gmail.com   
**Medium:** [atharvatnagane37](https://medium.com/@atharvatnagane37)    
**Organization:** C2SI  
**Mentor:** Pratik Dhanave, Mohit Bhat, Shubh Mehta  
**GSoC:** 2026 · ~360h track

# Project Abstract

RustCloud gives developers one Rust interface across AWS, GCP, and Azure, but before this project it had no support for generative AI APIs. Every GenAI provider exposes a different surface, with different auth models, different request and response shapes, and no shared way to route between them or retry failures. This project built a shared LlmProvider trait and implemented it against AWS Bedrock, GCP Vertex AI, and Azure OpenAI, overhauled the existing BigQuery client to the same standard, and added a UnifiedLlmClient routing layer with three routing strategies plus a generic RetryMiddleware on top, so a caller can compose multiple providers behind one interface with backoff and fallback built in.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/fkYCFYBS)

## [GSoC Project Proposal](https://drive.google.com/file/d/1EdTluDXwNOVJENThthl4zCLIg1e17sOj/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/RustCloud)

## [GitHub Personal Repo](https://github.com/atharva-nagane/RustCloud)

## [Commits during GSoC 2026](https://github.com/c2siorg/RustCloud/commits/main/?author=atharva-nagane)

## [Project Wiki](https://github.com/c2siorg/RustCloud/blob/main/README.md)

## [GSoC Blog](https://medium.com/@atharvatnagane37/list/rustcloud-gsoc-2026-41da2cc31765)

# Work Summary

**Pre-GSoC**

| **Description** | **PR** | **Merged** |
| --- | --- | --- |
| Fixed an AWS IAM `create_group` path parameter bug, added IAM user and role management operations | [#26](https://github.com/c2siorg/RustCloud/pull/26) | ✅ |
| Added missing AWS S3 object-level operations (put, get, list, head, copy) | [#28](https://github.com/c2siorg/RustCloud/pull/28) | ✅ |
| Added missing AWS DynamoDB item-level CRUD operations (get_item, put_item, update_item, scan, batch_write_item) | [#32](https://github.com/c2siorg/RustCloud/pull/32) | ✅ |
| Fixed the README and added a CODE_OF_CONDUCT | [#38](https://github.com/c2siorg/RustCloud/pull/38) | ✅ |
| Added a DigitalOcean Kubernetes (DOKS) managed cluster provider | [#111](https://github.com/c2siorg/RustCloud/pull/111) | ✅ |

**GSoC Coding Period**

| **Description** | **PR** | **Merged** |
| --- | --- | --- |
| AWS Bedrock: provider scaffold, generate(), embed() | [#140](https://github.com/c2siorg/RustCloud/pull/140), [#142](https://github.com/c2siorg/RustCloud/pull/142), [#144](https://github.com/c2siorg/RustCloud/pull/144) | ✅ |
| AWS Bedrock: stream() via converse_stream bridged into an mpsc channel | [#146](https://github.com/c2siorg/RustCloud/pull/146) | ✅ |
| AWS Bedrock: generate_with_tools() | [#148](https://github.com/c2siorg/RustCloud/pull/148) | ✅ |
| AWS Bedrock: SDK error classification, empty-tools guard | [#150](https://github.com/c2siorg/RustCloud/pull/150), [#152](https://github.com/c2siorg/RustCloud/pull/152) | ✅ |
| AWS Bedrock: usage examples | [#155](https://github.com/c2siorg/RustCloud/pull/155) | ✅ |
| GCP Vertex AI: generate() and stream() over raw REST | [#157](https://github.com/c2siorg/RustCloud/pull/157) | ✅ |
| GCP Vertex AI: embed(), TokenProvider injection | [#159](https://github.com/c2siorg/RustCloud/pull/159) | ✅ |
| GCP Vertex AI: generate_with_tools() | [#161](https://github.com/c2siorg/RustCloud/pull/161) | ✅ |
| GCP BigQuery: typed dataset operations, pagination | [#163](https://github.com/c2siorg/RustCloud/pull/163), [#165](https://github.com/c2siorg/RustCloud/pull/165) | ✅ |
| GCP BigQuery: typed table operations, query polling, streaming insert | [#167](https://github.com/c2siorg/RustCloud/pull/167) | ✅ |
| Azure OpenAI: full LlmProvider implementation | [#169](https://github.com/c2siorg/RustCloud/pull/169), [#171](https://github.com/c2siorg/RustCloud/pull/171) | ✅ |
| Azure OpenAI: human-readable error parsing, Retry-After support | [#173](https://github.com/c2siorg/RustCloud/pull/173) | ✅ |
| Azure OpenAI: stream event-ordering fix, edge case coverage | [#175](https://github.com/c2siorg/RustCloud/pull/175) | ✅ |
| UnifiedLlmClient: Explicit and ModelBased routing | [#177](https://github.com/c2siorg/RustCloud/pull/177) | ✅ |
| UnifiedLlmClient: Fallback routing | [#179](https://github.com/c2siorg/RustCloud/pull/179) | ✅ |
| RetryMiddleware: struct, config, generate() | [#181](https://github.com/c2siorg/RustCloud/pull/181) | ✅ |
| RetryMiddleware: full method coverage, usage doc | [#183](https://github.com/c2siorg/RustCloud/pull/183) | ✅ |
| Legacy test debt: Azure and AWS mock fixes | [#185](https://github.com/c2siorg/RustCloud/pull/185), [#187](https://github.com/c2siorg/RustCloud/pull/187) | ✅ |
| Legacy test debt: GCP token injection | [#189](https://github.com/c2siorg/RustCloud/pull/189) | ✅ |
| Streaming bug fixes found during final review (Vertex AI UTF-8, Azure dropped completion) | [#191](https://github.com/c2siorg/RustCloud/pull/191) | ✅ |

# What Covered

## AWS Bedrock Provider

I implemented all four methods of the LlmProvider trait against Bedrock's Converse API using aws-sdk-bedrockruntime: generate(), stream() (bridging the SDK's converse_stream receiver into an async Stream through an mpsc channel), embed() (via Titan Embed v2), and generate_with_tools(). I added an error classification layer mapping AWS SDK errors into typed CloudError variants covering auth failures, rate limits, retryable and non-retryable provider errors, network errors, and unsupported operations. This module has 38 tests. 
Covered in more depth: [implementation](https://medium.com/@atharvatnagane37/implementing-awsbedrockprovider-for-rustcloud-186b38ecfb5a) and [error handling](https://medium.com/@atharvatnagane37/error-handling-for-awsbedrockprovider-46ef34d8c6af).
 
## GCP Vertex AI Provider
 
I implemented the same four trait methods against Vertex AI's REST API using reqwest, since there is no official Rust SDK for Vertex AI. I pulled authentication out behind a TokenProvider trait so tests can inject a mock token provider instead of needing live GCP credentials. Streaming required hand rolled parsing of server sent events over raw HTTP, including manual buffering to handle a single JSON line arriving split across two separate network reads. This module also established the general structural pattern I reused for every later provider: struct and auth, then free function request builders, then an error mapper, then a response parser, then the trait implementation last. 44 unit tests plus 4 tests gated behind #[ignore] that require live credentials. 
Covered in more depth [here](https://medium.com/@atharvatnagane37/implementing-vertexaiprovider-for-rustcloud-63106f3739bb).
 
## GCP BigQuery Client Overhaul
 
I rebuilt the existing BigQuery client with injectable auth using the same TokenProvider pattern, typed responses in place of raw JSON for dataset and table operations, pagination, an async polling loop for BigQuery's asynchronous query jobs, and streaming row inserts. 26 unit tests plus 7 tests gated behind #[ignore] that require a live GCP project. 
Covered in more depth [here](https://medium.com/@atharvatnagane37/bigquery-client-typed-errors-injectable-auth-and-pagination-009d0c44fdb2).
 
## Azure OpenAI Provider
 
I implemented all four LlmProvider methods against Azure's REST API using static API key authentication, with model resolution based on deployment names rather than model IDs. I followed this with a hardening pass: human readable error message parsing from Azure's JSON error bodies, honoring the Retry-After header on rate limits, and a fix to a stream event ordering bug where a buffered terminal event could either be released ahead of content that should have preceded it, or get silently dropped, depending on the order chunks arrived in. 72 tests, no clippy warnings. 
Covered in more depth: [implementation](https://medium.com/@atharvatnagane37/implementing-azureopenaiprovider-for-rustcloud-4d5555af667e) and [error handling](https://medium.com/@atharvatnagane37/error-handling-and-a-streaming-fix-for-azureopenaiprovider-d0184eac234b).
 
## UnifiedLlmClient Routing Layer
 
I built a client that registers multiple LlmProvider implementations and routes requests between them using one of three strategies. Explicit always uses one named default provider. ModelBased routes by matching the requested model against provider specific prefixes. Fallback tries providers in registration order, skips past transient failures, and propagates hard failures immediately. UnifiedLlmClient itself implements LlmProvider, so it composes with other middleware the same way a concrete provider does.
 
Before merging this module I ran three rounds of self initiated adversarial review that were not requested by my mentors. That review caught a dead code match arm that was silently misrouting the Fallback strategy, helpers that needed pub(crate) visibility, four hand copied retry loops that I collapsed into one generic helper, and two trait methods with zero test coverage under Fallback. 35 tests. 
Covered in more depth [here](https://medium.com/@atharvatnagane37/unifiedllmclient-routing-across-rustclouds-three-providers-e75f05fdf513).
 
## RetryMiddleware
 
I built a generic exponential backoff retry wrapper, RetryMiddleware<P: LlmProvider>, that wraps any LlmProvider, including UnifiedLlmClient itself. Backoff follows base delay times two to the power of the attempt number, with jitter, using saturating arithmetic so a large attempt count clamps instead of overflowing. A server supplied Retry-After header always overrides the computed delay. This module reuses the same transient error classifier that the routing layer's Fallback strategy uses, so the two layers can never disagree about what counts as retryable. I split this across two PRs to keep each review sized reasonably: the first covered generate() only, the second extended the same treatment to stream(), embed(), and generate_with_tools(). 35 tests total. 
Covered in more depth [here](https://medium.com/@atharvatnagane37/retrymiddleware-backoff-and-retry-for-rustclouds-llmprovider-trait-db882323d302).
 
## Legacy Test Debt Cleanup, Beyond Original Scope
 
With the proposed work complete ahead of schedule, I used the remaining time to fix 119 pre-existing test failures across the AWS, GCP, and Azure modules that were unrelated to my project and required live cloud credentials to pass. Doing this work surfaced two real bugs in code I had already shipped. The first was a UTF-8 corruption bug in the Vertex AI stream parser, where a multi-byte character split across a network chunk boundary could silently become a replacement character. The second was a bug in Azure OpenAI's stream handling that could drop a completed generation entirely if the connection closed at the wrong moment. I fixed both. The full test suite went from 119 failing to 364 passing, 0 failing, and 43 intentionally ignored tests that require live credentials by design, with clippy clean.

# What left

- **CI-integrated code coverage.** The project has no cargo-llvm-cov or cargo-tarpaulin step
  in CI, so coverage is inferred from test counts rather than measured. Wiring this in would
  give every future PR an actual number instead of an estimate.
- **A mocked test harness for BigQuery.** Its 7 tests currently require a live GCP project to
  run, unlike every LLM provider module added this summer. Extending the same
  TokenProvider-based mocking pattern used across AWS, GCP, and Azure to BigQuery would bring
  it in line with the rest of the crate.
- **Publishing to crates.io.** RustCloud isn't published as a versioned crate yet. Once the API
  is stable across all three clouds, packaging it for external use is the logical next step.
