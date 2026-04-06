# JeevsClaudeKit

my personal Claude Code setup. 8 commands, 5 hooks, 17 plugins, and conventions that make Claude actually useful for real development work. consolidated from 19 commands down to 8 - each one is smarter and handles multiple modes instead of being a thin wrapper.

this is a living setup — I update it as I find new patterns that work.

---

## setup

paste this entire block into Claude Code. that's it.

```
set up my Claude Code environment using JeevsClaudeKit. follow these steps exactly:

1. clone the repo:
   git clone https://github.com/jeevankarandikar/JeevsClaudeKit.git /tmp/JeevsClaudeKit

2. copy commands to ~/.claude/commands/ (creates the directory if needed):
   mkdir -p ~/.claude/commands
   cp /tmp/JeevsClaudeKit/commands/*.md ~/.claude/commands/

3. copy hooks to ~/.claude/hooks/ (creates the directory if needed):
   mkdir -p ~/.claude/hooks
   cp /tmp/JeevsClaudeKit/hooks/hooks.json ~/.claude/hooks/hooks.json

4. copy the CLAUDE.md template:
   cp /tmp/JeevsClaudeKit/CLAUDE.md-template ~/.claude/CLAUDE.md-template

5. merge settings into ~/.claude/settings.json -- read my current file first, then merge these values WITHOUT overwriting my existing permissions.allow entries:
   - set defaultMode to "plan"
   - set effortLevel to "high"
   - enable these plugins (set to true): superpowers, context7, typescript-lsp, security-guidance, claude-md-management, code-simplifier, claude-code-setup, frontend-design, feature-dev, commit-commands, hookify, github, pr-review-toolkit, code-review, plugin-dev, playwright (all @claude-plugins-official), everything-claude-code (@everything-claude-code)
   - merge the extraKnownMarketplaces block so the ECC marketplace (affaan-m/everything-claude-code) is registered
   - set these to false: serena, supabase, greptile, ralph-loop

6. install all plugins (official + everything-claude-code):
   claude plugin install superpowers@claude-plugins-official
   claude plugin install context7@claude-plugins-official
   claude plugin install typescript-lsp@claude-plugins-official
   claude plugin install security-guidance@claude-plugins-official
   claude plugin install claude-md-management@claude-plugins-official
   claude plugin install code-simplifier@claude-plugins-official
   claude plugin install claude-code-setup@claude-plugins-official
   claude plugin install frontend-design@claude-plugins-official
   claude plugin install feature-dev@claude-plugins-official
   claude plugin install commit-commands@claude-plugins-official
   claude plugin install hookify@claude-plugins-official
   claude plugin install github@claude-plugins-official
   claude plugin install pr-review-toolkit@claude-plugins-official
   claude plugin install code-review@claude-plugins-official
   claude plugin install plugin-dev@claude-plugins-official
   claude plugin install playwright@claude-plugins-official
   claude plugin marketplace add affaan-m/everything-claude-code
   claude plugin install everything-claude-code@everything-claude-code

7. clean up:
   rm -rf /tmp/JeevsClaudeKit

8. tell me what was installed and flag any errors.
```

### updating an existing installation

```
update my Claude Code environment from JeevsClaudeKit. follow these steps exactly:

1. clone the latest version:
   git clone https://github.com/jeevankarandikar/JeevsClaudeKit.git /tmp/JeevsClaudeKit

2. remove old commands and copy new ones (handles renames and deletions):
   rm ~/.claude/commands/*.md
   cp /tmp/JeevsClaudeKit/commands/*.md ~/.claude/commands/

3. update hooks:
   cp /tmp/JeevsClaudeKit/hooks/hooks.json ~/.claude/hooks/hooks.json

4. update the CLAUDE.md template:
   cp /tmp/JeevsClaudeKit/CLAUDE.md-template ~/.claude/CLAUDE.md-template

5. merge new settings into ~/.claude/settings.json -- read my current file first, then ONLY add new plugin entries. do NOT overwrite my existing permissions.allow entries or change plugins I've manually toggled. if the ECC marketplace isn't registered locally, also run:
   claude plugin marketplace add affaan-m/everything-claude-code
   claude plugin install everything-claude-code@everything-claude-code

6. clean up:
   rm -rf /tmp/JeevsClaudeKit

7. tell me what changed since my last install.
```

### setting up a new project

open any project directory and run `/save` — if no CLAUDE.md exists, it will init one by scanning your codebase, then capture your session learnings on top.

---

## what this gives you

### 8 commands

| command | what it does |
| ------- | ------------ |
| `/plan [desc]` | scope challenge (EXPAND/HOLD/REDUCE) → research → design with error maps and ASCII diagrams → risk assessment → present plan → wait for approval |
| `/build [feature]` | auto-detects mode: build errors → fix one at a time; new feature → TDD (tests first); otherwise → phased build (core → errors → polish) |
| `/ship` | smart shipping: no args = commit only; "pr" = verify + commit + push + PR; "verify" = check only. all modes enforce lowercase/no-trailer conventions |
| `/clean [target]` | full cleanup: dead code + repo organization + file consolidation + reference updates. not just dead code removal |
| `/debug [issue]` | systematic 5-step root cause analysis: reproduce → gather context → hypothesize → fix → prevent |
| `/qa [target]` | auto-detects platform: iOS project → xcode build + code-level QA; web project → playwright browser testing with health scoring |
| `/review [timeframe]` | retrospective from git history (default); or `experiment` mode for autonomous modify → measure → decide loops |
| `/save` | all-in-one session end: updates CLAUDE.md (or inits if missing) + writes journal entry + saves personal learnings to memory |

### what got consolidated

| old (19) | new (8) |
|----------|---------|
| plan + challenge | `/plan` — scope challenge is now phase 0 of planning |
| tdd + build-phases + fix-build | `/build` — auto-detects which mode you need |
| commit + ship + verify + checkpoint | `/ship` — one command, three modes |
| cleanup | `/clean` — expanded with repo organization + consolidation |
| debug | `/debug` — unchanged, was already solid |
| qa | `/qa` — added iOS mode alongside browser mode |
| retro + experiment | `/review` — two modes in one |
| save + journal + init | `/save` — does all three in one pass |
| aside, explain | dropped — just ask the question directly |

### hooks that run automatically

- **destructive command blocker** — intercepts `rm -rf`, `git reset --hard`, `git push --force`, `DROP TABLE`. blocks until confirmed.
- **sensitive file warning** — warns on edits to `.env`, credentials, secrets, api keys.
- **co-authored-by blocker** — kills `Co-Authored-By` and `Signed-off-by` trailers.
- **session end reminder** — reminds to run `/save` when Claude stops.
- **debug statement warning** — flags `console.log`, `debugger`, `print(`, `NSLog(` in edits.

### plugins

16 official + 1 community plugin. the important ones:

- **superpowers** — brainstorming, debugging, TDD, verification workflows
- **context7** — pulls current docs instead of hallucinating from training data
- **feature-dev** — 7-phase feature workflow with parallel architect agents
- **pr-review-toolkit** — 6 parallel review agents for deep PR review
- **playwright** — browser automation for `/qa`
- **everything-claude-code** — 25 specialized agents, 108 skills

### conventions

baked into commands, hooks, and CLAUDE.md:

- **commits** — lowercase, concise, no emoji, no prefixes, no trailers, one change per commit
- **code comments** — explain why, not what. minimal in swift
- **documentation** — CLAUDE.md is single source of truth
- **error handling** — name specific exceptions, every rescue must retry/degrade/re-raise

---

## cheat sheet

```
/plan [desc]          plan + scope challenge + risk assessment
/build [feature]      build (auto: fix / tdd / phased)
/ship                 commit only (default)
/ship pr              verify + commit + push + PR
/ship verify          check everything, no changes
/clean [target]       dead code + repo org + consolidation
/debug [issue]        systematic root cause analysis
/qa [target]          iOS or browser QA (auto-detected)
/review [timeframe]   git retrospective (default 7d)
/review experiment    modify → measure → decide loop
/save                 update CLAUDE.md + journal + memory
```

---

## how I actually use this day-to-day

```bash
# first time in any project
/save
# (detects no CLAUDE.md, inits one, then captures learnings)

# building something
/plan user authentication system
# pick HOLD scope, review plan, approve
/build tdd login flow
# tests first, then implementation
/ship verify
/ship pr

# hit a bug
/debug users can't reset passwords after 24 hours

# build broke
/build
# (auto-detects errors, fixes one at a time)

# cleanup day
/clean
# dead code + repo org + consolidation

# QA
/qa

# end of session
/save

# weekly check-in
/review 7d
```

---

## sources

patterns from:
- **[gstack](https://github.com/garrytan/gstack)** — review, ship, QA, retro workflows
- **[everything-claude-code](https://github.com/affaan-m/everything-claude-code)** — build-fix, verify, refactor, 25 agents, 108 skills
- **[autoresearch](https://github.com/karpathy/autoresearch)** — autonomous experiment loop pattern

---

## repo structure

```
JeevsClaudeKit/
  commands/              # 8 slash commands -> ~/.claude/commands/
    build.md
    clean.md
    debug.md
    plan.md
    qa.md
    review.md
    save.md
    ship.md
  hooks/
    hooks.json           # 5 native hooks -> ~/.claude/hooks/
  settings.json          # plugin config (16 official + ECC) -> merge into ~/.claude/settings.json
  CLAUDE.md-template     # project template -> ~/.claude/CLAUDE.md-template
  CLAUDE.md              # this project's own config
```

---

## making it your own

**add a command**: create a `.md` file in `~/.claude/commands/` with `$ARGUMENTS` as a placeholder. immediately available, no reload.

**add a hook**: edit `~/.claude/hooks/hooks.json`. exit code 0 = warn, exit code 2 = block.

**enable a plugin**: set to `true` in `~/.claude/settings.json`, then `/reload-plugins`.
