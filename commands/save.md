Capture session learnings across up to three doc surfaces. Cheap on tokens — append only, never regenerate.

## Doc surfaces

This command touches whichever of these exist in the project. If a file is missing, skip it silently (no prompt, no auto-create).

1. `docs/changelog.md` — compact what-shipped, one bullet per change
2. `docs/journal.md` — themed subsections with terse technical bullets + open questions
3. `CLAUDE.md` — project context, update only the "current state" or "recent changes" section

## Rules (apply to every step)

- **Append, don't regenerate.** Read only the top 40 lines to find today's date header. Use Edit to insert under an existing header. Use Write only when creating a brand-new section at the top.
- **No approval gate.** Just do it and report what was appended.
- **No conversation scan.** Log what the user told you to log, or the last few concrete changes from the current session. Don't re-read the whole conversation.
- **Lowercase**, match existing voice in each file.
- **Resolve today's date** once, reuse across all steps. Format matches the file's existing convention (e.g. `april 13, 2026`).

## Step 1: changelog.md

Skip if file doesn't exist.

- Read top 40 lines. Find today's `## <month day, year>` header.
- If today's section exists: append new bullets under it with Edit.
- If not: insert a new `## <month day, year>` section at the top (below any intro paragraph) with Write's equivalent via Edit at a known anchor.
- Bullet format: `- **<short title>**: <one-to-two sentences, 80–180 chars>`.
- Never touch previous days.

## Step 2: journal.md

Skip if file doesn't exist.

- Same append rule as step 1.
- Today's header format typically: `## <month day, year> — <session theme>`.
- Under it, add bold subsection titles and terse bullets (1–3 sentences each).
- Capture decisions, trade-offs, and open questions — not a replay of what's in changelog.

## Step 3: CLAUDE.md

- Find the "current state" section (may be named `current state (<date>)`, `Recent Changes`, or similar). Update only that section.
- Do not touch repo tree, critical rules, gotchas, or reference tables unless they actually changed this session.
- If CLAUDE.md exceeds 15K chars, flag it and suggest which section to move to a reference file. Do not auto-move.

## Step 4: memory (optional)

- Only save to `~/.claude/projects/.../memory/` if there's a genuinely reusable pattern for future sessions.
- Skip entirely otherwise. Do not save ephemeral task state.

## Output

After all applicable steps, print a one-line summary per file touched:

```
changelog.md: +3 bullets under april 13, 2026
journal.md: +1 subsection under april 13, 2026 — onboarding overhaul
CLAUDE.md: current state section updated (shipped +2, next +1)
memory: skipped — nothing new
```
