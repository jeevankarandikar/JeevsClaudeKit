# JeevsClaudeKit

my personal Claude Code setup. commands, hooks, plugins, and conventions I've built up that make Claude actually useful for real development work. I got tired of Claude adding emoji to commits, writing vague messages, and guessing instead of being systematic -- so I built a toolkit that enforces the habits I want.

this is a living setup -- I update it as I find new patterns that work. if you're reading this, you can set up the exact same environment in about 2 minutes.

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
   - enable these plugins (set to true): superpowers, context7, typescript-lsp, security-guidance, claude-md-management, code-simplifier, claude-code-setup, frontend-design, feature-dev, commit-commands, hookify, github, pr-review-toolkit, code-review, plugin-dev, playwright (all @claude-plugins-official)
   - set these to false: serena, supabase, greptile, ralph-loop

6. install official marketplace plugins:
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

7. install everything-claude-code (community plugin with 25 agents):
   claude plugin marketplace add affaan-m/everything-claude-code
   claude plugin install everything-claude-code@everything-claude-code

8. clean up:
   rm -rf /tmp/JeevsClaudeKit

9. tell me what was installed and flag any errors.
```

### updating an existing installation

if you already have the kit installed and want to pull the latest commands, hooks, and settings:

```
update my Claude Code environment from JeevsClaudeKit. follow these steps exactly:

1. clone the latest version:
   git clone https://github.com/jeevankarandikar/JeevsClaudeKit.git /tmp/JeevsClaudeKit

2. update commands (overwrites old versions, adds new ones):
   cp /tmp/JeevsClaudeKit/commands/*.md ~/.claude/commands/

3. update hooks:
   cp /tmp/JeevsClaudeKit/hooks/hooks.json ~/.claude/hooks/hooks.json

4. update the CLAUDE.md template:
   cp /tmp/JeevsClaudeKit/CLAUDE.md-template ~/.claude/CLAUDE.md-template

5. merge new settings into ~/.claude/settings.json -- read my current file first, then ONLY add new plugin entries. do NOT overwrite my existing permissions.allow entries or change plugins I've manually toggled.

6. install any new plugins that aren't already installed:
   claude plugin install playwright@claude-plugins-official
   claude plugin marketplace add affaan-m/everything-claude-code
   claude plugin install everything-claude-code@everything-claude-code

7. clean up:
   rm -rf /tmp/JeevsClaudeKit

8. tell me what changed since my last install.
```

### setting up a new project

open any project directory and run `/init-project` -- it scans your codebase and generates a CLAUDE.md with your stack, commands, conventions, everything Claude needs to be useful from the first prompt.

### setting up an existing project (already has CLAUDE.md)

if the project already has a CLAUDE.md, `/init-project` will detect it and offer to update rather than overwrite. alternatively, you can manually add sections from the template at `~/.claude/CLAUDE.md-template`.

---

## what this gives you

### commands you can use anywhere

25 slash commands organized by workflow phase.

#### planning & scoping

| command | what it does |
| ------- | ------------ |
| `/plan-feature [desc]` | scope challenge → research → design with error maps and ASCII diagrams → present plan → wait for approval |
| `/scope-challenge [idea]` | CEO/founder-mode: challenge the premise, map dream state, choose EXPAND/HOLD/REDUCE scope |
| `/devils-advocate [change]` | premise challenge + risk analysis + failure modes registry + temporal/deployment risk |

#### building & fixing

| command | what it does |
| ------- | ------------ |
| `/tdd [feature]` | strict test-driven development -- tests first, implementation second, no cutting corners |
| `/progressive-build [feat]` | builds features in 3 committed phases with approval gates between each |
| `/build-fix [target]` | incrementally fix build errors one at a time, re-verify after each fix |

#### reviewing & QA

| command | what it does |
| ------- | ------------ |
| `/review [code/PR]` | two-pass review: critical (must-fix) + informational, with error & rescue maps |
| `/design-review [target]` | visual QA with AI slop detection, typography/spacing/interaction checks |
| `/qa [target]` | systematic browser-based QA using Playwright -- health score, issue tracking |
| `/perf [code]` | performance deep-dive -- Big O, N+1 queries, memory leaks, the works |

#### shipping

| command | what it does |
| ------- | ------------ |
| `/commit` | commit with my style enforced -- lowercase, no emoji, no prefixes, no trailers |
| `/commit-push-pr` | pre-flight checks + commit + pre-landing scan + push + PR |
| `/verify` | run build → types → lint → tests → console audit → git status in sequence |

#### design

| command | what it does |
| ------- | ------------ |
| `/design-system [project]` | guided design system creation → produces DESIGN.md with all visual decisions |

#### understanding & debugging

| command | what it does |
| ------- | ------------ |
| `/debug [issue]` | systematic root cause analysis instead of guessing and hoping |
| `/explain [area]` | walkthrough of unfamiliar code like you're onboarding a new teammate |

#### refactoring & cleanup

| command | what it does |
| ------- | ------------ |
| `/refactor-clean [target]` | find and safely remove dead code -- unused imports, functions, variables, commented-out blocks |

#### workflow management

| command | what it does |
| ------- | ------------ |
| `/aside [question]` | answer a side question without losing context on the main task |
| `/checkpoint [name]` | snapshot current work state with context about what's done and what's left |
| `/retro [timeframe]` | engineering retrospective from git history -- metrics, sessions, hotspots, habits |
| `/research [target]` | autonomous experiment loop -- modify, run, measure, keep/discard, repeat until optimized |
| `/fast [task]` | efficiency mode for routine stuff -- minimal tokens, one-shot, no over-thinking |

#### session management

| command | what it does |
| ------- | ------------ |
| `/init-project` | scans your project and generates a CLAUDE.md so Claude actually knows what it's working with |
| `/update-memory` | captures what you learned this session into CLAUDE.md for next time |
| `/learn` | extract reusable patterns (errors, conventions, workarounds) from this session into CLAUDE.md or memory |

### hooks that run automatically

these sit in the background and catch problems before they happen. no action needed on your part.

- **destructive command blocker** -- intercepts `rm -rf`, `git reset --hard`, `git push --force`, `DROP TABLE`, and other commands that can ruin your day. blocks execution until you explicitly confirm.
- **sensitive file warning** -- warns when Claude tries to edit files with `.env`, credentials, secrets, api keys. doesn't block, just makes sure you're paying attention.
- **co-authored-by blocker** -- Claude's system prompt tries to add `Co-Authored-By` trailers to every commit. this hook kills that. also blocks `Signed-off-by`.
- **session end reminder** -- when Claude stops, reminds you to run `/update-memory` or `/learn` to capture session insights.
- **debug statement warning** -- warns when an edit introduces `console.log`, `debugger`, `binding.pry`, or `print(` statements. doesn't block, just flags for removal before committing.

### plugins

16 official plugins + 1 community plugin enabled out of the box. the important ones:

- **superpowers** -- the backbone. brainstorming, debugging workflows, code review, TDD, verification before claiming something is done.
- **context7** -- when you mention a library, it pulls the actual current docs instead of hallucinating from training data.
- **typescript-lsp** -- real-time type errors and missing imports. catches stuff before you even run the code.
- **feature-dev** -- 7-phase feature workflow with parallel architect agents when you need to build something serious.
- **github** -- native access to PRs, issues, repos through MCP. makes `/commit-push-pr` actually work well.
- **pr-review-toolkit** -- 6 parallel review agents for deep PR review.
- **code-review** -- 5 parallel sonnet agents with confidence-based scoring.
- **playwright** -- browser automation for `/qa` and `/design-review` commands.
- **everything-claude-code** -- 25 specialized agents (architect, security-reviewer, database-reviewer, build-error-resolver, e2e-runner, refactor-cleaner, planner, tdd-guide, doc-updater, plus language-specific reviewers for python/go/rust/c++/java/kotlin), 108 skills, hooks infrastructure. installed as a community plugin via its own marketplace.

also enabled: security-guidance, claude-md-management, code-simplifier, claude-code-setup, frontend-design, commit-commands, hookify, plugin-dev.

**available but off by default**: serena (semantic code analysis), supabase, greptile (external PR review), ralph-loop (autonomous loops). flip them on in `~/.claude/settings.json` when you need them.

### conventions

these are baked into CLAUDE.md, the custom commands, and the hooks -- so they're enforced at every layer:

- **commits** -- lowercase, concise, no emoji, no conventional commit prefixes (`feat:`, `fix:`, etc.), no `Co-Authored-By` trailers, one logical change per commit
- **code comments** -- explain why, not what. google-style docstrings in python, minimal in js/ts/swift
- **documentation** -- CLAUDE.md is the single source of truth. don't create random .md files
- **diagrams** -- ASCII diagrams for non-trivial data flows, placed near the code they describe
- **error handling** -- name specific exceptions, never catch generic "Error", every rescue must retry/degrade/re-raise

---

## how I actually use this day-to-day

```bash
# first time in any project
/init-project

# building something
/scope-challenge user authentication system
# pick HOLD scope
/plan-feature user authentication system
# review the plan, approve it
/tdd login flow
# tests get written first, then implementation
/review
/verify
/commit-push-pr

# hit a bug
/debug users can't reset passwords after 24 hours
# systematic analysis, not guessing

# build broke
/build-fix

# quick detour
/aside what's the difference between bcrypt and argon2?

# frontend work
/design-system
# later...
/design-review

# QA before shipping
/qa standard

# end of session
/learn
/update-memory

# weekly check-in
/retro 7d
```

the key insight is the CLAUDE.md learning loop -- `/init-project` creates it, Claude reads it every session, `/update-memory` and `/learn` keep it current. next time you open Claude in that project, it already knows your stack, your conventions, your recent changes, your known issues. no re-explaining.

---

## sources

this toolkit merges patterns from:
- **[gstack](https://github.com/garrytan/gstack)** — CEO review, eng review, code review, ship, QA, retro, design consultation, design review workflows
- **[everything-claude-code](https://github.com/affaan-m/everything-claude-code)** — build-fix, learn, verify, refactor-clean, aside, checkpoint, 25 specialized agents, 108 skills (also installed as a plugin for direct agent access)
- **[autoresearch](https://github.com/karpathy/autoresearch)** — autonomous experiment loop pattern: modify, run, measure, keep/discard, repeat

---

## repo structure

```
JeevsClaudeKit/
  commands/              # slash commands -> ~/.claude/commands/
    tdd.md
    plan-feature.md
    debug.md
    review.md
    perf.md
    commit.md
    commit-push-pr.md
    init-project.md
    progressive-build.md
    devils-advocate.md
    explain.md
    fast.md
    update-memory.md
    scope-challenge.md
    retro.md
    qa.md
    design-system.md
    design-review.md
    build-fix.md
    learn.md
    verify.md
    refactor-clean.md
    aside.md
    checkpoint.md
    research.md
  hooks/
    hooks.json           # native hooks -> ~/.claude/hooks/
  settings.json          # plugin config -> merge into ~/.claude/settings.json
  CLAUDE.md-template     # project template -> ~/.claude/CLAUDE.md-template
  CLAUDE.md              # this project's own config
```

---

## making it your own

**add a command**: create a `.md` file in `~/.claude/commands/` with `$ARGUMENTS` as a placeholder. it's immediately available as a slash command, no reload needed.

**add a hook**: edit `~/.claude/hooks/hooks.json`. exit code 0 = warn and continue, exit code 2 = block execution.

**enable a plugin**: set it to `true` in `~/.claude/settings.json` under `enabledPlugins`, then `/reload-plugins`.

**change modes**: `defaultMode` in settings -- `"plan"` thinks before acting, `"normal"` acts immediately. `effortLevel` -- `"high"` for deep reasoning, `"medium"` for daily work, `"low"` for quick tasks.
