# Agentic Cognitive Firewall SDK

## Contributor Information

* **Name:** Pranjal Udhwani
* **GitHub:** https://github.com/Pranjal0410
* **LinkedIn:** https://www.linkedin.com/in/pranjal-udhwani

# Project Abstract

ACF-SDK is a process-boundary security firewall for AI agents. The Python SDK runs inside the agent process, while policy decisions are evaluated in an isolated Go sidecar connected over a Unix Domain Socket with HMAC-SHA256 authentication. Every intercepted agent action passes through a five-stage pipeline — **validate, normalise, scan, aggregate, and OPA** — before producing an **ALLOW, SANITISE, or BLOCK** decision.

My GSoC project strengthened the enforcement surface across four areas:

1. **Policy foundation.** Built the complete OPA/Rego policy layer for all four hooks — prompt, context, tool call, and memory write — with 102 passing OPA tests and fail-closed tool allowlist enforcement.

2. **Security bug discovery and fix.** Independently discovered that the SANITISE path was silently broken for obfuscated attacks. The normalizer detected an attack in transformed text, while redaction searched for the normalized string in the original payload. Because the representations did not match, the system reported SANITISE while allowing the original attack to pass through unchanged. Fixed this using canonical-span tracking in the executor.

3. **Semantic scanner integration.** Ported and integrated the semantic scanner with runtime enable/disable controls, environment-variable configuration, per-hook text extraction, and backend-specific threshold calibration. Upgraded the default model to multilingual detection. The semantic layer catches paraphrased attacks that lexical matching cannot detect and, in the 30-language transfer evaluation, detected the same attack across 25 of 30 languages with zero false positives on the evaluated benign set.

4. **Framework adapters and demo.** Built the LangGraph FirewallNode adapter, including a fix for the deprecated NodeInterrupt behaviour, added Agent Kernel InputGuardrail and OutputGuardrail adapters, and created a Docker demo that runs the complete system from a single command across all four enforcement points.

## Project Links

* **GSoC Project Page:** https://summerofcode.withgoogle.com/myprojects/details/YdkWURkI
* **Organization Repository:** https://github.com/c2siorg/acf-sdk
* **Personal Repository:** https://github.com/Pranjal0410/acf-sdk
* **GSoC PRs:** https://github.com/c2siorg/acf-sdk/pulls?q=is%3Apr+author%3APranjal0410
* **Project Documentation:** https://github.com/c2siorg/ACF-SDK/tree/main/docs

# Work Summary

The original proposal focused on library expansion and multilingual pattern coverage. As the project progressed, the work shifted toward the areas that had the highest impact on the SDK: strengthening the SDK-to-sidecar enforcement path, identifying and fixing a security bug, integrating semantic detection, building framework adapters, and shipping a runnable end-to-end demo.

These redirects were mentor-directed and resulted in a more complete enforcement architecture than the original proposal alone would have produced.

## Merged Pull Requests

| PR      | Work                                                                                                                                                                           |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **#19** | OPA/Rego policy templates for all four hooks. 1,230 lines with 102 passing OPA tests.                                                                                          |
| **#50** | Memory-jailbreak SANITISE path fix.                                                                                                                                            |
| **#51** | LangGraph FirewallNode adapter. BLOCK halts the graph; SANITISE rewrites state in place.                                                                                       |
| **#55** | SANITISE canonical-span security fix. Independently discovered and fixed.                                                                                                      |
| **#58** | Semantic scanner package port. Five modules, 24 tests, and two bugs fixed during review.                                                                                       |
| **#60** | SDK semantic scanner integration with runtime controls, environment-variable configuration, per-hook text extraction, and 29 tests.                                            |
| **#61** | FirewallBlocked exception replacing deprecated NodeInterrupt behaviour, with two runnable adapter examples.                                                                    |
| **#62** | Detection-rate evaluation over 58 adversarial payloads, including threshold tradeoff analysis.                                                                                 |
| **#65** | Per-backend threshold calibration. TF-IDF threshold: 0.85; sentence-transformer threshold: 0.50. Increased attacks caught by 67% at zero false positives on the evaluated set. |
| **#68** | Pattern library expansion from 53 to 79 patterns, closing 5 new corpus gaps (ap-087, ap-088, ap-089, ap-095, ap-102).                                                               |

## Pull Requests Submitted for Review

| PR      | State           | Work                                                                                                                                                                                 |
| ------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **#67** | Open, mergeable | Docker demo with six scenarios across all four hooks.                                                                                                                                |
| **#71** | Open, mergeable | Agent Kernel adapter with InputGuardrail and OutputGuardrail. 12 tests.                                                                                                              |
| **#77** | Open, mergeable | Multilingual model, background calibration, and field-aware extraction. 30/47 English attacks at 0 FP on the evaluated benign set, 28/32 multilingual attacks at 0 FP on the evaluated benign set. |

# What I Covered

## 1. Policy Enforcement Layer

Built the complete OPA/Rego policy foundation across all four enforcement points: prompt, context, tool call, and memory write.

The tool allowlist is **fail-closed**: when the allowlist is unconfigured or empty, tool calls are blocked rather than implicitly permitted. Memory-jailbreak patterns return SANITISE rather than allowing the payload to continue unchanged.

The policy layer is covered by **102 OPA tests**, including enforcement logic and policy edge cases.

## 2. SANITISE Security Bug

The most significant security issue I found was a silent failure in the SANITISE path.

The normalizer transforms obfuscated text before scanning, allowing the system to detect attacks involving leetspeak and Unicode substitutions. However, the redaction stage subsequently searched for the normalized representation inside the original payload. Since those strings were different, the system could correctly identify the attack and return **SANITISE**, while leaving the original malicious content untouched.

This is particularly dangerous because the system appears to have enforced the policy correctly while the attack actually continues through the pipeline.

I fixed this using **canonical-span tracking**, allowing the executor to map detections in normalized text back to the exact spans in the original payload that must be redacted.

The issue was discovered independently while testing the enforcement path rather than through an existing bug report.

## 3. Semantic Scanner Integration

Integrated the semantic scanner directly into the Firewall class with:

* Runtime enable/disable control
* Environment-variable configuration
* Per-hook text extraction
* Backend-specific threshold calibration
* Error handling that preserves the sidecar lexical scanner as the safety fallback

Threshold calibration showed that score magnitude alone is not a useful measure of model quality. TF-IDF produced noisy scores and retained a threshold of **0.85**, while the sentence-transformer backend produced better attack/benign separation and was calibrated to **0.50**.

## 4. Multilingual Detection

Benchmarked three models across adversarial payloads and multilingual variants.

In the **30-language transfer evaluation**, the English-only MiniLM model detected only **1/30 non-English attacks**, while the multilingual model detected the same attack across **25/30 languages** with zero false positives on the evaluated benign set.

A separate evaluation corpus produced:

* **30/47 English attacks** detected at 0 false positives on the evaluated benign set
* **28/32 multilingual attacks** detected at 0 false positives on the evaluated benign set
* Noise floor reduced from **0.674 to 0.000**

I also added **background calibration**, replacing manually tuned thresholds with thresholds derived from a benign background corpus.

## 5. Framework Adapters

### LangGraph

The LangGraph integration exposed an issue with the deprecated `NodeInterrupt` mechanism in V1, where the expected blocking behaviour could silently fail.

I replaced this with a dedicated `FirewallBlocked(FirewallError)` exception that correctly propagates out of `invoke()`.

The adapter maps:

* **ALLOW** → continue execution
* **SANITISE** → rewrite state in place
* **BLOCK** → halt graph execution

### Agent Kernel

Added `InputGuardrail` and `OutputGuardrail` adapters, mapping the firewall decisions to the framework's guardrail semantics:

* **ALLOW** → ALLOW
* **BLOCK** → BLOCK
* **SANITISE** → OVERRIDE

## 6. Docker Demo

Built a single-container demonstration that runs both the Go sidecar and Python agent and exercises all four enforcement points through six scenarios.

One scenario demonstrates the semantic scanner detecting a paraphrased attack with **zero lexical overlap**, showing the specific capability that semantic detection adds beyond pattern matching.

## 7. Pattern Library

Expanded the jailbreak pattern library from **53 to 79 patterns**, closing **5 new adversarial corpus gaps** (ap-087, ap-088, ap-089, ap-095, ap-102) with zero regressions in the existing test suite.

# What Remains

* **Go-side syntax coverage:** remaining gaps include bare `&`, glob characters, sensitive path detection, and `1 → l` versus `1 → i` normalization. These are syntactic cases that semantic embeddings are not designed to reliably detect.
* **ONNX Runtime backend:** architecture already supports it; measured performance indicates a potential **5.2x speedup at 1.49 ms**.
* **Paper evaluation:** remaining sections include RQ3 and RQ5, baseline comparisons against DeBERTa and LlamaGuard, and confidence intervals for detection metrics.

# Challenges and Lessons

## A firewall that says it blocked something it didn't is worse than no firewall.

The SANITISE bug was silent. The system logged the correct decision and passed tests that validated only the decision label. The issue became visible only when I verified the actual output content.

After this, I changed how I test security-critical paths: **validate the resulting content, not just the decision code.**

## Score separation matters more than the score value.

TF-IDF produced high scores for both attacks and benign inputs. For example, an attack scored **0.81** while a benign weather question scored **0.83**, leaving no useful threshold between them.

The sentence-transformer backend produced lower absolute scores but much better separation: an attack scored **0.60** compared with **0.15** for the benign example.

I also caught an incorrect latency claim during the project. I had reported **0.26 ms** for the semantic scanner after measuring the TF-IDF backend rather than the sentence-transformer backend. I corrected the measurement the same day.

The lesson was straightforward: **measure the specific implementation you are claiming, not an adjacent one.**

## Background calibration is better than manual tuning.

Every change to the model or pattern library could shift the score distribution and require manual threshold adjustment.

Background calibration makes the threshold a property of the benign background corpus rather than a hard-coded configuration value. This makes the system more robust to changes underneath the scanner.

## The semantic layer's job is meaning, not syntax.

The remaining misses are primarily syntactic: shell metacharacters, path traversal tokens, command substitution, and similar constructs.

Embedding models are not designed to reliably distinguish these constructs from benign text because the distinction is often syntactic rather than semantic.

This reinforced the architecture of the system:

**lexical scanning handles syntax; semantic scanning handles meaning.**

The hybrid design is therefore not a compromise between two approaches. It is the appropriate architecture for covering different classes of threats.
