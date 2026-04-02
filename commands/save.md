Capture session learnings and update project docs.

Handles three things in one pass:
1. **CLAUDE.md** — update with session findings (or create via init if missing)
2. **Journal** — write today's dev journal entry
3. **Memory** — save personal/general learnings to memory system

## Step 1: Check for CLAUDE.md

If no CLAUDE.md exists at the project root, run init first:
1. Read package.json, Cargo.toml, pyproject.toml, go.mod, .xcodeproj, or equivalent
2. Scan directory structure, config files, test setup
3. Create CLAUDE.md with: project context, stack, build/test/lint commands, conventions, key paths
4. Then continue with steps below.

## Step 2: Scan the Conversation

Look for insights worth preserving:
- **Error patterns**: errors encountered and how they were resolved
- **Conventions discovered**: codebase patterns, naming rules, architectural decisions
- **Workarounds applied**: non-obvious solutions to tricky problems
- **Architecture decisions**: structural choices made and why
- **Tool/dependency quirks**: unexpected behaviors of libraries or frameworks
- **New gotchas**: things that would trip up a future session

## Step 3: Update CLAUDE.md

Route project-specific findings to the right sections:
- Add to "Recent Changes" with today's date
- Add any new "Known Issues"
- Update "Current Sprint" task statuses
- Add any new "Gotchas" discovered
- Update paths if files were moved/renamed

Keep entries concise. Don't duplicate existing entries — update them.

## Step 4: Update Journal

Find the journal file (check `docs/journal.md`, `JOURNAL.md`, or `journal.md`). If it doesn't exist, create at `docs/journal.md`.

Write today's entry at the TOP (newest first):

```markdown
## YYYY-MM-DD — [short theme/title]

### what happened
- [key events, work done]

### key decisions
- [directional choices, scope changes]

### what's next
- [concrete next steps]

### open questions
- [unresolved items]
```

If today already has an entry, update it rather than duplicating.

## Step 5: Save to Memory

Route personal/general learnings (debugging techniques, tool quirks, preferences) to the memory system. Only save genuinely useful patterns, not obvious things.

## Step 6: Present Before Writing

Show what will be saved and where. Wait for approval before writing.

## Rules
- Only save genuinely useful patterns
- Include enough context for actionability in future sessions
- Keep CLAUDE.md scannable, not verbose
- Date-stamp recent changes
- Be specific about what was built, not just what was discussed
- Lowercase in journal entries (match project style)
