Review and reflect. Detects mode from $ARGUMENTS:

- **Timeframe (24h, 7d, 14d, 30d)** → engineering retrospective from git history
- **"experiment" + target** → autonomous modify → measure → decide loop

$ARGUMENTS

---

## Mode: Retrospective (default)

Analyze git history for the given window (default: 7d).

### Data Gathering
- `git log --since="<window>" --pretty=format:"%H|%an|%ai|%s" --no-merges`
- Insertion/deletion counts via diff-tree
- New files added
- Time distribution of commits

### Metrics Table
| metric | value |
|--------|-------|
| commits | N |
| insertions | N |
| deletions | N |
| test LOC ratio | N% |
| active days | N of N possible |

### Session Detection
Group commits by 45-minute gap:
- **Deep sessions** (>2 hours): count and average length
- **Medium sessions** (30min-2hr): count
- **Micro sessions** (<30min): count
Flag if micro sessions dominate (>60%) — may indicate context-switching.

### Commit Type Breakdown
Classify each commit: features, fixes, refactoring, tests, docs, config.

### Hotspot Analysis
Top 10 most-changed files by commit count. Flag 5+ changes as potential churn.

### Shipping Streak
Consecutive days with at least 1 commit. Current streak and longest in window.

### Narrative
1. **What went well**: patterns, velocity, focus
2. **Where to improve**: churn, gaps, imbalances
3. **3 habits for next week**: specific, actionable

Output to conversation only — do not write files.

---

## Mode: Experiment

Autonomous modify → measure → decide loop (inspired by Karpathy's autoresearch).

### Setup
1. Identify target file(s) and metric to optimize
2. Identify run command (from CLAUDE.md or ask)
3. Identify how to extract metric from output
4. Confirm setup with user before starting

### Establish Baseline
Run current code as-is. Record metric value, secondary metrics, git hash. This is experiment 0.

### Experiment Loop
For each experiment:
1. **Hypothesize**: what you're changing and why
2. **Modify**: one logical change
3. **Run**: execute, capture output
4. **Measure**: extract metric
5. **Decide**:
   - Improved → `git commit`, mark `keep`
   - Unchanged/worse → `git checkout` to revert, mark `discard`
   - Crashed → revert, mark `crash`, diagnose
6. **Log**: EXPERIMENT | COMMIT | METRIC | STATUS | DESCRIPTION

Repeat until: user says stop, N experiments done (default 10), or 3 consecutive no-improvement.

### Report
- Best result vs baseline
- Full experiment log
- Top 3 changes that helped most
- Ideas not yet tried

Rules:
- ONE change per experiment
- Always revert failed experiments before next
- Never modify test/evaluation harness
- STOP before making architectural changes
