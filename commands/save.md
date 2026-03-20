Capture session learnings into CLAUDE.md and memory.

## Steps

1. **Read the current CLAUDE.md** in the project root

2. **Scan the conversation** for insights worth preserving:
   - **Error patterns**: errors encountered and how they were resolved
   - **Conventions discovered**: codebase patterns, naming rules, architectural decisions found during exploration
   - **Workarounds applied**: non-obvious solutions to tricky problems
   - **Architecture decisions**: structural choices made and why
   - **Debugging techniques**: what worked to find root causes
   - **Tool/dependency quirks**: unexpected behaviors of libraries, frameworks, or tools

3. **Classify each finding**:
   - **error-pattern**: specific error + fix (e.g., "postgres connection timeout → increase pool size")
   - **convention**: how this codebase does things (e.g., "all API routes use middleware chain X")
   - **workaround**: non-obvious fix (e.g., "must clear cache before running migrations")
   - **architecture-decision**: why something is structured a certain way
   - **debugging-technique**: approach that worked for a class of problems

4. **Route findings to the right place**:
   - **Project-specific** (conventions, architecture, known issues) → update CLAUDE.md sections:
     - Add to "Recent Changes" with today's date
     - Add any new "Known Issues"
     - Update "TODO" list
     - Add any new "Gotchas" discovered
     - Update "Conventions" if new patterns were established
   - **Personal/general** (debugging techniques, tool quirks, preferences) → save to memory system

5. **Present findings before writing** — show what will be saved and where, then wait for approval

6. If no CLAUDE.md exists, suggest running `/init` first

## Rules
- Only save genuinely useful patterns, not obvious things
- Include enough context that the learning is actionable in a future session
- If a learning duplicates something already in CLAUDE.md, update the existing entry instead of adding a new one
- Keep entries concise: one sentence for the pattern, one for when it applies
- Don't remove existing entries unless they're resolved
- Date-stamp recent changes
- Keep CLAUDE.md scannable, not verbose
