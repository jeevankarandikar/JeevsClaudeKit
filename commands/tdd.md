Strict TDD workflow for: $ARGUMENTS

Follow this exact sequence:

## Phase 1: Write Failing Tests
1. Analyze the requirements described above
2. Write comprehensive test cases that MUST fail:
   - Happy path tests
   - Edge cases (null, empty, extreme values)
   - Error scenarios
   - Integration tests where applicable
3. Run the tests and confirm they ALL FAIL
4. Output results summary:
   - Test file path
   - Number of tests
   - All failures listed
5. Commit the failing tests with message: "test: add failing tests for [feature]"

## Phase 2: STOP - Await Approval
Present the test plan and WAIT for explicit approval before implementing.

## Phase 3: Implement
1. Write the minimum code to make tests pass
2. Run tests after each meaningful change
3. No mocks unless absolutely necessary - prefer real integrations
4. Continue until ALL tests pass

## Phase 4: Refactor
1. Clean up implementation while keeping tests green
2. Check for DRY violations, naming clarity, complexity
3. Run tests one final time to confirm

Rules:
- No skipping tests. No shortcuts.
- Tests must actually test real behavior, not just exist.
- If a test can't fail, it's not a real test - rewrite it.
