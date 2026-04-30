# G-009: Anti-Patterns — The Illusion of General Competence *

**Status:** Active
**Type:** General
**Domain:** Ecosystem

## Context
The introduction to this pattern language acknowledges AI's asymmetric strengths and weaknesses. But a brief list of weaknesses is insufficient—these failure modes are so pervasive and so consistently misunderstood that they deserve deep analysis. Teams routinely over-invest in AI automation for tasks that fall squarely into these traps, burning cycles on workflows that will never reliably work.

⋇ ⋇ ⋇

## Problem
AI's linguistic fluency creates a persistent illusion of general competence that leads practitioners to deploy it in domains where it will systematically fail. Without a formal catalog of these failure modes, teams repeatedly discover the same limitations the hard way.

### Body of Problem
The core danger is that AI output *looks* competent. It is grammatically fluent, confidently stated, and superficially plausible. Humans are calibrated to associate these signals with actual competence—because in human interaction, fluency and confidence are reliable proxies for expertise. But in AI, they are completely decorrelated from correctness. This creates a systematic over-trust that leads to misallocation of effort and disappointing results.

## Solution
Maintain and reference a formal **Anti-Pattern Catalog** of domains and task types where AI systematically underperforms human expectations. Use this catalog as a decision gate alongside [G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md) when evaluating whether to invest in AI automation for a given task.

### Body of Solution

#### Anti-Pattern 1: Tacit Knowledge Domains

AI cannot *learn by doing*. It can only operate on pre-codified, explicit knowledge. People assume the AI will "absorb the project's culture" or "learn the codebase feel" through exposure, but it has no mechanism for experiential learning within a session.

More fundamentally, vast domains of human tacit and embodied knowledge are simply absent from base model training data. Craftsmanship, physical intuition, domain-specific "feel," and the kind of expertise that practitioners acquire over years of hands-on practice—these are poorly represented in text corpora. AI is therefore especially fallible in high-tacit-knowledge domains (skilled trades, music performance, clinical diagnosis, mechanical engineering intuition) where the real expertise lives in practitioners' bodies and habits, not in written documentation.

Every piece of tacit knowledge the AI needs must be explicitly written down and loaded into context (→ [G-020: Pageable Wisdom](G-020-pageable-wisdom.md)). And even then, recognize that codified approximations of tacit knowledge are inherently lossy.

#### Anti-Pattern 2: Long-Horizon Task Adherence Without Harness

AI loses the thread on multi-step plans spanning many tool calls. It contradicts earlier decisions, scope-drifts, or declares premature victory. Without an explicit external harness (checklist, plan artifact, state machine), tasks beyond approximately 5–10 coherent steps degrade significantly.

The root cause is architectural: base models are trained for high responsiveness—optimized to produce a satisfying, complete-seeming answer as quickly as possible. This training incentive actively works *against* sustained, multi-step execution where the correct behavior is to defer completion, maintain state, and methodically work through a long sequence. The model's optimization pressure is to *conclude*, not to *persist*.

People over-trust the AI to "just figure it out" on complex workflows. The solution is explicit external scaffolding: task checklists, plan artifacts, state machines, and harnesses that hold the long-horizon context the model cannot maintain internally (→ [G-040: Adversarial Verification Loops](G-040-adversarial-verification.md), [G-041: Inline Verification Checklists](G-041-inline-verification-checklists.md)).

#### Anti-Pattern 3: The Fluency Trap

AI output is linguistically fluent and confident, which triggers human trust heuristics calibrated for human competence signals. But fluency ≠ correctness. A model can produce a perfectly grammatical, authoritative-sounding explanation of something completely wrong—and the human reader's instinct is to trust it because it "sounds like it knows what it's talking about."

This causes systematic over-delegation of tasks requiring judgment, taste, or deep domain expertise. The antidote is structural: never evaluate AI output by how it reads—evaluate it by running it through objective verification (→ [G-042: Tool-Driven Correctness](G-042-tool-driven-correctness.md)). If you catch yourself thinking "that looks right," you are in the trap.

#### Anti-Pattern 4: Unverifiable Domains

Tasks where the objective function is subjective, expensive, or nonexistent are fundamentally resistant to AI closed loops (→ [G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md)). Creative writing quality, strategic business decisions, UX taste, and architectural aesthetics lack cheap, objective verifiers. In these domains, AI reliably produces "regression to the mean" results—output that is generically acceptable but never excellent, because there is no signal to drive it toward excellence.

People attempt to fully automate these domains and are disappointed. The correct approach is either to invest in building structured eval pipelines that approximate an objective function (→ [G-008: Eval-Driven System Design](G-008-eval-driven-system-design.md)), or to accept that AI serves as an *assistant* in these domains—generating options for human judgment—rather than an autonomous agent.

#### Anti-Pattern 5: Implicit State and Convention

AI struggles with unwritten rules, team conventions, and "the way we do things here" unless explicitly codified. It will confidently produce output that violates unstated norms—using the wrong naming convention, breaking an implicit architectural boundary, or ignoring a team's preferred approach to error handling.

This is a specific instance of the tacit knowledge problem, but worth calling out separately because the fix is actionable: codify your conventions. Style guides, architectural decision records, and this pattern language itself exist precisely to convert implicit convention into explicit, loadable context.

⋇ ⋇ ⋇

## Related Smaller Patterns
This anti-pattern catalog serves as the diagnostic complement to the entire pattern language. It explains *why* the scaffolding patterns exist: [G-020: Pageable Wisdom](G-020-pageable-wisdom.md) addresses Anti-Pattern 1 by codifying tacit knowledge. [G-040: Adversarial Verification Loops](G-040-adversarial-verification.md) and [G-041: Inline Verification Checklists](G-041-inline-verification-checklists.md) address Anti-Pattern 2 by providing external harnesses. [G-042: Tool-Driven Correctness](G-042-tool-driven-correctness.md) addresses Anti-Pattern 3 by replacing subjective "looks good" evaluation with objective tooling. [G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md) and [G-008: Eval-Driven System Design](G-008-eval-driven-system-design.md) address Anti-Pattern 4 by evaluating and building verifiers.
