# CLAUDE.md

## Project Context
- **Name**: JeevsClaudeKit
- **Purpose**: Personal Claude Code toolkit — 8 commands, 5 hooks, 17 plugins
- **Stack**: Markdown documentation, JSON config, shell scripts

## Key Paths
- **Commands**: `~/.claude/commands/*.md` (8 commands)
- **Hooks**: `~/.claude/hooks/hooks.json` (5 hooks)
- **Settings**: `~/.claude/settings.json` (16 official plugins + ECC via community marketplace)
- **Template**: `~/.claude/CLAUDE.md-template`

## Commands (8)
| command | modes |
|---------|-------|
| `/plan` | scope challenge → research → design → risk → present |
| `/build` | auto-detect: fix-build / TDD / phased build |
| `/ship` | auto-detect from CLAUDE.md / commit / push / pr / verify |
| `/clean` | dead code + repo org + consolidation + reference updates |
| `/debug` | 5-step root cause analysis |
| `/qa` | auto-detect: iOS (xcode) / browser (playwright) |
| `/review` | retrospective (default) / experiment loop |
| `/save` | append-only: changelog.md + journal.md + CLAUDE.md current-state |

## Conventions

### Commits
- lowercase only, no capital letters anywhere
- concise: one short sentence, under 72 characters
- no emoji, no conventional commit prefixes
- no trailers: never Co-Authored-By, Signed-off-by
- granular: one logical change per commit

### READMEs
- lowercase headers preferred
- technical and direct, no marketing language
- no emoji

### Code Comments
- explain why, not what
- minimal in swift, let types and naming do the work
- never add comments to code you didn't change

## Recent Changes
- 2026-04-24: CLAUDE.md-template gained "Working Principles" section (folds Karpathy's Think → Simplicity → Surgical → Goal-Driven into project-local sharpening of SOUL), optional "Strategic Shift" placeholder block at top (for use when major repositioning happens), and References footer pointing to SOUL + per-project MEMORY + Karpathy skills repo. Surfaced from PinPal session 2026-04-24 where the team got beat to market by a competitor and needed to consolidate the strategic shift into the project CLAUDE.md.
- 2026-04-13: audited kit against real pinpal workflow. /save rewritten as token-efficient three-doc append (changelog.md + journal.md + CLAUDE.md current-state). /ship gained push mode + auto-detect from CLAUDE.md worktree section. /plan made subagent dispatch opt-in for large changes only. /build and /qa now run xcodegen before xcodebuild when ios/project.yml exists and know `cd website && npx next build` for next.js. CLAUDE.md-template gained docs-conventions and worktree-model sections.
- 2026-04-01: consolidated 19 commands → 8 smart multi-mode commands. added iOS/xcode support to /qa and /build. expanded /clean with repo organization. merged /save + /journal + /init. updated README with new cheat sheet and consolidation table.
- 2026-03-20: slimmed commands from 25 to 19
- 2026-03-18: merged gstack + everything-claude-code + autoresearch patterns
- 2026-03-15: initial commit conventions, Co-Authored-By blocking hook
- 2026-03-08: initial setup

## Gotchas
- Hooks exit code 2 = block execution, exit code 0 = warn and continue
- Plugin changes require `/reload-plugins` to take effect
- Commands are immediately available after creating the .md file (no reload needed)
- CLAUDE.md at project root is auto-read; the template at `~/.claude/` is not
