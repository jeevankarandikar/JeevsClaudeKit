Create a checkpoint of current work: $ARGUMENTS

## Step 1: Assess State
- `git status` — what's changed?
- `git diff --stat` — scope of changes
- Current branch name

## Step 2: Create Checkpoint
If $ARGUMENTS says "stash":
  `git stash push -m "checkpoint: $ARGUMENTS"`
Otherwise:
  `git add -A && git commit -m "checkpoint: <description>"`

Use a descriptive checkpoint name based on $ARGUMENTS or the current work.

## Step 3: Record Context
Display:
- **Checkpoint**: name/description
- **Branch**: current branch
- **Files changed**: count and list
- **What was being worked on**: brief summary of current task
- **What's done**: completed steps
- **What's left**: remaining work
- **Blockers**: anything preventing progress

## Step 4: Verify (if tests are configured)
Run the test command from CLAUDE.md.
Note pass/fail in the checkpoint summary.

## Rules
- Checkpoint commits use the format: `checkpoint: <description>`
- These are meant to be squashed or amended later, not final commits
- If there are no changes to checkpoint, say so and stop
