Incrementally fix build errors for: $ARGUMENTS

## Step 1: Detect Build System
Look for build commands in this order:
1. CLAUDE.md "Build" command (if documented)
2. `package.json` scripts: `build`, `compile`, `tsc`
3. `Cargo.toml` → `cargo build`
4. `go.mod` → `go build ./...`
5. `Makefile` → `make`
6. Ask the user if nothing is detected

## Step 2: Run Build
Execute the build command, capture full output (stdout + stderr).

## Step 3: Parse Errors
Extract a structured list of errors:
- File path
- Line number
- Error message
- Error type/code if available

Sort by file, then by line number.

## Step 4: Fix Loop
For each error (one at a time):
1. Read the file around the error line
2. Understand the root cause
3. Apply the minimal fix
4. Re-run the build to verify the fix worked and didn't introduce new errors
5. If the fix caused new errors: revert and try a different approach

Repeat until the build passes or 10 iterations are reached.

## Rules
- Fix ONE error at a time, then re-verify
- Minimal changes only — fix the error, don't refactor surrounding code
- Never suppress errors with `@ts-ignore`, `// eslint-disable`, `#[allow()]`, or similar
- Never modify test files to make them pass
- Never delete code to fix type errors (fix the types instead)
- If an error requires a design decision, STOP and ask the user
- If stuck after 3 attempts on the same error, STOP and explain

## Report
When done:
- Errors fixed: N
- Errors remaining: N (with explanations)
- Files modified: list
- Build status: PASS / FAIL
