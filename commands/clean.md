Clean up: $ARGUMENTS

Full repo cleanup — dead code, repo organization, file consolidation, and reference updates. If no target specified, analyze recently changed files.

## Phase 1: Dead Code Scan

Search for:
- **Unused imports**: imported but never referenced in the file
- **Unused functions**: defined but no callers found in the codebase
- **Unused variables**: assigned but never read
- **Commented-out code blocks**: 3+ consecutive commented lines that look like code (not documentation)
- **Unreachable code**: code after return/throw/break with no conditional path
- **Unused type definitions**: types/interfaces/structs with no references
- **Duplicated code**: identical functions/blocks across multiple files → extract to shared utility

### Verify Each Candidate
1. Grep the entire codebase for references (not just the current file)
2. Check for dynamic usage: string-based imports, reflection, serialization
3. Check if it's a public API or referenced in tests
4. Mark as: CONFIRMED / UNCERTAIN / FALSE POSITIVE

## Phase 2: Repo Organization

Scan for:
- **Root clutter**: files at project root that belong in subdirectories
- **Redundant directories**: multiple dirs serving the same purpose (merge them)
- **Superseded files**: old versions of files that have been replaced (check git history exists)
- **Scattered related files**: files that should be grouped together
- **Naming inconsistencies**: mismatched naming conventions across dirs

## Phase 3: File Consolidation

Look for:
- **Small files that should be one**: multiple tiny files (<30 lines) covering the same topic → consolidate
- **Deprecated scripts/tools**: code that CLAUDE.md or README says not to use → delete
- **Stale configs**: config files referencing old paths, deleted files, or renamed directories

## Phase 4: Reference Updates

After any moves/renames/deletes, update ALL references:
- CLAUDE.md path references
- README.md structure and setup instructions
- .gitignore patterns
- Import paths in source code
- Any cross-file references

## Phase 5: Remove & Report

Group confirmed changes by type. For each batch:
1. Make the change
2. Run tests if configured
3. If tests fail: revert, mark as UNCERTAIN

### Report
- **Dead code removed**: N items across M files
- **Files moved/consolidated**: list
- **Files deleted**: list (confirm in git history)
- **References updated**: list
- **Uncertain (needs review)**: list with reasoning

## Rules
- Never remove code that's part of a public API without asking
- Never remove TODO/FIXME comments
- Don't remove code behind feature flags
- If in doubt, skip it
- Keep diffs clean: no style changes mixed with cleanup
- Always verify references are updated after any move/rename
