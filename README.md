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
   - enable these plugins (set to true): superpowers, context7, typescript-lsp, security-guidance, claude-md-management, code-simplifier, claude-code-setup, frontend-design, feature-dev, commit-commands, hookify, github, pr-review-toolkit, code-review, plugin-dev (all @claude-plugins-official)
   - set these to false: playwright, serena, supabase, greptile, ralph-loop

6. install all the plugins:
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

7. clean up:
   rm -rf /tmp/JeevsClaudeKit

8. tell me what was installed and flag any errors.
```

once that's done, open any project and run `/init-project` -- it'll scan your codebase and generate a CLAUDE.md with your stack, commands, conventions, everything Claude needs to be useful from the first prompt.

---

## what this gives you

### commands you can use anywhere

these are the slash commands I use daily. they enforce structure so Claude doesn't just wing it.

| command | what it does |
| ------- | ------------ |
| `/tdd [feature]` | strict test-driven development -- tests first, implementation second, no cutting corners |
| `/plan-feature [desc]` | research the codebase before writing anything, present a plan, wait for approval |
| `/debug [issue]` | systematic root cause analysis instead of guessing and hoping |
| `/review [code/PR]` | 6-dimension review -- quality, correctness, tests, security, perf, docs |
| `/perf [code]` | performance deep-dive -- Big O, N+1 queries, memory leaks, the works |
| `/commit` | commit with my style enforced -- lowercase, no emoji, no prefixes, no trailers |
| `/commit-push-pr` | same conventions but also pushes and opens a PR |
| `/init-project` | scans your project and generates a CLAUDE.md so Claude actually knows what it's working with |
| `/progressive-build [feat]` | builds features in 3 committed phases with approval gates between each |
| `/devils-advocate [change]` | pre-deploy risk analysis -- edge cases, race conditions, rollback plan |
| `/explain [area]` | walkthrough of unfamiliar code like you're onboarding a new teammate |
| `/fast [task]` | efficiency mode for routine stuff -- minimal tokens, one-shot, no over-thinking |
| `/update-memory` | captures what you learned this session into CLAUDE.md for next time |

### hooks that run automatically

these sit in the background and catch problems before they happen. no action needed on your part.

- **destructive command blocker** -- intercepts `rm -rf`, `git reset --hard`, `git push --force`, `DROP TABLE`, and other commands that can ruin your day. blocks execution until you explicitly confirm.
- **sensitive file warning** -- warns when Claude tries to edit files with `.env`, credentials, secrets, api keys. doesn't block, just makes sure you're paying attention.
- **co-authored-by blocker** -- Claude's system prompt tries to add `Co-Authored-By` trailers to every commit. this hook kills that. also blocks `Signed-off-by`.

### plugins

15 plugins enabled out of the box. the important ones:

- **superpowers** -- the backbone. brainstorming, debugging workflows, code review, TDD, verification before claiming something is done.
- **context7** -- when you mention a library, it pulls the actual current docs instead of hallucinating from training data.
- **typescript-lsp** -- real-time type errors and missing imports. catches stuff before you even run the code.
- **feature-dev** -- 7-phase feature workflow with parallel architect agents when you need to build something serious.
- **github** -- native access to PRs, issues, repos through MCP. makes `/commit-push-pr` actually work well.
- **pr-review-toolkit** -- 6 parallel review agents for deep PR review.
- **code-review** -- 5 parallel sonnet agents with confidence-based scoring.

also enabled: security-guidance, claude-md-management, code-simplifier, claude-code-setup, frontend-design, commit-commands, hookify, plugin-dev.

**available but off by default**: playwright (E2E testing), serena (semantic code analysis), supabase, greptile (external PR review), ralph-loop (autonomous loops). flip them on in `~/.claude/settings.json` when you need them.

### conventions

these are baked into CLAUDE.md, the custom commands, and the hooks -- so they're enforced at every layer:

- **commits** -- lowercase, concise, no emoji, no conventional commit prefixes (`feat:`, `fix:`, etc.), no `Co-Authored-By` trailers, one logical change per commit
- **code comments** -- explain why, not what. google-style docstrings in python, minimal in js/ts/swift
- **documentation** -- CLAUDE.md is the single source of truth. don't create random .md files

---

## how I actually use this day-to-day

```bash
# first time in any project
/init-project

# building something
/plan-feature user authentication system
# review the plan, approve it
/tdd login flow
# tests get written first, then implementation
/review
/commit-push-pr

# hit a bug
/debug users can't reset passwords after 24 hours
# systematic analysis, not guessing

# end of session
/update-memory
```

the key insight is the CLAUDE.md learning loop -- `/init-project` creates it, Claude reads it every session, `/update-memory` keeps it current. next time you open Claude in that project, it already knows your stack, your conventions, your recent changes, your known issues. no re-explaining.

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
