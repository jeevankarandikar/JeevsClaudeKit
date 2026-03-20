Build in 3 phases (core → errors → polish): $ARGUMENTS

Build this feature in 3 committed phases:

## Phase 1: Core Functionality
1. Implement the bare minimum that works
2. No error handling, no edge cases, no polish
3. Run tests to verify core behavior
4. Commit: "core [feature] implementation"
5. STOP - show what was built, await approval

## Phase 2: Error Handling & Validation
1. Add input validation at system boundaries
2. Add error handling for failure cases
3. Handle edge cases (null, empty, concurrent, timeout)
4. Add/update tests for error scenarios
5. Commit: "add error handling for [feature]"
6. STOP - show changes, await approval

## Phase 3: Polish & Harden
1. Optimize performance if needed
2. Add logging for debugging
3. Ensure documentation is complete
4. Final test run - all green
5. Commit: "polish and harden [feature]"

Rules:
- Each phase produces working, committed code
- Easy to roll back to any phase
- Never skip ahead - complete each phase fully
- Show progress at each gate
