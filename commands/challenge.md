Challenge scope, risks, and assumptions for: $ARGUMENTS

## Agents & Skills
- Invoke `superpowers:brainstorming` skill to explore the problem space before committing to a direction
- Dispatch `feature-dev:code-explorer` agent to find existing code that already solves parts of the problem
- Dispatch these risk agents in parallel:
  - `pr-review-toolkit:silent-failure-hunter` — error handling gaps, silent failures, fallback abuse
  - `pr-review-toolkit:code-reviewer` — code quality issues that could become bugs
  - `pr-review-toolkit:pr-test-analyzer` — missing test coverage for failure paths
Synthesize agent findings into the risk assessment below.

Before any work begins, think like a founder deciding where to invest limited resources — and then think like a pessimist finding everything that can go wrong.

## Phase 1: Premise & Scope

1. Is this the right problem? Could a different framing yield a simpler or more impactful solution?
2. What happens if we do nothing? Real pain point or hypothetical?
3. Who benefits most from this? Users? Developers? The codebase?
4. What existing code already partially or fully solves each sub-problem?
5. Is there a 3rd-party tool, library, or service that handles this better than building it?

### Existing Code Leverage Check
Search the codebase for:
- Functions, modules, or patterns that overlap with the proposed work
- Prior attempts at solving similar problems (check git log)
- Utilities that could be composed instead of building from scratch

### Dream State Mapping
CURRENT STATE → THIS PLAN → 12-MONTH IDEAL
- Does this move toward the ideal, or is it a detour?
- What would need to change later to reach the ideal?
- Are we building something we'll want to tear down?

### Scope Options
Present three options with effort, risk, and what gets deferred:

**A) EXPAND** — push scope up. What's the 10x version for 2x effort?
**B) HOLD** — scope is right. Make the plan bulletproof. What's missing?
**C) REDUCE** — strip to minimum. What's the smallest thing that ships value?

For each option: estimated effort, risk level, what gets deferred, and what we learn.

## Phase 2: Risk Assessment

### What Could Go Wrong?
1. **Edge Cases**: What inputs/states did we miss? (null, empty, concurrent, huge, malformed)
2. **Under Load**: What happens with 10x, 100x, 1000x the expected traffic?
3. **Bad Assumptions**: What are we assuming that might not be true in production?
4. **External Failures**: What if the database is slow? API is down? Network is flaky?
5. **Bad Data**: What if upstream sends garbage? What if the schema changes?
6. **Security**: Could this be exploited? Injected? Abused?
7. **Race Conditions**: What if two users hit this simultaneously?
8. **Rollback**: If this breaks, can we safely revert? What's the blast radius?

### For Each Risk Found
- **Risk**: What could happen
- **Likelihood**: Low/Medium/High
- **Impact**: Low/Medium/High
- **Mitigation**: What to do about it

### Failure Modes Registry
For each new codepath:
CODEPATH | FAILURE MODE | RESCUED? | TEST? | USER SEES? | LOGGED?
Any row where RESCUED=N + TEST=N + USER SEES=Silent → CRITICAL GAP

## Phase 3: Temporal Analysis

### Implementation Timeline
- Hour 1 (foundations): what does the implementer need to know up front?
- Hour 2-3 (core logic): what ambiguities will they hit?
- Hour 4-5 (integration): what will surprise them?
- Hour 6+ (polish/tests): what will they wish they'd planned for?

### Outage Timeline
- Hour 1 of outage: what breaks first? blast radius?
- Hours 2-3: cascade effects?
- Day 1 post-deploy: what will users report?
- Week 1: what slow-burn issues surface?

Surface ambiguities NOW, not as "figure it out later."

## Phase 4: Deployment Risk
- Can this be safely reverted with `git revert`?
- Old code + new code running simultaneously during deploy — what breaks?
- Should any part be behind a feature flag?
- Post-deploy verification checklist: first 5 minutes, first hour

## STOP
Present all three scope options plus the full risk assessment. Wait for the user to select a scope and confirm before proceeding to any planning or implementation.
