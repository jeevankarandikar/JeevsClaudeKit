Build for: $ARGUMENTS

Detects the right mode automatically based on context:
- **Build errors detected?** → fix-build mode (fix one at a time)
- **New feature or $ARGUMENTS says "tdd"?** → TDD mode (tests first)
- **Otherwise** → phased build (core → errors → polish)

---

## Mode: Fix Build

### Step 1: Detect Build System
Look for build commands in this order:
1. CLAUDE.md "Build" or "Key Commands" section
2. `ios/project.yml` (xcodegen-managed) → `cd ios && xcodegen generate && xcodebuild -scheme <scheme> build`
3. `website/package.json` → `cd website && npx next build`
4. `.xcodeproj` / `.xcworkspace` at repo root → `xcodebuild -scheme <scheme> build`
5. `Package.swift` → `swift build`
6. `package.json` scripts: `build`, `compile`, `tsc`
7. `Cargo.toml` → `cargo build`
8. `go.mod` → `go build ./...`
9. `Makefile` → `make`
10. Ask the user if nothing is detected

Note on xcodegen: if `ios/project.yml` exists, always run `xcodegen generate` before `xcodebuild`. The `.xcodeproj` is generated and may be stale.

### Step 2: Fix Loop
For each error (one at a time):
1. Read the file around the error line
2. Understand the root cause
3. Apply the minimal fix
4. Re-run the build to verify
5. If the fix caused new errors: revert and try differently

Repeat until build passes or 10 iterations reached.

Rules:
- ONE error at a time, then re-verify
- Minimal changes only — fix the error, don't refactor
- Never suppress errors with `@ts-ignore`, `// swiftlint:disable`, `#[allow()]`, or similar
- Never delete code to fix type errors (fix the types instead)
- If stuck after 3 attempts on the same error, STOP and explain

---

## Mode: TDD

### Phase 1: Write Failing Tests
1. Analyze the requirements
2. Write comprehensive tests that MUST fail: happy path, edge cases, error scenarios
3. Run tests and confirm they ALL FAIL
4. Commit: `add failing tests for [feature]`

### Phase 2: STOP — Await Approval
Present the test plan and WAIT for explicit approval.

### Phase 3: Implement
1. Write minimum code to make tests pass
2. Run tests after each meaningful change
3. No mocks unless absolutely necessary

### Phase 4: Refactor
1. Clean up while keeping tests green
2. Run tests one final time

---

## Mode: Phased Build

### Phase 1: Core Functionality
1. Implement the bare minimum that works
2. No error handling, no edge cases, no polish
3. Run tests to verify core behavior
4. Commit: `core [feature] implementation`
5. STOP — show what was built, await approval

### Phase 2: Error Handling & Validation
1. Add input validation at system boundaries
2. Add error handling for failure cases
3. Handle edge cases (null, empty, concurrent, timeout)
4. Commit: `add error handling for [feature]`
5. STOP — show changes, await approval

### Phase 3: Polish & Harden
1. Optimize performance if needed
2. Final test run — all green
3. Commit: `polish [feature]`

---

## Report (all modes)
- Build status: PASS / FAIL
- Errors fixed / tests passing: N
- Files modified: list
