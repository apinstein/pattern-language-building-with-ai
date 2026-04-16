# General Ecosystem Pattern Index

This is the index of all patterns within the **General** domain of the AI Pattern Language skill.
Unlike project-specific domains (Business/Product/Technical), these patterns apply universally to **all repositories** where this AI skill is loaded.

*Instructions for AI Agents:* Before creating a new pattern in this domain, check this index to determine the next available sequential ID (e.g., `G-001`). 

## Pattern Categories

### 1. Philosophy & Agent Action (Scale Block 001-019)
- [PHILOSOPHY](PHILOSOPHY.md): The core Product > Technology directive.
- [G-001: Strongly Constrained Tools](G-001-strongly-constrained-tools.md): Prioritize hard-bounded, specific wrapper tools over generalized, destructive mega-commands to enforce AI focus and safety.
- [G-002: Tool Specification Schema](G-002-tool-specification-schema.md): Defines the strict input/output rules for creating the strongly constrained wrapper tools mandated by G-004.
- [G-003: Architecture Diagrams (LikeC4 vs Mermaid)](G-003-architecture-diagrams.md): Use LikeC4 for structural and dependency mapping, and reserve Mermaid exclusively for dynamic flowcharts and state machines.

### 2. Context & Ecosystem Memory (Scale Block 020-039)
- [G-020: Pageable Wisdom and Context Management](G-020-pageable-wisdom.md): Treat the pattern language as a modular memory bank of tacit knowledge that must be "lazy loaded" to preserve context windows.
- [G-021: Saliency and Conflict Resolution](G-021-saliency-and-conflict-resolution.md): Use patterns to bind solutions to their specific contexts, preventing decision paralysis and improving the saliency of the correct approach amongst thousands of conflicting rules.
- [G-022: Future-Proof Data Capture](G-022-future-proof-data-capture.md): Prioritize storing structured, high-fidelity raw data alongside parsed decisions so that future, more powerful AI models can re-process historical context without suffering from lossy summarization.

### 3. Rigid Quality Control (Scale Block 040-059)
- [G-040: Adversarial Verification Loops](G-040-adversarial-verification.md): Structurally mandate inline standard checking and separate verification loops to counteract an AI's confirmation bias and "premature finish" syndrome.
- [G-041: Inline Verification Checklists](G-041-inline-verification-checklists.md): Use concrete markdown checklists during adversarial verification loops to fundamentally short-circuit confirmation bias and force objective audits.
- [G-042: Tool-Driven Correctness](G-042-tool-driven-correctness.md): Use hard-bounded verification tools to objectively prove correctness, significantly increasing saliency and reducing the cognitive token load required by stochastic reasoning.
