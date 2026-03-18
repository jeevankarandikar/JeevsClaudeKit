Run all verification checks in sequence. Stop on first failure.

## Agents & Skills
- Invoke `superpowers:verification-before-completion` skill — evidence before assertions

## Pipeline

### 1. Build
Run the build command from CLAUDE.md (if documented).
If not configured: skip and note "build: not configured"

### 2. Type Check
Run the type-check command from CLAUDE.md (if documented).
If not configured: skip and note "types: not configured"

### 3. Lint
Run the lint command from CLAUDE.md (if documented).
If not configured: skip and note "lint: not configured"

### 4. Tests
Run the test command from CLAUDE.md (if documented).
If not configured: skip and note "tests: not configured"

### 5. Console Audit
Search changed files (`git diff --name-only HEAD`) for debug statements:
- `console.log` (in .js/.ts/.jsx/.tsx files)
- `debugger` (in .js/.ts/.jsx/.tsx files)
- `binding.pry` (in .rb files)
- `print(` (in .py files, excluding test files)
- `puts ` (in .rb files)
- `dd(` (in .php files)

### 6. Git Status
Show uncommitted changes. Flag any untracked files that look like they should be committed.

## Output Format
For each step, show:
```
[PASS] build (2.3s)
[FAIL] types (1.1s) — 3 errors
[SKIP] lint — not configured
```

If a step fails: show the error output and STOP.
If all steps pass: `Verification complete: all checks passed`

## Rules
- Run steps sequentially — later steps are pointless if earlier ones fail
- Use the exact commands from CLAUDE.md, don't guess
- If no commands are configured at all, tell the user to add them to CLAUDE.md
- Keep output concise — show full errors only for failures
