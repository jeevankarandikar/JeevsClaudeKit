Commit current changes, push to remote, and create a pull request.

## Agents & Skills
- Invoke `superpowers:verification-before-completion` skill before committing — run all checks first
- During Quick Pre-Landing Scan, dispatch `pr-review-toolkit:silent-failure-hunter` agent on the diff

## Pre-Flight
1. If on main/master: STOP — "ship from a feature branch"
2. Detect base branch:
   - `gh pr view --json baseRefName -q .baseRefName` (if PR exists)
   - `gh repo view --json defaultBranchRef -q .defaultBranchRef.name` (repo default)
   - fall back to `main`
3. `git fetch origin <base> && git merge origin/<base> --no-edit`
   - If merge conflicts: STOP and show them
4. If a test command is documented in CLAUDE.md: run it
   - If tests fail: STOP and show failures

## Commit Message Rules

Follow these rules exactly:

1. **Lowercase**: entire message is lowercase (no capital letters anywhere)
2. **Concise**: one short sentence, under 72 characters
3. **No emoji**: never use emoji in commit messages
4. **No conventional commit prefixes**: no `feat:`, `fix:`, `chore:`, `docs:`, etc.
5. **No trailers**: NEVER add `Co-Authored-By`, `Signed-off-by`, or any trailer lines
6. **Granular**: one logical change per commit. if there are multiple unrelated changes, make multiple commits
7. **Descriptive**: explain what changed and why, not just "update file"

## PR Title Rules

- Same rules as commit messages: lowercase, no emoji, no prefixes, concise
- Under 70 characters

## Steps

1. Run `git status` and `git diff` to understand all changes
2. Run `git log --oneline -5` to see recent commit style
3. Stage appropriate files (prefer specific files over `git add -A`)
4. Create commit(s) following the rules above, using heredoc format:
   ```
   git commit -m "$(cat <<'EOF'
   your lowercase commit message here
   EOF
   )"
   ```
5. Create a new branch if on main/master:
   ```
   git checkout -b descriptive-branch-name
   ```
6. Push to remote:
   ```
   git push -u origin HEAD
   ```

## Quick Pre-Landing Scan
Before pushing, scan `git diff origin/<base>` for:
- String interpolation in SQL queries
- New TODO/FIXME added in this diff
- Hardcoded credentials, API keys, tokens
- Console.log / debugger / binding.pry left in
Warn before pushing if any found.

7. Create PR using `gh pr create`:
   ```
   gh pr create --title "lowercase pr title" --body "$(cat <<'EOF'
   ## summary
   - what changed and why

   ## test plan
   - [ ] verification steps
   EOF
   )"
   ```
8. Return the PR URL

## Critical Rules

- NEVER add Co-Authored-By or Signed-off-by trailers
- NEVER use conventional commit prefixes
- NEVER capitalize commit messages or PR titles
- PR body uses lowercase headers (## summary, not ## Summary)
- If there are no changes to commit, say so and stop
