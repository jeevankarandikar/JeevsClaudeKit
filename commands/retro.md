Engineering retrospective for this project.

Analyze git history for the given time window: $ARGUMENTS (default: 7d, accepts 24h/7d/14d/30d)

## Data Gathering
Run these git commands to collect data:
- `git log --since="<window>" --pretty=format:"%H|%an|%ai|%s" --no-merges`
- `git log --since="<window>" --pretty=format:"%H" --no-merges | xargs -I{} git diff-tree --no-commit-id --numstat {} | awk '{ins+=$1; del+=$2} END {print ins, del}'`
- `git log --since="<window>" --diff-filter=A --name-only --pretty=format:""`
- `git log --since="<window>" --pretty=format:"%ai"` (for time distribution)

## Metrics Table
| metric | value |
|--------|-------|
| commits | N |
| contributors | N |
| insertions | N |
| deletions | N |
| test LOC ratio | N% of insertions in test files |
| active days | N of N possible |

## Session Detection
Group commits by author with 45-minute gap threshold:
- **Deep sessions** (>2 hours): count and average length
- **Medium sessions** (30min-2hr): count
- **Micro sessions** (<30min): count
Flag if micro sessions dominate (>60% of total) — may indicate context-switching.

## Commit Type Breakdown
Classify each commit message:
- Features (new functionality)
- Fixes (bug fixes)
- Refactoring (restructuring without behavior change)
- Tests (test additions/modifications)
- Docs (documentation)
- Config (build, CI, dependencies)

## Hotspot Analysis
Top 10 most-changed files by commit count:
FILE | CHANGES | INSERTIONS | DELETIONS
Flag any file with 5+ changes as potential churn — may need refactoring or better abstraction.

## Commit Time Distribution
Hourly histogram (0-23h):
- Peak productivity hours
- Late-night clusters (flag if >20% of commits after 10pm)

## Shipping Streak
Consecutive days with at least 1 commit. Current streak and longest streak in window.

## Narrative
Based on the data above, write a brief narrative:
1. **What went well**: patterns, velocity, focus areas
2. **Where to improve**: churn, gaps, imbalances
3. **3 habits for next week**: specific, actionable recommendations

Output everything to conversation only — do not write any files.
