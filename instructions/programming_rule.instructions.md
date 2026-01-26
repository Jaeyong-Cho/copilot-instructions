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
- Assertions must check meaningful preconditions, postconditions, or internal invariants.
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

---

## Function Documentation (Doxygen Style)

- **Every function must be documented using Doxygen-style comments.**
- Documentation must be colocated immediately above the function definition.
- Doxygen comments are mandatory even for private or internal functions.

### Required Doxygen Tags

Each function documentation block must include, at minimum:

- `@brief`  
  - A concise, single-sentence summary of the function’s responsibility.
- `@param`  
  - One entry per parameter.
  - Each parameter description must state:
    - Expected constraints
    - Semantic meaning
    - Relevant preconditions
- `@return`  
  - Description of the return value.
  - Must explicitly state postconditions related to the return value.
- `@pre`  
  - Formalized preconditions required before invocation.
- `@post`  
  - Formalized postconditions guaranteed after successful execution.
- `@throws` / `@error` (language-appropriate)  
  - All explicit error conditions or failure modes.

### Documentation Rules

- Documentation must describe **intent and contract**, not implementation details.
- Preconditions and postconditions in documentation must align with:
  - Assertions in the function body
  - Test cases validating the function
- Documentation must be kept accurate; outdated documentation is considered a defect.
- If a function cannot be clearly documented using these tags, its design must be reconsidered.

---

## Test Case Requirements

- Every function **must provide at least one concrete, executable test example**.
- Test examples must demonstrate:
  - A valid invocation that satisfies all preconditions
  - Verification of all stated postconditions
- Tests must be deterministic and repeatable.

---

## Test Execution and Visibility

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
- Untested functions must be discoverable via automated reports.
- Untested functions must remain visible in review and CI workflows.

---

## Test Pyramid and Instrumented Testing

- The test strategy must follow the **test pyramid**:
  - Unit tests (primary, isolated, fast)
  - Integration tests (component interactions)
  - End-to-End tests (full system behavior)
- Instrumented testing must be supported at all levels.
- Instrumentation must allow inspection of:
  - Execution paths
  - State transitions
  - Input/output boundaries
- All test levels must be executable through the **single canonical test command** with clear breakdowns.

---

## Naming Conventions

- Names must clearly express intent and responsibility.
- Function names should start with verbs.
- Class and type names should be nouns.
- Boolean variables should use prefixes such as `is`, `has`, or `can`.

---

## Code Readability

- Code must be clear, consistent, and readable.
- Avoid magic numbers; use named constants.
- Keep line length within 100–120 characters.
- Separate logical sections with blank lines.

---

## Control Flow and Error Handling

- Prefer early returns over deep nesting.
- Do not silently ignore errors.
- Separate error-handling paths from normal execution.
- Prefer explicit error types.

---

## Modularity and Dependencies

- Organize code into cohesive modules.
- Dependencies must flow in a single direction.
- Circular dependencies are not allowed.
- External libraries must be isolated behind abstraction layers.

---

## Testability and Maintainability

- Limit side effects to well-defined boundaries.
- Design for predictable change impact.
- Code that is difficult to test is a maintenance risk.

---

## Logging

- Logging must be **sufficiently detailed to allow clear understanding of execution flow**.
- Logs must be written at **key execution points** (e.g., state transitions, decision boundaries, external interactions).
- Logging must support **traceability, debugging, and post-mortem analysis**.
- Logs must be **intentional and semantically meaningful**.
- Logging must never replace proper error handling.
- Logging in tight or high-frequency execution paths must be **explicitly justified**.