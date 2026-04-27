# G-043: Multi-Agent Council *

**Status:** Active
**Type:** General
**Domain:** Ecosystem

## Context
While **[G-040: Adversarial Verification Loops](G-040-adversarial-verification.md)** establishes the need for a separate reviewer agent or adversarial discriminator to evaluate output, a single adversarial prompt is inherently limited by its own narrow perspective and biases.

⋇ ⋇ ⋇

## Problem
In complex architecture, code generation, or product planning, a single AI agent cannot robustly evaluate output across all competing concerns simultaneously (e.g., performance, UI/UX, security, and maintainability). If prompted to care about everything, the AI experiences "regression to the mean," producing an average, un-insightful review that misses nuanced edge cases.

### Body of Problem
An AI instructed to be a "general expert reviewer" will spread its attention too thin. Conversely, an adversary instructed to look for one specific flaw will blindly ignore catastrophic failures outside its prompt's purview. The agent lacks the capacity to simulate the distinct, conflicting perspectives of stakeholders within a single context window without muddying the waters.

## Solution
Deploy a **"Multi-Agent Council"** where numerous AI agents are orchestrated chronologically or in parallel, each strictly prompted with a uniquely separate, highly opinionated persona.

### Body of Solution
Rather than relying on a monolithic prompt to evaluate or synthesize a complex task, splinter the verification or planning process:
1.  **Distinct Personas:** Create rigidly defined roles for distinct agents. For example, simultaneously prompt a "Ruthless Security Auditor," a "Pedantic Architect focused on DRYness," and an "Impatient End-User."
2.  **Opinionated Blind Blinders:** Explicitly instruct each council member to focus *only* on their domain constraint and ruthlessly attack the generated output from that specific angle.
3.  **Synthesis Agent:** Pass the outputs of the council to a separate synthesizing agent (or explicitly prompt the developer agent) to digest the diverse, hyper-focused feedback and negotiate a final, holistic solution.

⋇ ⋇ ⋇

## Related Smaller Patterns
- **[G-040: Adversarial Verification Loops](G-040-adversarial-verification.md)**: The predecessor pattern; the Council is the scaled-up, multi-lens evolution of single-agent adversarial verification.
- **[G-021: Saliency and Conflict Resolution](G-021-saliency-and-conflict-resolution.md)**: The Council surfaces inherent design conflicts, which then must be resolved through explicit context binding.
