# G-010: Functional Composition for AI-Friendly Code *

**Status:** Active
**Type:** General
**Domain:** Ecosystem

## Context
[G-004: Compiler-Driven Validation](G-004-compiler-driven-validation.md) makes the compiler a fast feedback loop for AI-generated code. Types help verify the shape of individual operations, but code also needs a structure that makes a larger transformation understandable and safely editable. Functional composition supplies that structure: a chain of small, typed transformations from an explicit input to an explicit output.

Functional composition lifts business logic from statements that mutate state to a composition of functions. This higher-order representation gives an AI a compact, explicit model of data flow: it can reason about each stage's typed contract, its position in the pipeline, and its effect boundary instead of reconstructing mutable state across control flow.

AI is especially effective at implementing repetitive, well-specified transformations that a human would understand but might not take the time to factor, name, or keep consistently separated. This pattern turns that strength into maintainable code without relying on the model to track a large amount of mutable, implicit state.

⋇ ⋇ ⋇

## Problem
Imperative implementations often accumulate mutable variables, branching, and interleaved effects until the business transformation is hidden inside control flow. AI agents then have to infer state across many lines and make localized changes without a clear contract for each intermediate step.

### Body of Problem
An imperative loop is sometimes the clearest or fastest solution, but sprawling imperative code creates a poor editing surface for AI. A small change can silently affect variable lifetime, mutation order, or a later conditional. Because the transformation is not decomposed, types can validate the program while still leaving the intent and the consequences of a change hard to inspect.

The result is unnecessary complexity: copy-pasted traversal code, flag variables with unclear invariants, and methods that both select, transform, aggregate, and perform I/O. Those methods make composition difficult for people and increase the chance that an AI introduces an accidental state or ordering bug.

## Solution
Prefer the functional style that the host language supports idiomatically: express business logic as small, typed, composable transformations; connect collections with `map`, `filter`, `flatMap`, and `reduce`; and make data flow through readable pipelines. Keep mutation and effects at explicit boundaries.

### Body of Solution

1. **Model transformations as functions.** Give each meaningful operation a focused input and output. Functions that produce a new value from an input are easier to type-check, test, reuse, and compose than procedures that modify distant state.
2. **Use collection combinators for collection work.** Prefer `map` for one-to-one transformations, `filter` for selection, `flatMap` for expansion or optional flattening, and `reduce` for aggregation with an explicit identity. This makes the shape of a calculation visible at a glance.
3. **Write readable pipelines.** Assemble multi-step logic in source order so a reader can follow the data from raw input to result. Name intermediate stages when that improves domain clarity; a pipeline should reveal the business rules, not become compressed cleverness.
4. **Isolate effects.** Keep network calls, filesystem access, database writes, UI mutation, and other side effects at a narrow orchestration boundary. Pass the required data into pure transformations and return their results before committing an effect.
5. **Honor the language and the problem.** Use the functional constructs native to the language (for example, Swift collection algorithms, Rust iterators, Java streams, or TypeScript array methods). Do not add a functional framework, use opaque point-free expressions, or replace a plainly clearer loop merely to satisfy this pattern. Make imperative state explicit when it is the more readable, performant, or idiomatic choice.

For example, a pipeline makes selection, conversion, and aggregation independently visible:

```ts
const total = orders
  .filter(isBillable)
  .map(toLineItem)
  .reduce(sumLineItemAmounts, 0);
```

The important property is not the syntax. It is that every stage has a clear contract, the aggregate begins from a known identity, and no hidden mutable state is required to understand the result. Types and tests can then verify each stage as well as the complete composition.

⋇ ⋇ ⋇

## Related Smaller Patterns
[G-004: Compiler-Driven Validation](G-004-compiler-driven-validation.md) validates the typed contracts at each composition boundary. [G-006: Zero Defects and Signal-to-Noise](G-006-zero-defects.md) complements this pattern by keeping the resulting pipelines free of warning noise and accidental complexity. [G-007: Verifiability as Prerequisite](G-007-verifiability-as-prerequisite.md) and [G-042: Tool-Driven Correctness](G-042-tool-driven-correctness.md) provide the objective feedback loops that verify a composed transformation's behavior.
