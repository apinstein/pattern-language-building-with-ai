# G-008: Eval-Driven System Design *

**Status:** Active
**Type:** General
**Domain:** Ecosystem

## Context
[G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md) establishes that the quality of the objective function determines the ceiling of any AI closed loop. For many domains, a strong verifier doesn't exist naturally—but one can be *built* if the system is designed from the start to produce evaluation-ready data. Meanwhile, [G-022: Future-Proof Data Capture](G-022-future-proof-data-capture.md) advocates retaining raw data for future reprocessing. This pattern addresses a complementary but distinct concern: not just preserving data, but *intentionally instrumenting* the system architecture to produce the structured inputs an evaluation pipeline needs.

⋇ ⋇ ⋇

## Problem
Teams build AI-powered features, ship them, and then realize they have no way to systematically measure whether the AI is performing well. Bolting on evaluation after the fact is expensive and fragile because the data needed to assess quality was never captured in a structured, eval-ready format.

### Body of Problem
G-022 says "store raw data so future AI can reprocess it." That's necessary but insufficient. Raw logs and telemetry are not the same as structured evaluation datasets. To close the loop on AI quality, you need *(input, output, expected_output)* tuples—not just a firehose of events. If the system wasn't designed to capture these tuples at the right granularity, you end up reverse-engineering eval data from production logs, which is lossy, expensive, and often impossible.

The distinction matters: G-022 is a *preservation* philosophy ("don't throw data away"). This pattern is an *architectural* directive ("design the system to produce eval fuel from day one").

## Solution
Treat the evaluation pipeline as a **first-class architectural component**. Design data models, API contracts, and telemetry to produce structured evaluation pairs as a natural byproduct of system operation.

### Body of Solution
1. **Capture Evaluation Pairs, Not Just Logs:** Design your data models to store *(input, output, expected_output)* tuples at the right granularity for your domain. Don't just log "request received" and "response sent"—capture the structured context, the AI's raw output, any post-processing, and the ground truth (when available). Schema design should make it trivial to run evals retroactively.

2. **Build the Eval Harness Early:** The eval pipeline should influence your architecture from day one—not be bolted on after launch. If you're building an ASR system, design the pipeline to capture *(audio_context, raw_transcription, post_processed_output, expected_phrase)* tuples from the start. If you're building a code generation tool, capture *(prompt, generated_code, compilation_result, test_results)*. The eval harness is not a testing afterthought; it's a product feature.

3. **Close the Loop:** Captured eval data must feed back into system improvement. Whether through fine-tuning, prompt iteration, regression test suites, or human review queues, the data capture exists to power a continuous improvement cycle. Data that's captured but never used for improvement is waste.

4. **Design for Both Online and Offline Eval:** Online evaluation (real-time quality checks during production) and offline evaluation (batch analysis of historical performance) have different data requirements. Instrument for both: real-time signals enable immediate feedback loops, while historical datasets enable trend analysis and regression detection.

5. **Make Eval a Product Concern, Not Just an Engineering Concern:** The decision of *what to evaluate* is a product decision. Which dimensions of quality matter to users? What failure modes are unacceptable? These product requirements should drive the eval schema design, ensuring that engineering captures the right data to answer the right questions.

⋇ ⋇ ⋇

## Related Smaller Patterns
This pattern is a direct complement to [G-022: Future-Proof Data Capture](G-022-future-proof-data-capture.md), which provides the preservation philosophy that ensures raw data survives for reprocessing. It operationalizes [G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md) by providing the architectural strategy for *building* the verifier when one doesn't exist naturally. The structured eval data it produces becomes the fuel for [G-040: Adversarial Verification Loops](G-040-adversarial-verification.md) and [G-042: Tool-Driven Correctness](G-042-tool-driven-correctness.md).
