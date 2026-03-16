Create a git commit for the current staged or unstaged changes.

## Commit Message Rules

Follow these rules exactly:

1. **Lowercase**: entire message is lowercase (no capital letters anywhere)
2. **Concise**: one short sentence, under 72 characters
3. **No emoji**: never use emoji in commit messages
4. **No conventional commit prefixes**: no `feat:`, `fix:`, `chore:`, `docs:`, etc.
5. **No trailers**: NEVER add `Co-Authored-By`, `Signed-off-by`, or any trailer lines
6. **Granular**: one logical change per commit. if there are multiple unrelated changes, make multiple commits
7. **Descriptive**: explain what changed and why, not just "update file"

## Good Examples

- `add retry logic for failed api calls`
- `fix off-by-one in pagination offset`
- `remove deprecated user.legacy_id field`
- `switch token refresh from polling to websocket`
- `handle null response from payment gateway`

## Bad Examples (never do these)

- `Fix: Add retry logic` (capitalized, has prefix)
- `feat: add retry logic for API calls` (conventional commit prefix)
- `🐛 fix pagination bug` (emoji)
- `Update files` (vague)
- `Add retry logic\n\nCo-Authored-By: ...` (has trailer)

## Steps

1. Run `git status` and `git diff` (staged and unstaged) to understand all changes
2. Run `git log --oneline -5` to see recent commit style for context
3. Stage appropriate files (prefer specific files over `git add -A`)
4. Draft a commit message following the rules above
5. Create the commit using a heredoc format:
   ```
   git commit -m "$(cat <<'EOF'
   your lowercase commit message here
   EOF
   )"
   ```
6. Run `git status` to verify the commit succeeded

## Critical Rules

- NEVER add Co-Authored-By or Signed-off-by trailers
- NEVER use conventional commit prefixes (feat:, fix:, chore:, etc.)
- NEVER capitalize the commit message
- If there are no changes to commit, say so and stop
- Do not push unless explicitly asked
