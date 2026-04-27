# G-005: Contextual Tool Responses *

**Status:** Active
**Type:** General
**Domain:** Ecosystem

## Context
We proactively build custom, strongly constrained wrapper tools (G-001) for AI agents so they can safely interact with their environment without relying on destructive mega-commands.

⋇ ⋇ ⋇

## Problem
Even with custom tools, an AI frequently loses track of the overarching plan or struggles to determine the exact mechanical next step. Supplying a bare-bones data dump from a tool forces the AI to constantly synthesize what it should do next using its highly fallible internal state.

### Body of Problem
Unlike a human, an AI does not maintain continuity of thought well. After executing a tool, it can easily misinterpret the result or pause and declare victory. If a tool simply outputs `{ "status": "error", "code": 12 }`, the AI is left to guess how to resolve it, which invites arbitrary tangents, circular loops, or giving up completely.

## Solution
Have specialized tools return more than just raw data: their responses should explicitly include contextual information on how to leverage the result, including available options and instructions for the next mechanical step.

### Body of Solution
Rather than relying on the AI to maintain procedural memory, you embed the workflow directly into the tool response (much like how REST APIs use HATEOAS to send contextual links alongside data). By structuring tool outputs to guide the agent:
1. **Provide Contextual Next Steps:** For example, if an error occurs, the tool output should include the options for resolution (e.g., `ERROR: Missing permission. Options: Run 'auth-tool --grant' then retry, or halt and ask the user for administrative access.`).
2. **Offload Procedural Memory:** The burden of maintaining workflow continuity is shifted from the AI's fragile context window back to the deterministic tooling itself.
3. **Improve Follow-up Quality:** This makes the AI's follow-up interactions significantly better and more predictable, as the agent is handed explicit contextual instructions determining how to chain tools together based on the result.

⋇ ⋇ ⋇

## Related Smaller Patterns
- **[G-001: Strongly Constrained Tools](G-001-strongly-constrained-tools.md)**: Defines the boundaries for tools, which this pattern then enriches with explicit next-step context.
- **[G-002: Tool Specification Schema](G-002-tool-specification-schema.md)**: The schema for building custom AI tools should mandate that output includes contextual follow-up paths.
