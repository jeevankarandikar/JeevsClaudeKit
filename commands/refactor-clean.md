Identify and safely remove dead code in: $ARGUMENTS

## Agents & Skills
- Dispatch `code-simplifier:code-simplifier` agent to identify simplification opportunities alongside dead code
- After removal, dispatch `pr-review-toolkit:code-reviewer` agent to verify the cleanup didn't break patterns

If no target specified, analyze recently changed files.

## Step 1: Scan for Dead Code Candidates
Search for:
- **Unused imports**: imported but never referenced in the file
- **Unused functions**: defined but no callers found in the codebase
- **Unused variables**: assigned but never read
- **Commented-out code blocks**: more than 3 consecutive commented lines that look like code (not documentation)
- **Unreachable code**: code after return/throw/break/continue with no conditional path to reach it
- **Unused type definitions**: types/interfaces/structs with no references

## Step 2: Verify Each Candidate
For each candidate:
1. Grep the entire codebase for references (not just the current file)
2. Check for dynamic usage: string-based imports, reflection, serialization
3. Check if it's a public API that external consumers might use
4. Check if it's referenced in tests (test-only usage may still be valid)
5. Mark as: CONFIRMED (safe to remove) / UNCERTAIN (needs human judgment) / FALSE POSITIVE (actually used)

## Step 3: Remove in Batches
Group confirmed dead code by file. For each batch:
1. Remove the dead code
2. Run tests (if configured in CLAUDE.md)
3. If tests fail: revert the batch, mark items as UNCERTAIN
4. If tests pass: move to next batch

## Step 4: Report
- **Removed**: N items across M files
- **Skipped (tests failed)**: N items — list with explanations
- **Uncertain (needs review)**: N items — list with why
- **False positives**: N items — briefly note why they looked dead but aren't

## Rules
- Never remove code that's part of a public API without asking
- Never remove TODO/FIXME comments (those are intentional)
- Don't remove code that's behind feature flags — it may be upcoming work
- If in doubt, skip it — false negatives are better than broken code
- Keep the diff clean: only dead code removal, no style changes or refactoring
