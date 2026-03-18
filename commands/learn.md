Extract reusable patterns from this session.

Scan the current conversation for insights worth preserving:

## What to Look For
1. **Error patterns**: errors encountered and how they were resolved
2. **Conventions discovered**: codebase patterns, naming rules, architectural decisions found during exploration
3. **Workarounds applied**: non-obvious solutions to tricky problems
4. **Architecture decisions**: structural choices made and why
5. **Debugging techniques**: what worked to find root causes
6. **Tool/dependency quirks**: unexpected behaviors of libraries, frameworks, or tools

## Classification
For each finding, classify it:
- **error-pattern**: specific error + fix (e.g., "postgres connection timeout → increase pool size")
- **convention**: how this codebase does things (e.g., "all API routes use middleware chain X")
- **workaround**: non-obvious fix (e.g., "must clear cache before running migrations")
- **architecture-decision**: why something is structured a certain way
- **debugging-technique**: approach that worked for a class of problems

## Where to Save
- **Project-specific** findings (conventions, architecture, known issues) → add to project's CLAUDE.md under `## Learnings` or `## Known Issues` or `## Gotchas` as appropriate
- **Personal/general** findings (debugging techniques, tool quirks, preferences) → save to memory system

## Rules
- Only extract genuinely useful patterns, not obvious things
- Include enough context that the learning is actionable in a future session
- If a learning duplicates something already in CLAUDE.md, update the existing entry instead of adding a new one
- Keep entries concise: one sentence for the pattern, one for when it applies
- Ask the user before writing to CLAUDE.md — present findings first
