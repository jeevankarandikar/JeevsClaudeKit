Ship current work. Detects mode from context:

- **No args** → auto-detect default from CLAUDE.md (see below)
- **"commit"** → commit only, no push
- **"push"** → commit + push to current branch, no PR
- **"pr"** → full ship: verify + commit + push + PR
- **"verify" or "check"** → verify only, no changes

$ARGUMENTS

## Auto-detect default mode

When invoked with no args, grep CLAUDE.md for any of these signals to pick the default:

- Phrase `push to main`, `push-to-main`, `no PR`, `no pull request`, `worktree`, or an explicit `ship-mode: push` marker → default is **push** mode
- Otherwise → default is **commit** mode (safest fallback)

Explicit arguments always override auto-detect.

---

## Commit Message Rules (apply to ALL modes)

1. **Lowercase**: entire message is lowercase (no capital letters anywhere)
2. **Concise**: one short sentence, under 72 characters
3. **No emoji**: never use emoji in commit messages
4. **No conventional commit prefixes**: no `feat:`, `fix:`, `chore:`, `docs:`, etc.
5. **No trailers**: NEVER add `Co-Authored-By`, `Signed-off-by`, or any trailer lines
6. **Granular**: one logical change per commit
7. **Descriptive**: explain what changed and why, not just "update file"

---

## Mode: Commit Only (default)

1. Run `git status` and `git diff` to understand all changes
2. Run `git log --oneline -5` to see recent style
3. Stage appropriate files (prefer specific files over `git add -A`)
4. Create commit(s) using heredoc:
   ```
   git commit -m "$(cat <<'EOF'
   your lowercase commit message here
   EOF
   )"
   ```
5. Run `git status` to verify

---

## Mode: Push (commit + push, no PR)

For solo-on-main repos and worktree workflows.

1. Run commit flow above.
2. Before pushing to `main` under auto-detected push mode: show the commits that will land (`git log origin/main..HEAD --oneline`) and confirm once. In explicit `"push"` mode, skip the confirm — user already opted in.
3. `git push` (use `-u origin HEAD` if upstream not set).
4. Report: what was pushed and to where.

No PR created. Do not run the full PR pre-flight (merge base-branch, verify, etc.) — those belong in `pr` mode.

---

## Mode: Verify Only

### 1. Build
Run the build command from CLAUDE.md. Detect build system:
- `.xcodeproj` → `xcodebuild -scheme <scheme> build`
- `Package.swift` → `swift build`
- `package.json` → `npm run build` / `yarn build`
- `Cargo.toml` → `cargo build`
- `go.mod` → `go build ./...`
If not configured: skip and note "build: not configured"

### 2. Type Check
Run type-check from CLAUDE.md if documented. Skip if not.

### 3. Lint
Run lint from CLAUDE.md if documented. Skip if not.

### 4. Tests
Run tests from CLAUDE.md if documented. Skip if not.

### 5. Console Audit
Search changed files (`git diff --name-only HEAD`) for debug statements:
- `print(` in .swift files (excluding test files)
- `console.log` / `debugger` in .js/.ts/.jsx/.tsx files
- `binding.pry` / `puts` in .rb files
- `print(` in .py files (excluding test files)
- `dd(` in .php files
- `NSLog(` / `os_log(` in .swift files

### 6. Git Status
Show uncommitted changes. Flag untracked files that should be committed.

Output format:
```
[PASS] build (2.3s)
[FAIL] types (1.1s) — 3 errors
[SKIP] lint — not configured
```
If any step fails: show errors and STOP.

---

## Mode: Full Ship (PR)

### Pre-Flight
1. If on main/master: STOP — "ship from a feature branch"
2. Detect base branch:
   - `gh pr view --json baseRefName -q .baseRefName` (if PR exists)
   - `gh repo view --json defaultBranchRef -q .defaultBranchRef.name`
   - fall back to `main`
3. `git fetch origin <base> && git merge origin/<base> --no-edit`
   - If merge conflicts: STOP and show them
4. Run verify mode (above)

### Quick Pre-Landing Scan
Scan `git diff origin/<base>` for:
- String interpolation in SQL queries
- New TODO/FIXME added in this diff
- Hardcoded credentials, API keys, tokens
- Debug statements left in
Warn before pushing if any found.

### Ship It
1. Stage and commit with rules above
2. Push: `git push -u origin HEAD`
3. Create PR:
   ```
   gh pr create --title "lowercase pr title" --body "$(cat <<'EOF'
   ## summary
   - what changed and why

   ## test plan
   - [ ] verification steps
   EOF
   )"
   ```
4. Return the PR URL

---

## Critical Rules
- NEVER add Co-Authored-By or Signed-off-by trailers
- NEVER use conventional commit prefixes
- NEVER capitalize commit messages or PR titles
- If there are no changes, say so and stop
- Do not push unless mode is "pr" or user explicitly asks
