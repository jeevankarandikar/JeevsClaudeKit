Comprehensive code review for: $ARGUMENTS

## Agents & Skills
Dispatch these agents in parallel for maximum coverage:
- `pr-review-toolkit:code-reviewer` — code quality, style, patterns
- `pr-review-toolkit:silent-failure-hunter` — error handling gaps, silent failures
- `pr-review-toolkit:pr-test-analyzer` — test coverage gaps
- `pr-review-toolkit:comment-analyzer` — comment accuracy
If the diff touches types/interfaces, also dispatch `pr-review-toolkit:type-design-analyzer`.
Synthesize all agent results into the output format below.

## Step 0: Context Gathering
1. Detect base branch:
   - `gh pr view --json baseRefName -q .baseRefName` (if PR exists)
   - `gh repo view --json defaultBranchRef -q .defaultBranchRef.name` (repo default)
   - fall back to `main`
2. `git fetch origin <base> --quiet && git diff origin/<base> --stat`
3. If no diff: say so and stop.
4. `git log --oneline -20` for recent context
5. Scan changed files for TODO/FIXME/HACK comments

## Pass 1: Critical (must fix before merge)

### SQL & Data Safety
- String interpolation in queries, TOCTOU races, missing validations

### Race Conditions
- Check-then-set without atomics, missing unique constraints, concurrent status transitions

### Input Trust Boundaries
- Unsanitized user input, LLM output written to DB without validation

### Error Handling
Build an Error & Rescue Map for new codepaths:
METHOD | FAILURE MODE | RESCUED? | TEST? | USER SEES? | LOGGED?
Any row with RESCUED=N + TEST=N + USER SEES=Silent → CRITICAL GAP

### Security
- Auth/authz checks, injection vectors, sensitive data exposure

## Pass 2: Informational (include in review, not blocking)

### Code Quality
- Naming clarity, DRY violations, dead code, pattern consistency with codebase

### Testing
- Coverage gaps, test quality, missing negative-path tests

### Performance
- N+1 queries, unbounded growth, missing indexes

### Documentation
- Public API docs, complex logic explanation

### Enum/Value Completeness
- New enum values traced through all consumers

### Conditional Side Effects
- Branches that forget side effects on one path

## Output Format
1. Summary: `Review: N issues (X critical, Y informational)`
2. For each CRITICAL: file:line, problem, recommended fix — mark as must-fix
3. For each informational: file:line, problem, suggested fix
4. Failure Modes Registry (if new codepaths):
   CODEPATH | FAILURE MODE | RESCUED? | TEST? | USER SEES? | LOGGED?
5. Positive: things done well (acknowledge good work)
