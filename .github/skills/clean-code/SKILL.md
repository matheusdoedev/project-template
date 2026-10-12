---
name: clean-code
description: 'Improve code quality and maintainability in software development. Use for refactoring, code reviews, implementation work, and ensuring readable, testable, and resilient code.'
argument-hint: 'What code quality issue or refactor do you want to improve?'
user-invocable: true
disable-model-invocation: false
---

# Clean Code

## When to Use
- Refactor existing code without changing behavior
- Review or improve newly written implementation
- Resolve complexity, duplication, or unclear logic
- Prepare code for long-term maintenance, teamwork, and testing
- Improve readability, reliability, and correctness before merge or release

## Core Objective
Produce code that is easy to understand, safe to change, and straightforward to validate. Favor clarity over cleverness, and keep code aligned with the problem it solves.

## Procedure

### 1. Understand the problem and constraints
Before changing code, identify:
- the real requirement or bug
- functional and non-functional constraints
- affected boundaries, inputs, outputs, and error cases
- whether the task is a bug fix, refactor, feature, or cleanup

If the requirement is unclear, ask targeted questions before editing. Do not optimize prematurely.

### 2. Read the relevant code narrowly and confidently
Inspect only the code needed to understand the behavior:
- the function, class, or module directly involved
- adjacent call sites if needed
- tests that currently cover the behavior

Prefer reading the minimum context that explains the root cause or required change. When the code is confusing, trace the data flow before making edits.

### 3. Identify the root cause and the code smell
Evaluate the code using clean-code principles:
- naming: variables, functions, and classes should communicate intent
- single responsibility: each function/class should have one reason to change
- small functions: prefer focused units with clear purpose
- readability: avoid nested conditionals or clever shortcuts when clarity is better
- consistency: follow the surrounding codebase conventions
- explicitness: surface assumptions, validation, and failure cases clearly
- no duplication: centralize repeated logic where it improves cohesion

If a bug is caused by unclear flow, wrong abstraction, or missing validation, fix the underlying issue rather than patching symptoms.

### 4. Make the smallest safe improvement
Apply a minimal, targeted change that improves structure without broadening scope.

Good refactor patterns:
- rename unclear symbols to describe intent
- extract repeated logic into a helper or private method
- simplify branching and early returns
- reduce parameter count by grouping related inputs
- move validation to the boundary where it belongs
- improve error handling to be explicit and actionable

Avoid:
- unrelated cleanup in the same patch
- large rewrites without a clear need
- introducing abstraction before the pattern is justified
- premature optimization for performance without evidence

### 5. Preserve behavior and improve testability
Clean code should be easy to verify.

When applicable:
- add or update focused tests for the changed behavior
- cover edge cases and failure conditions
- keep tests readable and behavior-oriented
- avoid asserting implementation details when behavior is what matters

If the behavior is not testable, simplify the design until it is.

### 6. Validate the change
Verify the result with the smallest relevant command or test:
- run the affected unit or integration tests
- confirm the bug is fixed or the feature behaves as expected
- check formatting, linting, or static analysis if the project uses them
- ensure the change does not break adjacent behavior

Do not claim success without evidence from the relevant checks.

## Decision Points

### If the code is confusing or misleading
- rename symbols to match intent
- extract a function or helper to clarify the responsibility
- reduce deeply nested conditionals with guard clauses or early returns

### If there is duplicated logic
- centralize the shared behavior in one place
- ensure the abstraction does not hide important context
- keep the extracted logic responsible and readable

### If the change is risky or broad
- narrow the scope to the specific behavior under change
- separate refactor from functional edits when possible
- validate incrementally before continuing

### If the code is hard to test
- identify control flow or hidden dependencies
- isolate side effects and external calls
- favor explicit inputs and outputs over hidden state

## Completion Checklist
Before finishing, confirm:
- the code is understandable to a teammate reading it for the first time
- names reflect business or technical intent accurately
- each function/class has a clear responsibility
- complexity is reduced without losing correctness
- error handling is explicit and safe
- tests or validation cover the changed behavior
- formatting, linting, and project conventions are respected
- the patch is scoped to the actual problem

## Quality Bar
A solution is considered clean when it is:
- readable without excessive ceremony
- coherent and consistent with local conventions
- easy to reason about and modify
- robust in the face of edge cases and errors
- supported by targeted validation

## Example Prompts
- /clean-code refactor this function to reduce duplication and improve readability
- /clean-code review this module for naming, responsibility, and complexity issues
- /clean-code improve the error handling and testability of this API path
- /clean-code simplify this logic without changing behavior

## Related Customizations
- create a naming-conventions instruction
- create a code-review checklist prompt
- create a refactoring workflow skill for larger architectural improvements
