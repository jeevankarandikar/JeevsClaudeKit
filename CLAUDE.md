# CLAUDE.md

## Project Context
- **Name**: JeevsClaudeKit
- **Purpose**: Personal Claude Code toolkit reference and configuration hub
- **Stack**: Markdown documentation, JSON config, shell scripts
- **Location**: ~/Documents/JeevsClaudeKit

## Key Paths
- **Commands**: `~/.claude/commands/*.md`
- **Hooks**: `~/.claude/hooks/hooks.json`
- **Settings**: `~/.claude/settings.json`
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

## What This Project Is For
This is a living reference document. When you want to:
- **Check what commands exist**: Read README.md "Commands Reference"
- **Understand what's automatic**: Read README.md "What's Automatic vs Manual"
- **Add a new command**: Create a .md file in `~/.claude/commands/`, document it here
- **Add a new hook**: Edit `~/.claude/hooks/hooks.json`, document it here
- **Change plugin config**: Edit `~/.claude/settings.json`

## Recent Changes
- 2026-03-15: Added commit/documentation conventions, custom `/commit` and `/commit-push-pr` commands, Co-Authored-By blocking hook
- 2026-03-08: Initial setup - 10 commands, 2 hooks, 10 plugins enabled

## TODO
- Consider adding: pre-commit hook that requires tests
- Consider adding: file-outside-project warning hook
- Evaluate ruflo if multi-agent orchestration is needed
- Try Anthropic skills marketplace: `/plugin marketplace add anthropics/skills`
- Explore awesome-claude-code tools for additional productivity

## Gotchas
- Hooks exit code 2 = block execution, exit code 0 = warn and continue
- Plugin changes require `/reload-plugins` to take effect
- Commands are immediately available after creating the .md file (no reload needed)
- CLAUDE.md at project root is auto-read; the template at `~/.claude/` is not
