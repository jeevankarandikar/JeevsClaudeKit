Autonomous experiment loop for: $ARGUMENTS

Inspired by Karpathy's autoresearch. Iteratively modify, run, measure, and keep or discard changes to optimize a target metric.

## Agents & Skills
- Invoke `superpowers:brainstorming` skill to generate experiment ideas
- Dispatch `feature-dev:code-explorer` agent to understand the current implementation before experimenting

## Step 1: Setup
1. Identify the target file(s) to modify and the metric to optimize
2. Identify the run command (from CLAUDE.md, or ask the user)
3. Identify how to extract the metric from run output (grep pattern, log parsing, etc.)
4. Create or locate results tracking (a `results.tsv` or table in conversation)
5. Confirm setup with the user before starting

## Step 2: Establish Baseline
Run the current code as-is. Record:
- Metric value (the number we're optimizing)
- Any secondary metrics (memory, time, etc.)
- Git commit hash (short)

This is experiment 0. All future experiments are compared against this.

## Step 3: Experiment Loop
For each experiment:
1. **Hypothesize**: state what you're changing and why you expect it to improve the metric
2. **Modify**: change the target file(s) — one logical change per experiment
3. **Run**: execute the run command, capture output
4. **Measure**: extract the metric from output
5. **Decide**:
   - If metric improved: `git commit` with description, mark as `keep`
   - If metric unchanged or worse: `git checkout` to revert, mark as `discard`
   - If crashed: revert, mark as `crash`, diagnose before next attempt
6. **Log**: record in results table:
   EXPERIMENT | COMMIT | METRIC | STATUS | DESCRIPTION

Repeat until:
- User says stop
- N experiments completed (ask user for N, default 10)
- Metric stops improving for 3 consecutive experiments

## Step 4: Report
- Best result vs baseline: metric improvement, what changed
- Full experiment log table
- Top 3 changes that helped most
- Ideas not yet tried (for future runs)

## Rules
- ONE change per experiment — never combine multiple ideas in one run
- Always revert failed experiments cleanly before trying the next
- If the run command takes >5 minutes, warn the user and ask to continue
- Never modify test/evaluation harness code — only the target file(s)
- Simpler is better: if two approaches give similar results, keep the simpler one
- If stuck (3 consecutive discards), try a fundamentally different approach instead of tweaking the same idea
- STOP and ask before making architectural changes (new files, new dependencies)
