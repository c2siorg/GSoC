# Adversarial Validation Module for ACF-SDK

# Project Abstract

ACF-SDK is a framework-agnostic security firewall for LLM agents. Its Python SDK runs in the agent process, while policy decisions run inside an isolated Go sidecar. My GSoC project built the evaluation path for this boundary. The main deliverable is an adversarial integration harness that sends attack payloads through the signed IPC path and live sidecar pipeline, records the enforced decision, and tracks known detection gaps. I also worked on fixes found by the harness, false-positive coverage, concurrent scan correctness, replay of public external benchmarks, and trace and audit correlation tests for the existing observability work.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/2p2ipWVL)

## [GitHub Organization Repo](https://github.com/c2siorg/ACF-SDK)

## [GitHub Personal Repo](https://github.com/VibhorGautam/acf-sdk)

## [Commits during GSoC 2026](https://github.com/c2siorg/ACF-SDK/commits/main/?author=VibhorGautam)

## [Project Documentation](https://github.com/c2siorg/ACF-SDK/tree/main/docs)

# Work Summary

The initial project plan described a Python and pytest validation module. The repository's live integration path was later standardised in Go, so I moved the core harness into `tests/integration` and used the same signed Unix socket path as a real SDK request. This kept the original goal, testing attacks against the actual enforcement chain, while matching the architecture that shipped during GSoC.

The merged harness covers all 4 v1 hooks: `on_prompt`, `on_context`, `on_tool_call`, and `on_memory`. It records expected and desired decisions separately, so a known gap stays visible without making CI fail on every run. The corpus and harness then found issues in decoding, pattern normalisation, memory policy, destination policy, and signal attribution.

I also added a separate external runner in PR [#73](https://github.com/c2siorg/ACF-SDK/pull/73). It sends pinned InjecAgent and PINT sample cases through the Python `Firewall` and a live Go sidecar. It records dataset, code, configuration, model, dependency, and result hashes. It reports full results and exact-overlap-excluded results so known source overlap is visible.

## Merged work

| PR | Work |
| --- | --- |
| [#26](https://github.com/c2siorg/ACF-SDK/pull/26) | Added adversarial Rego fixtures for all 4 v1 hook policies |
| [#53](https://github.com/c2siorg/ACF-SDK/pull/53) | Removed a dead jailbreak pattern that could not fire after normalisation |
| [#54](https://github.com/c2siorg/ACF-SDK/pull/54) | Added embedded Base64 decoding before scan |
| [#56](https://github.com/c2siorg/ACF-SDK/pull/56) | Added URL-safe Base64 decoding |
| [#57](https://github.com/c2siorg/ACF-SDK/pull/57) | Added the live adversarial integration harness |
| [#59](https://github.com/c2siorg/ACF-SDK/pull/59) | Normalised pattern entries before building the Aho-Corasick dictionary |
| [#63](https://github.com/c2siorg/ACF-SDK/pull/63) | Made memory reads fail closed when HMAC proof is absent |
| [#64](https://github.com/c2siorg/ACF-SDK/pull/64) | Activated the destination allowlist gate |
| [#66](https://github.com/c2siorg/ACF-SDK/pull/66) | Preserved attack categories through the scan stage |
| [#72](https://github.com/c2siorg/ACF-SDK/pull/72) | Added 16 benign hard negatives authored by Kavishka Fernando, with 9 strict passes and 7 tracked false-positive gaps |
| [#74](https://github.com/c2siorg/ACF-SDK/pull/74) | Switched to thread-safe Aho-Corasick matching and added a concurrent regression test |

## Work submitted for review

| PR | Work | State on Aug 24 |
| --- | --- | --- |
| [#41](https://github.com/c2siorg/ACF-SDK/pull/41) | Pre-GSoC observability branch rebased during GSoC with new trace and audit correlation tests | Open, mergeable, CI green |
| [#73](https://github.com/c2siorg/ACF-SDK/pull/73) | Pinned external benchmark replay through the Python SDK and live sidecar | Open, approved, mergeable, CI green |

# What Covered

## Live adversarial evaluation

- Policy fixtures and live integration cases cover prompt injection, indirect context injection, unsafe tool calls, and memory poisoning
- The harness uses the real HMAC, nonce, framing, IPC, scan, aggregation, OPA, and executor path
- Expected and desired decisions make open security gaps visible without hiding current behaviour
- PR #72 added the missing benign side of the corpus and grew it from 58 to 74 cases

## Fixes driven by the harness

- Embedded standard and URL-safe Base64 attacks are decoded before scanning
- Pattern data is normalised before the Aho-Corasick dictionary is built
- Memory reads without an HMAC proof fail closed
- Destination allowlist checks are active through configuration
- Pattern hits keep their attack category through scan, aggregation, and policy analysis
- PR #74 found a shared-matcher race. Before the fix, repeated 2,000-call runs missed 217 to 341 known matches. The merged branch now includes a 2,000-call synchronized regression test. Manual runs at concurrency 1, 4, 16, and 32 returned 0 wrong decisions

## External benchmark replay

PR #73 ran 6 modes from a clean runner state: scanner OFF, TF-IDF ON, and MiniLM ON for InjecAgent and the public PINT format sample. All 32 benchmark tests pass.

- InjecAgent text detection: scanner OFF blocked 0/1,054 cases. TF-IDF added signals on 19/1,054 cases and MiniLM added signals on 15/1,054 cases, but neither changed a final sidecar decision
- InjecAgent authorization: 1,054/1,054 attack cases had at least 1 required attacker call blocked, 1,581/1,598 attacker calls were blocked, and 1,054/1,054 legitimate calls were allowed
- PINT public format sample: 1/2 attacks were caught and 0/6 benign cases were false positives. After exact-overlap exclusion, 0/1 attack was caught
- The runner records pinned dataset commits, file hashes, runner and configuration hashes, dependency versions, model snapshots, result hashes, and latency percentiles

These are hook-level detector and authorization results. They are not agent attack success rate results. The InjecAgent allowlist was built from the 17 legitimate tool names in the same selected dataset, so the legitimate-name result does not test unseen tools or allowlist selection.

## Observability

PR #41 started before the GSoC coding period. During GSoC I rebased it onto the current code and added coverage that checks trace and audit IDs together. The branch includes a root pipeline span, child spans for each stage, an OPA evaluation span, and 1 structured audit record per request. Raw payload text and canonical text are not written to telemetry. The audit path uses a buffered background writer so telemetry failure does not block policy enforcement.

# Challenges and Lessons

- A high detection number is not useful if the system blocks legitimate work. Catch rate, false positives, and authorization utility need to be reported together
- SDK semantic signals and sidecar decisions are different measurements. The external runner records both instead of treating a scanner signal as a blocked attack
- Some ACF patterns were based on public prompt-injection sources. Exact-overlap exclusion reduces 1 obvious contamination risk, but it is not a held-out benchmark
- Go can cache integration tests when only policy data changes. Corpus decisions must be checked with `-count=1`
- Correct single-request tests did not expose the shared Aho-Corasick matcher race. The concurrent regression test in PR #74 did
- Negative benchmark results are useful when the runner is reproducible and the claim stays narrow

# What left

- Merge the remaining observability and evaluation PRs in the agreed order, then rerun PR #73 against the final corrected main branch
- Add an `on_tool_result` hook so injected tool responses no longer use `on_context` as a proxy
- Add AgentDojo extraction and a model-in-the-loop experiment for agent attack success rate
- Request access to the full PINT evaluation set. The public repository contains only an 8-case format sample
- Build a held-out evaluation set with unseen legitimate tools and a larger benign `on_context` set before adding policy weights for new semantic signals
- Continue the latency, resilience, and related-work evaluation for the planned TRUST 2027 paper
- Maintain the corpus and reproduction path, review detector changes against benign and attack cases, and help new contributors use the harness before changing policies
