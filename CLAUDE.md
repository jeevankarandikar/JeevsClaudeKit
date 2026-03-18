# CLAUDE.md

## Project Context
- **Name**: JeevsClaudeKit
- **Purpose**: Personal Claude Code toolkit reference and configuration hub
- **Stack**: Markdown documentation, JSON config, shell scripts
- **Location**: ~/Documents/JeevsClaudeKit

## Key Paths
- **Commands**: `~/.claude/commands/*.md` (25 commands)
- **Hooks**: `~/.claude/hooks/hooks.json` (5 hooks)
- **Settings**: `~/.claude/settings.json` (16 official plugins + ECC via community marketplace)
- **Template**: `~/.claude/CLAUDE.md-template`
- **Memory**: `~/.claude/projects/-Users-jeevankarandikar/memory/MEMORY.md`

## Conventions

### Commits
- lowercase only, no capital letters anywhere in the message
- concise: one short sentence, under 72 characters
- no emoji in commit messages
- no conventional commit prefixes (`feat:`, `fix:`, `chore:`, `docs:`, etc.)
- no trailers: never add `Co-Authored-By`, `Signed-off-by`, or any trailer lines
- granular: one logical change per commit
- good: `add retry logic for failed api calls`, `fix off-by-one in pagination offset`
- bad: `Fix: Add retry logic`, `feat: add retry`, `🐛 fix bug`, `Update files`

### READMEs
- lowercase headers preferred
- technical and direct, no marketing language
- include repo structure tree for non-trivial projects
- include stack/dependencies table
- setup instructions in code blocks
- no emoji in headers or body text

### Code Comments
- explain why, not what
- shape annotations for tensor/matrix operations (e.g. `# [batch, seq_len, hidden]`)
- python: google-style docstrings
- js/ts/swift: minimal comments, let types and naming do the work
- never add comments to code you didn't change

### Documentation
- do not create unnecessary .md files
- CLAUDE.md is the single source of truth for project context
- no README.md creation unless explicitly requested

### Toolkit Conventions
- command files are plain markdown with `$ARGUMENTS` placeholders
- hook matchers use `input_contains_any` arrays for pattern matching
- plugin names follow `name@marketplace` format
- all commands use structured phases with STOP/approval gates

## Agent & Skill Routing

When the user's intent matches a pattern below, use the specified agents and skills automatically. Do NOT wait for a slash command — route based on what the user is asking for.

### Planning & Scoping
- "plan", "design", "architect", "how should we build" → invoke `superpowers:writing-plans` skill, then dispatch `feature-dev:code-architect` + ECC `architect` agents
- "should we even", "is this worth", "scope", "challenge this", "do we need" → invoke `superpowers:brainstorming` skill, dispatch ECC `planner` agent
- "what could go wrong", "devil's advocate", "risks", "what if this breaks" → dispatch `pr-review-toolkit:silent-failure-hunter` + ECC `security-reviewer` agents in parallel

### Code Review & Quality
- "review", "look over", "check this", "is this good" → dispatch in parallel: `pr-review-toolkit:code-reviewer`, `pr-review-toolkit:silent-failure-hunter`, `pr-review-toolkit:comment-analyzer`, ECC `code-reviewer`
- "review the PR", "PR review", "check the pull request" → invoke `pr-review-toolkit:review-pr` skill (runs 6 parallel agents)
- "security", "vulnerabilities", "audit", "is this secure" → dispatch ECC `security-reviewer` + `pr-review-toolkit:silent-failure-hunter` agents in parallel
- "test coverage", "are tests enough", "missing tests" → dispatch `pr-review-toolkit:pr-test-analyzer` agent
- "types", "type design", "type safety" → dispatch `pr-review-toolkit:type-design-analyzer` agent
- "database", "queries", "schema", "migration" → dispatch ECC `database-reviewer` agent

### Building & Fixing
- "build is broken", "build errors", "won't compile", "fix the build" → dispatch ECC `build-error-resolver` agent (or language-specific: `cpp-build-resolver`, `go-build-resolver`, `java-build-resolver`, `rust-build-resolver`)
- "TDD", "test first", "write tests then code" → invoke `superpowers:test-driven-development` skill, dispatch ECC `tdd-guide` agent
- "bug", "broken", "not working", "failing" → invoke `superpowers:systematic-debugging` skill
- "refactor", "clean up", "dead code", "unused" → dispatch `code-simplifier:code-simplifier` + ECC `refactor-cleaner` agents
- "e2e", "end to end", "integration test" → dispatch ECC `e2e-runner` agent

### Shipping
- "commit", "push", "PR", "ship it", "merge" → invoke `superpowers:verification-before-completion` skill first, then commit
- "verify", "check everything", "ready to ship?" → run build → types → lint → tests → console audit in sequence

### Design & Frontend
- "design system", "colors", "typography", "visual style" → invoke `frontend-design:frontend-design` skill
- "looks wrong", "visual bug", "design review", "UI review" → use Playwright for screenshots, check against DESIGN.md
- "QA", "test the site", "check the pages", "browser test" → use Playwright for systematic page-by-page testing

### Understanding & Exploring
- "explain", "how does this work", "walk me through" → dispatch `feature-dev:code-explorer` agent
- "find", "where is", "search for" → dispatch Explore agent
- "docs", "update documentation" → dispatch ECC `doc-updater` agent

### Research & Experimentation
- "experiment", "try different approaches", "optimize", "iterate", "research" → use experiment loop: modify → run → measure → keep/discard → repeat. Track results in a table. Always establish a baseline first.
- "benchmark", "compare approaches", "which is faster" → run each variant, measure, record in results table, keep the winner

### Session Management
- "what did we learn", "capture this", "remember this" → extract patterns into CLAUDE.md or memory system
- "side question", "quick question", "unrelated but" → pause main task, answer briefly, resume with context summary
- "checkpoint", "save progress", "snapshot" → commit current state with checkpoint prefix

### Language-Specific Review
ECC provides language-specific reviewers that activate automatically based on file types:
- Python files → ECC `python-reviewer`
- Go files → ECC `go-reviewer`
- Rust files → ECC `rust-reviewer`
- C++ files → ECC `cpp-reviewer`
- Java files → ECC `java-reviewer`
- Kotlin files → ECC `kotlin-reviewer`

## What This Project Is For
This is a living reference document. When you want to:
- **Check what commands exist**: Read README.md "Commands Reference"
- **Understand what's automatic**: Read README.md "What's Automatic vs Manual"
- **Add a new command**: Create a .md file in `~/.claude/commands/`, document it here
- **Add a new hook**: Edit `~/.claude/hooks/hooks.json`, document it here
- **Change plugin config**: Edit `~/.claude/settings.json`

## Recent Changes
- 2026-03-18: merged gstack + everything-claude-code + autoresearch patterns — 12 new commands, enhanced 4 existing, 2 new hooks, ECC agents wired into routing table, playwright + ECC plugins enabled
- 2026-03-15: Added commit/documentation conventions, custom `/commit` and `/commit-push-pr` commands, Co-Authored-By blocking hook
- 2026-03-08: Initial setup - 10 commands, 2 hooks, 10 plugins enabled

## TODO
- Consider adding: pre-commit hook that requires tests
- Consider adding: file-outside-project warning hook

## Gotchas
- Hooks exit code 2 = block execution, exit code 0 = warn and continue
- Plugin changes require `/reload-plugins` to take effect
- Commands are immediately available after creating the .md file (no reload needed)
- CLAUDE.md at project root is auto-read; the template at `~/.claude/` is not
