# JeevsClaudeKit

Personal Claude Code power-user toolkit. Custom commands, hooks, plugins, and workflows for maximum development velocity.

**Last updated**: 2026-03-15

---

## Table of Contents

- [Quick Start](#quick-start)
- [What's Automatic vs Manual](#whats-automatic-vs-manual)
- [Commands Reference](#commands-reference)
- [Hooks Reference](#hooks-reference)
- [Plugins Reference](#plugins-reference)
- [CLAUDE.md Learning Loop](#claudemd-learning-loop)
- [Workflow Recipes](#workflow-recipes)
- [Tips & Power Tricks](#tips--power-tricks)
- [File Locations](#file-locations)
- [Customizing](#customizing)

---

## Quick Start

Everything is already installed. Open Claude Code and:

```bash
# In any project - initialize persistent memory
/init-project

# Plan before coding
/plan-feature add user authentication

# Test-driven development
/tdd password reset flow

# When done for the day
/update-memory
```

---

## What's Automatic vs Manual

### Runs Automatically (no action needed)

| What | How it Works | Where |
|------|-------------|-------|
| **Destructive command blocker** | Intercepts `rm -rf`, `git reset --hard`, `git push --force`, `DROP TABLE`, etc. before execution | `~/.claude/hooks/hooks.json` |
| **Sensitive file warning** | Warns when editing files containing `.env`, `credentials`, `secret`, `password`, `api_key`, `token` | `~/.claude/hooks/hooks.json` |
| **Co-Authored-By blocker** | Blocks commits containing `Co-Authored-By` or `Signed-off-by` trailers | `~/.claude/hooks/hooks.json` |
| **TypeScript diagnostics** | Real-time type errors, missing imports, etc. in TS projects | `typescript-lsp` plugin |
| **Security guidance** | Warns about potential security issues (XSS, injection, etc.) when editing files | `security-guidance` plugin |
| **Code simplification** | Agent auto-reviews code for clarity and maintainability when triggered | `code-simplifier` plugin |
| **Context7 docs lookup** | Pulls up-to-date library docs when you reference a library | `context7` plugin |
| **Plan mode default** | Claude starts in plan mode, researches before coding | `settings.json` defaultMode |
| **High effort** | Claude uses maximum thinking depth | `settings.json` effortLevel |
| **Explanatory output** | Educational insights with implementation choices | `settings.local.json` outputStyle |

### Manual - You Invoke These

| What | How to Use | When |
|------|-----------|------|
| `/tdd [feature]` | Type in Claude Code | Starting any feature or bugfix |
| `/plan-feature [desc]` | Type in Claude Code | Before writing significant code |
| `/debug [issue]` | Type in Claude Code | When you hit a bug |
| `/review [code/PR]` | Type in Claude Code | Before merging |
| `/perf [code]` | Type in Claude Code | Performance concerns |
| `/init-project` | Type in Claude Code | First time in a new project |
| `/progressive-build [feat]` | Type in Claude Code | Complex multi-phase features |
| `/devils-advocate [change]` | Type in Claude Code | Before shipping to production |
| `/explain [area]` | Type in Claude Code | Understanding unfamiliar code |
| `/update-memory` | Type in Claude Code | End of every work session |
| `/fast [task]` | Type in Claude Code | Routine tasks where you want minimal tokens |
| `/commit` | Type in Claude Code | Commit with enforced style conventions (custom) |
| `/commit-push-pr` | Type in Claude Code | Commit + push + create PR with enforced style (custom) |
| `/clean-gone` | Type in Claude Code | Clean up merged branches (plugin) |
| `/hookify` | Type in Claude Code | Create new hooks from patterns |
| `/simplify` | Type in Claude Code | Review changed code for quality |
| `/claude-md-management:revise-claude-md` | Type in Claude Code | Update CLAUDE.md with session learnings |

### Semi-Automatic (plugin-driven, triggers on context)

| What | Triggers When | Plugin |
|------|--------------|--------|
| **Superpowers: brainstorming** | Before any creative/feature work | superpowers |
| **Superpowers: systematic-debugging** | When encountering bugs | superpowers |
| **Superpowers: verification-before-completion** | Before claiming work is done | superpowers |
| **Superpowers: code-reviewer** | After completing a major step | superpowers |
| **Frontend design skill** | Building web UI components | frontend-design |
| **Claude-code-setup recommender** | Analyzing new codebases | claude-code-setup |

---

## Commands Reference

### `/tdd [feature description]`
**Purpose**: Enforces strict test-driven development.
**Flow**: Write failing tests -> Confirm they fail -> Commit tests -> STOP for approval -> Implement -> Refactor
**Best for**: Any new feature or bugfix. Forces you to think about behavior before implementation.
**Key rule**: No mocks unless absolutely necessary. Tests must be able to fail.

### `/plan-feature [feature description]`
**Purpose**: Research-first planning that prevents premature coding.
**Flow**: Search codebase -> Identify reusable code -> Design approach -> Present plan -> STOP for approval
**Best for**: Any feature that touches more than 1-2 files. Saves hours of rework.
**Key rule**: No code is written during planning.

### `/debug [error/symptom description]`
**Purpose**: Systematic root cause analysis instead of guessing.
**Flow**: Reproduce -> Gather context -> Root cause analysis -> Fix -> Add preventive test -> Update CLAUDE.md
**Best for**: Any bug. Especially good for "I have no idea why this is broken."
**Key rule**: Never suggest a fix without understanding the root cause.

### `/review [file/PR/code area]`
**Purpose**: 6-dimension code review.
**Checks**: Code quality, correctness, testing, security (OWASP), performance, documentation.
**Output**: Findings categorized as Critical / Warning / Suggestion / Positive.
**Best for**: Before every merge. Also great for self-review.

### `/perf [file or code area]`
**Purpose**: Performance deep-dive.
**Checks**: Big O complexity, N+1 queries, memory leaks, async pitfalls, caching opportunities.
**Output**: Each issue with location, impact estimate, and specific fix with before/after code.
**Best for**: When something feels slow, or before deploying to production.

### `/init-project`
**Purpose**: Bootstrap project memory.
**Flow**: Reads package.json/config -> Scans structure -> Generates CLAUDE.md with stack, commands, conventions.
**Best for**: First time using Claude Code in any project. Run once.

### `/progressive-build [feature]`
**Purpose**: Build in 3 committed phases with approval gates.
**Flow**: Phase 1 (core, commit) -> Phase 2 (error handling, commit) -> Phase 3 (polish, commit)
**Best for**: Complex features where you want rollback points.

### `/devils-advocate [change description]`
**Purpose**: Pre-deploy risk analysis.
**Checks**: Edge cases, load behavior, bad assumptions, external failures, security, race conditions, rollback plan.
**Output**: Each risk rated by likelihood and impact with mitigations.
**Best for**: Before any production deployment.

### `/fast [task description]`
**Purpose**: Efficiency mode for routine tasks.
**Behavior**: Minimal exploration, concise output, one-shot implementation, no educational insights.
**Best for**: Simple refactoring, renaming, boilerplate, CRUD operations, running commands.
**Saves**: 40-60% tokens compared to default high-effort mode on simple tasks.

### `/explain [area of codebase]`
**Purpose**: Onboarding-style walkthrough.
**Covers**: High-level overview, architecture, key decisions, gotchas, how to modify.
**Best for**: Joining a new project, understanding unfamiliar code, or documenting for teammates.

### `/update-memory`
**Purpose**: Capture session learnings into CLAUDE.md.
**Updates**: Recent changes, known issues, TODOs, gotchas, conventions.
**Best for**: End of every significant work session. Keeps project memory current.

---

## Hooks Reference

Hooks live in `~/.claude/hooks/hooks.json` and run automatically.

### Destructive Command Blocker
- **Type**: `preToolUse` on `Bash`
- **Triggers on**: `rm -rf /`, `rm -rf ~`, `rm -rf .`, `git reset --hard`, `git push --force`, `git push -f`, `git clean -fd`, `git checkout -- .`, `drop table`, `DROP TABLE`, `truncate table`, `TRUNCATE TABLE`, `> /dev/sda`, `mkfs.`, `dd if=`, fork bomb, `chmod -R 777`, `git branch -D main`, `git branch -D master`
- **Action**: Blocks execution (exit 2), requires you to explicitly confirm
- **Why**: Prevents catastrophic data loss from a single command

### Sensitive File Warning
- **Type**: `preToolUse` on `Edit`
- **Triggers on**: Files containing `.env`, `credentials`, `secret`, `password`, `api_key`, `API_KEY`, `private_key`, `token`
- **Action**: Shows warning, continues (exit 0)
- **Why**: Reminds you not to hardcode secrets

### Co-Authored-By Blocker
- **Type**: `preToolUse` on `Bash`
- **Triggers on**: `Co-Authored-By`, `co-authored-by`, `CO-AUTHORED-BY`, `Signed-off-by`, `signed-off-by`
- **Action**: Blocks execution (exit 2)
- **Why**: Prevents Claude from adding unwanted attribution trailers to commits. Claude's system prompt hard-codes a Co-Authored-By trailer -- this hook overrides that behavior globally.

### Creating New Hooks
Use `/hookify` to analyze conversation patterns and create new hooks automatically. Or edit `~/.claude/hooks/hooks.json` directly.

Hook types:
- `preToolUse` - Runs before a tool executes (can block with exit 2)
- `postToolUse` - Runs after a tool executes
- `userPromptSubmit` - Runs when you submit a prompt
- `stop` - Runs when Claude finishes responding

---

## Plugins Reference

### Always-On (enabled)

| Plugin | What it Does |
|--------|-------------|
| **superpowers** | Planning, debugging, code review, TDD, verification workflows. The "brain" plugin. |
| **context7** | Live documentation lookup. When you reference React, Next.js, etc., pulls current docs. |
| **typescript-lsp** | Real-time TypeScript diagnostics. Catches type errors, missing imports. |
| **security-guidance** | Warns about XSS, injection, unsafe patterns when editing files. |
| **claude-md-management** | Audit and improve CLAUDE.md files. |
| **code-simplifier** | Reviews code for clarity, consistency, maintainability. |
| **claude-code-setup** | Recommends automations (hooks, skills, MCP servers) for new projects. |
| **frontend-design** | Production-grade UI/UX with distinctive design (avoids "AI slop"). |
| **commit-commands** | `/commit`, `/commit-push-pr`, `/clean-gone` git workflows. |
| **hookify** | Create hooks from conversation patterns. `/hookify` to use. |

### Available but Disabled

| Plugin | What it Does | Enable When |
|--------|-------------|-------------|
| **feature-dev** | Full feature dev workflow with specialized agents | Large features (overlaps with superpowers) |
| **playwright** | Browser automation and E2E testing | E2E testing or web scraping needed |
| **serena** | Semantic code analysis via LSP | Deep refactoring (overlaps with TS LSP) |
| **supabase** | Supabase database/auth management | Working with Supabase projects |
| **greptile** | AI code review for GitHub/GitLab PRs | Want external PR review integration |
| **ralph-loop** | Continuous AI loops | Autonomous iterative development |

Enable/disable in `~/.claude/settings.json` under `enabledPlugins`.

---

## CLAUDE.md Learning Loop

The continuous learning loop is the most important pattern. It makes Claude remember your project across sessions.

### How it Works
1. `/init-project` generates a `CLAUDE.md` at your project root
2. Claude reads this file at the start of every session
3. As you work, Claude references it for conventions, known issues, etc.
4. `/update-memory` captures what you learned back into CLAUDE.md
5. Next session picks up where you left off

### Template Location
`~/.claude/CLAUDE.md-template` - copy into any project, or just use `/init-project`.

### What Goes in CLAUDE.md
- **Project Context**: Stack, package manager, versions
- **Key Commands**: Build, test, lint, dev server
- **Architecture**: Directory structure, entry points, data flow
- **Conventions**: Naming, imports, error handling, testing patterns
- **Recent Changes**: Date-stamped log of modifications
- **Known Issues**: Bugs, tech debt, quirks
- **TODO**: Active tasks
- **Gotchas**: Non-obvious things that cause confusion

### Best Practice
Run `/update-memory` at the end of every significant session. This takes 30 seconds and saves you 10 minutes of re-explaining context next time.

---

## Workflow Recipes

### Recipe 1: New Feature (Full Workflow)
```
/plan-feature [describe the feature]
# Review plan, approve
/tdd [feature name]
# Review tests, approve
# Implementation happens automatically
/review the changes just made
/devils-advocate deploying [feature]
/update-memory
/commit
```

### Recipe 2: Quick Bugfix
```
/debug [paste error or describe symptom]
# Fix is implemented
/review the bugfix
/update-memory
/commit
```

### Recipe 3: New Project Setup
```
/init-project
# CLAUDE.md is generated
# Start working, Claude now knows your project
```

### Recipe 4: Complex Feature with Checkpoints
```
/plan-feature [complex feature]
# Approve plan
/progressive-build [feature]
# Phase 1: Core -> approve
# Phase 2: Error handling -> approve
# Phase 3: Polish -> approve
/review all changes
/commit-push-pr
```

### Recipe 5: Pre-Deploy Checklist
```
/review the changes on this branch
/perf any new queries or hot paths
/devils-advocate deploying these changes
# Address findings
/commit-push-pr
```

### Recipe 6: Onboarding to Existing Project
```
/init-project                    # If no CLAUDE.md exists
/explain the overall architecture
/explain [specific area you'll work on]
```

---

## Tips & Power Tricks

### Model Optimization & Token Efficiency

Your setup is tuned for maximum intelligence by default. Here's when to shift gears:

**Current defaults** (in `settings.json`):
- `defaultMode: "plan"` - Think before acting (prevents expensive rewrites)
- `effortLevel: "high"` - Maximum reasoning depth

**Model switching strategy**:
| Task Type | Model | Effort | Why |
|-----------|-------|--------|-----|
| Architecture, complex algorithms, debugging unknowns | Opus (default) | High | These need deep reasoning |
| Routine coding, refactoring, tests, boilerplate | Sonnet (`/model sonnet`) | Medium | 80% cheaper, fast enough |
| Quick lookups, simple renames, formatting | Sonnet + `/fast` | Low | Minimal token burn |

**Built-in command**: `/fast [task]` - Switches Claude to efficiency mode (minimal tokens, no exploration, one-shot implementation). Use for routine tasks.

**Token-saving habits**:
1. **`/compact` before major work** - Compresses conversation history, frees 70% token space
2. **Scope your context explicitly** - "Focus on /src/api/auth/* only" prevents Claude from reading the whole codebase
3. **One task per session** - Use `/clear` between unrelated work to prevent cross-contamination
4. **Reference by path, not content** - "Read src/config.ts" instead of pasting the file contents
5. **Plan mode catches mistakes early** - Research is cheap, rewrites cost 10x more tokens
6. **Use `/progressive-build`** for large features - Each phase is self-contained, so if context runs out mid-feature, you have committed checkpoints

**When effort level matters**:
- `high` (default): Complex reasoning, architecture, debugging. Uses more thinking tokens but catches more issues.
- `medium`: Good for most daily coding. Reduce via `effortLevel` in settings.json if you want to save tokens globally.
- `low`: Quick tasks, simple edits. Set per-session when doing bulk routine work.

**Real savings**: Strategic model switching + context scoping + `/compact` usage = ~60-70% cost reduction at equivalent productivity.

### Prompting

1. **Be specific about output format**: "Return findings as JSON with severity ratings" beats "review this code"
2. **Use XML tags for complex context**: Wrap code, instructions, and context in tags for clarity
3. **Scope aggressively**: "Focus on /src/api/auth/* only" saves tokens and improves accuracy
4. **Chain prompts**: Don't try to do everything in one prompt. Plan -> Test -> Build -> Review -> Document

### Context Management

1. **Use `/compact` before major work** to free up 70% of token space
2. **One task per session** when possible - use `/clear` between unrelated work
3. **CLAUDE.md is your RAM** - keep it updated and Claude stays sharp
4. **Context window auto-compacts** - Claude will continue working across compactions, so don't stop tasks early

### Git Workflow

1. `/commit` creates commits with enforced conventions: lowercase, no emoji, no prefixes, no Co-Authored-By trailers
2. `/commit-push-pr` does commit + push + PR creation with the same conventions
3. `/clean-gone` removes local branches that have been merged remotely
4. Custom `/commit` and `/commit-push-pr` shadow the plugin versions with style enforcement

### Creating New Hooks

```bash
# Use hookify interactively
/hookify

# Or edit directly
~/.claude/hooks/hooks.json
```

Common hooks to consider adding:
- Warn when creating files outside the project directory
- Require test files when creating new source files
- Block commits without running tests first

### Creating New Commands

Create a `.md` file in `~/.claude/commands/` with your prompt. Use `$ARGUMENTS` as a placeholder for user input. That's it - it's immediately available as a slash command.

```markdown
# ~/.claude/commands/my-command.md
Do something specific with: $ARGUMENTS

## Steps
1. First thing
2. Second thing
```

---

## File Locations

| What | Path |
|------|------|
| Global commands | `~/.claude/commands/*.md` |
| Hooks | `~/.claude/hooks/hooks.json` |
| Settings (plugins, permissions) | `~/.claude/settings.json` |
| Local settings (output style) | `~/.claude/settings.local.json` |
| CLAUDE.md template | `~/.claude/CLAUDE.md-template` |
| Plugin marketplace | `~/.claude/plugins/marketplaces/claude-plugins-official/` |
| Auto memory | `~/.claude/projects/-Users-jeevankarandikar/memory/MEMORY.md` |
| This reference | `~/Documents/JeevsClaudeKit/README.md` |

---

## Customizing

### Add a new command
1. Create `~/.claude/commands/my-command.md`
2. Write your prompt with `$ARGUMENTS` for user input
3. It's immediately available as `/my-command`

### Add a new hook
1. Edit `~/.claude/hooks/hooks.json`
2. Add a new entry with `matcher` and `hooks` array
3. Hook types: `preToolUse`, `postToolUse`, `userPromptSubmit`, `stop`
4. Exit codes: `0` = continue, `2` = block

### Enable/disable a plugin
1. Edit `~/.claude/settings.json`
2. Set the plugin to `true` or `false` under `enabledPlugins`
3. Run `/reload-plugins` in Claude Code

### Change default mode
- In `~/.claude/settings.json`, change `defaultMode` to `plan` (think first) or `normal` (act immediately)

### Change effort level
- In `~/.claude/settings.json`, change `effortLevel` to `high`, `medium`, or `low`

---

## Sources & Credits

Built from:
- [Anthropic Skills Guide](https://github.com/anthropics/skills) (official)
- [The Complete Guide to Building Skills for Claude](https://docs.claude.com) (Anthropic PDF)
- [Anthropic Prompt Library](https://platform.claude.com/docs/en/resources/prompt-library/library)
- [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) community list
- [The Ultimate Guide to Claude Code](https://medium.com/@tonimaxx) by Toni Maxx
- Personal workflow iteration
