---
applyTo: "**"
---

# Global Programming Rules

- Everything must be written in English.
- Emojis must never be used.

---

## Function Design

- The length of a single function must not exceed 60 lines.
- A function must perform only a single responsibility.
- Code that is used repeatedly must be extracted into reusable functions.
- A function should operate at a single level of abstraction.
- The number of function parameters should be kept to a minimum.
- Argument and return types must be explicitly specified.
- Avoid complex coding techniques; use simple and straightforward syntax.
- Indentation must not be nested more than two levels deep.
- Use early returns to reduce nested control structures.
- Each function must include at least two assertions that explicitly validate critical assumptions or invariants.
- Assertions must check meaningful preconditions, postconditions, or internal invariants, not trivial or redundant conditions.
- Assertions must not be used as a replacement for proper error handling in production paths.

---

## Function Contracts (Preconditions and Postconditions)

- Every function must explicitly define its **preconditions** and **postconditions**.
- Preconditions describe assumptions that must be true **before** the function is invoked.
- Postconditions describe guarantees that must be true **after** the function completes successfully.
- Output guarantees (return values and observable effects) must be included as part of the postconditions.
- Preconditions and postconditions must be:
  - Precise and unambiguous
  - Expressed in terms of observable inputs, outputs, and state
  - Sufficient to support reasoning, testing, and refactoring

### Representation Rules

- Preconditions and postconditions must be expressed using one or more of the following:
  - Assertions inside the function body
  - Explicit type definitions or domain-specific types
  - Public API documentation comments at module or interface boundaries
- Assertions used for contracts must validate:
  - Input validity
  - Required invariants
  - Output integrity
- Assertions must not restate trivial facts already guaranteed by the type system.

---

## Test Case Requirements

- Every function **must provide at least one concrete, executable test example**.
- Test examples must demonstrate:
  - A valid invocation that satisfies all preconditions
  - Verification of all stated postconditions
- Test cases must be:
  - Directly traceable to the function’s preconditions and postconditions
  - Deterministic and repeatable
- If a function cannot be accompanied by a clear test example, its design is considered incomplete.

---

## Test Execution and Visibility

- Test cases must be **independently executable**.
- All tests must be executable via a **single, well-defined command**.
- Test results must be **immediately visible and understandable at a glance**.
- Silent success or failure is not allowed.

---

## Test Result Transparency

- Test output must include:
  - Total, passed, failed, and skipped test counts
  - Clear overall success or failure status
- For each test, it must be possible to inspect:
  - Input data and state **before** execution
  - Output data and state **after** execution
  - Expected results versus actual results
- Failures must clearly indicate which precondition or postcondition was violated.

---

## Test Coverage Tracking

- Functions without tests must be explicitly tracked.
- Untested functions must be:
  - Discoverable via automated reports
  - Identifiable by name and location
- Untested functions must remain visible in review and CI workflows.

---

## Test Pyramid and Instrumented Testing

- The test strategy must follow the **test pyramid model**:
  - **Unit tests** as the foundation (fast, isolated, most numerous)
  - **Integration tests** validating interactions between components
  - **End-to-End (E2E) tests** validating full system behavior
- The system must support **instrumented testing** across all pyramid levels.
- Instrumentation must allow measurement and inspection of:
  - Execution paths
  - State transitions
  - Input/output boundaries
  - Performance-relevant signals when applicable
- Each test level must be:
  - Separately identifiable in reports
  - Selectively executable if needed
- Unit, integration, and E2E tests must all be executable through the **single canonical test command**, with clear aggregation and breakdown of results.

---

## Naming Conventions

- Names must clearly express intent and responsibility.
- Function names should start with verbs.
- Class and type names should be nouns.
- Boolean variables should use prefixes such as `is`, `has`, or `can`.

---

## Code Readability

- Code should be written in a clear and consistent style.
- Avoid magic numbers; use named constants.
- Keep line length reasonable (100–120 characters).
- Separate logical sections with blank lines.

---

## Comments and Documentation

- Minimize comments.
- Do not explain *what* the code does; explain *why* only when necessary.
- Public APIs may include brief documentation comments.

---

## Control Flow and Error Handling

- Avoid deep nesting; prefer early returns.
- Do not silently ignore errors.
- Separate error-handling paths from normal execution.
- Prefer explicit error types.

---

## Modularity and Dependencies

- Organize code into cohesive modules.
- Dependencies must be acyclic and flow in one direction.
- External libraries must be isolated behind abstraction layers.

---

## Testability and Maintainability

- Limit side effects.
- Design for predictable change impact.
- Code that is difficult to test is a maintenance risk.

---

## Logging

- Logging must be intentional and minimal.
- Logs must improve understanding, not add noise.
- Logging must never replace proper error handling.
- Avoid logging in tight or high-frequency paths.