Systematic debugging protocol for: $ARGUMENTS

Follow this structured approach - no guessing:

## Step 1: Reproduce & Observe
1. Understand the symptoms described above
2. Find the relevant code path
3. Read the full stack trace or error output
4. Identify the exact file and line where the error originates

## Step 2: Gather Context
1. Read the failing code and its immediate dependencies
2. Check recent changes (git log, git diff) that may have introduced the issue
3. Look for similar patterns elsewhere in the codebase that work correctly
4. Check configuration, environment variables, and external dependencies

## Step 3: Root Cause Analysis
1. Form a hypothesis about the root cause
2. Verify the hypothesis by reading code - don't guess
3. Trace the data flow from input to the failure point
4. Identify the EXACT line/condition that causes the bug

## Step 4: Fix
1. Explain the root cause clearly
2. Implement the minimal fix that addresses the root cause
3. Verify the fix doesn't break other functionality
4. Run relevant tests

## Step 5: Prevent
1. Add a test that would have caught this bug
2. If this is a pattern that could recur, note it
3. Update CLAUDE.md with the finding if it's a significant gotcha

Rules:
- Never suggest a fix without understanding the root cause
- Read the code before speculating
- Prefer minimal, targeted fixes over broad refactors
- Document the fix for future reference
