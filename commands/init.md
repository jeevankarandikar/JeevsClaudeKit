Scan codebase and generate CLAUDE.md.

## Steps

1. **Analyze the project**: Read package.json, Cargo.toml, pyproject.toml, go.mod, or equivalent to identify the stack, dependencies, and tooling.

2. **Scan the codebase**: Look at the directory structure, key entry points, config files, and test setup to understand conventions.

3. **Create CLAUDE.md** at the project root with this structure:

```markdown
# CLAUDE.md

## Project Context
- **Name**: [project name]
- **Stack**: [detected languages, frameworks, databases]
- **Package Manager**: [npm/yarn/pnpm/cargo/pip/etc]
- **Build**: [build command]
- **Test**: [test command]
- **Lint**: [lint command]

## Architecture
- [Brief description of project structure]
- [Key directories and their purposes]
- [Entry points]

## Conventions

### Commits
- lowercase only, no capital letters anywhere
- concise: one short sentence, under 72 characters
- no emoji, no conventional commit prefixes (feat:, fix:, etc.)
- no trailers: never add Co-Authored-By, Signed-off-by, or any trailer lines
- granular: one logical change per commit

### Code Style
- [Code style: naming, formatting - detect from .editorconfig, .prettierrc, pylintrc, etc.]
- [Import ordering]
- [Error handling patterns]
- [Testing patterns]

### Comments & Documentation
- explain why, not what
- CLAUDE.md is the single source of truth for project context
- do not create unnecessary .md files

## Key Commands
- `[build command]` - Build the project
- `[test command]` - Run tests
- `[lint command]` - Run linter
- `[dev command]` - Start dev server

## Recent Changes
- [Will be updated as work progresses]

## Known Issues
- [Will be updated as issues are discovered]

## TODO
- [Will be updated as tasks are identified]

## Gotchas
- [Non-obvious things that have caused bugs or confusion]
```

4. **Create .claude/ directory** if it doesn't exist, for project-specific commands.

5. **Report**: Show what was created and detected.

Rules:
- Only include information you can verify from the codebase
- Don't guess at conventions - read the actual config files
- Keep it concise but complete
