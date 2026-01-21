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

### Design Implications

- A function whose preconditions are complex or difficult to state likely violates single-responsibility or abstraction-level rules.
- Postconditions must not depend on undocumented side effects.
- Functions with side effects must explicitly include those effects in their postconditions.
- If a function cannot clearly state its postconditions, its design must be reconsidered.

---

## Test Case Requirements

- Every function **must provide at least one concrete, executable test example**.
- Test examples must demonstrate:
  - A valid invocation that satisfies all preconditions
  - Verification of all stated postconditions
- Test cases must be:
  - Directly traceable to the function’s preconditions and postconditions
  - Deterministic and repeatable
  - Written using the project’s standard testing framework or a clearly defined equivalent
- Functions with multiple logical branches must provide test examples covering:
  - The primary success path
  - Meaningful edge cases derived from contract boundaries
- If a function cannot be accompanied by a clear test example, its design is considered incomplete.

---

## Test Execution and Visibility

- Test cases must be **independently executable** without requiring manual setup beyond documented prerequisites.
- Each test must be runnable in isolation (single command or single entry point).
- Test results must be **immediately and clearly visible**.
- Silent success or failure is not allowed.

---

## Test Result Transparency

- Test results must be **understandable at a glance**.
- The test output must provide a clear, structured summary including:
  - Total number of tests executed
  - Number of passed, failed, and skipped tests
  - A clear overall success or failure indicator
- For each test case, it must be possible to **inspect detailed execution data**, including:
  - Input data and system state **before** the function execution
  - Output values and system state **after** the function execution
  - The actual result produced by the function
  - The expected result derived from postconditions
- When a test fails, the output must clearly show:
  - Which precondition or postcondition was violated
  - The difference between expected and actual results
- Test outputs must not require debugging tools to interpret; all critical information must be available through standard test reporting mechanisms.

---

## Test Coverage Tracking

- The system must support **explicit tracking of functions that do not have associated tests**.
- Each function must be traceable to one or more test cases, or be explicitly marked as **untested**.
- Untested functions must be:
  - Discoverable through automated tooling or reports
  - Clearly identifiable by name, location, and ownership
- The tracking mechanism must make it possible to:
  - Enumerate all untested functions
  - Prioritize test creation based on risk or change frequency
- Functions marked as untested must not be silently ignored; their status must be visible in development and review workflows.

---

## Test Execution Consistency

- **All tests must be executable via a single, well-defined command**.
- The command must:
  - Execute the complete test suite without requiring additional manual steps
  - Produce a consolidated and readable summary of results
- Partial or fragmented test execution mechanisms are not allowed.
- The canonical test command must be:
  - Documented
  - Stable across environments (local development, CI, automation)
- Any test that cannot be executed through this unified command is considered non-compliant.

---

## Naming Conventions

- Names must clearly express intent and responsibility.
- Avoid abbreviations unless they are widely and commonly understood.
- Function names should start with verbs.
- Class and type names should be nouns.
- Boolean variables should use prefixes such as `is`, `has`, or `can`.

---

## Code Readability

- Code should be written in a clear, readable, and consistent style.
- Prefer positive conditions over negative ones in conditional statements.
- Complex conditional expressions must be extracted into well-named variables or functions.
- Avoid magic numbers; define constants with meaningful names instead.
- Write one logical idea per line.
- Keep line length within a reasonable limit (e.g., 100–120 characters).
- Use blank lines to separate logical sections of code.

---

## Comments and Documentation

- Comments should be minimized and avoided whenever possible.
- Do not comment on what the code does; comment only on why it exists when necessary.
- Public APIs, interfaces, and boundaries may include brief documentation comments.
- Test-related output may include structured labels solely to improve result clarity.

---

## Control Flow and Error Handling

- Reduce the use of `else` by structuring code with clear and explicit branches.
- Do not silently ignore errors.
- Clearly separate error-handling logic from normal execution paths.
- Prefer explicit error types or mechanisms over implicit error signaling.

---

## Modularity and Dependencies

- Organize code into well-defined, cohesive modules.
- Dependencies must flow in a single direction.
- Circular dependencies are not allowed.
- Minimize reliance on global state; define clear ownership when unavoidable.
- Depend on abstractions or interfaces rather than concrete implementations.
- Isolate external libraries behind dedicated layers.

---

## Testability and Maintainability

- Design code to be easy to test, especially in areas that change frequently.
- Limit side effects to well-defined boundaries.
- Code should be structured so that the impact of changes is predictable.
- Code that is difficult to test should be considered a maintenance risk.

---

## Logging

- Logging must be used sparingly and intentionally.
- Logs should exist only at meaningful boundaries or critical decision points.
- Do not log information that can be inferred directly from code flow.
- Avoid repetitive, verbose, or low-value logs.
- Logs must improve understanding of system behavior, not add noise.
- Logging must never be used as a substitute for proper error handling.
- Log messages must be clear, concise, and written in plain language.
- Avoid logging inside tight loops or high-frequency execution paths.
- Sensitive or unnecessary internal details must not be logged.
- The absence of a log should be the default; add logs only when they provide clear diagnostic value.