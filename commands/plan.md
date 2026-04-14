Plan, scope-challenge, and design for: $ARGUMENTS

## When to escalate to subagents

By default, run the five phases below inline — Claude Code's plan mode already covers the same ground that feature-dev agents would, and dispatching them on small tasks wastes tokens.

**Only escalate when the change is large:**
- touches more than 5 files, OR
- introduces a new subsystem / module, OR
- integration with existing code is unclear after a first read

If any of those apply, dispatch in parallel:
- `feature-dev:code-explorer` to map existing patterns and reusable code
- `feature-dev:code-architect` to propose architecture
- load `superpowers:brainstorming` during Phase 0 and `superpowers:writing-plans` during Phase 2

For small and medium plans, skip all of the above and just run the phases.

Before writing ANY code, follow this sequence:

## Phase 0: Scope & Premise Challenge

1. Is this the right problem? Could a different framing yield a simpler or more impactful solution?
2. What happens if we do nothing? Real pain point or hypothetical?
3. What existing code already partially or fully solves each sub-problem?
4. Complexity check: if the plan touches >8 files or adds >2 new classes, challenge whether fewer moving parts can achieve the same goal.
5. What could go wrong? Edge cases, under load, bad assumptions, external failures, security, race conditions, rollback safety?

Select scope mode:
- A) EXPAND — push scope up. what's the 10x version for 2x effort?
- B) HOLD — scope is right. make the plan bulletproof.
- C) REDUCE — strip to the minimum that ships value.

STOP and wait for mode selection before proceeding.

## Phase 1: Research & Analysis

1. Search the codebase for related implementations, patterns, and utilities
2. Read relevant files to understand existing architecture
3. Identify reusable functions, components, and abstractions
4. List required dependencies (existing and new)

## Phase 2: Design

1. Define the approach with clear steps
2. List all files to create or modify
3. Map out data flow and component interactions — for non-trivial flows, draw ASCII diagrams showing: happy path, nil/missing path, error path
4. Build an Error & Rescue Map: METHOD | FAILURE MODE | HANDLED? | USER SEES?
5. List interaction edge cases: double-submit, navigate-away, stale state, timeout, concurrent access
6. Identify potential breaking changes
7. Estimate scope (small/medium/large)

### Temporal Interrogation
- Hour 1 (foundations): what does the implementer need to know up front?
- Hour 2-3 (core logic): what ambiguities will they hit?
- Hour 4-5 (integration): what will surprise them?
- Hour 6+ (polish/tests): what will they wish they'd planned for?
Surface ambiguities NOW, not as "figure it out later."

## Phase 3: Risk Assessment

For each risk found:
- **Risk**: what could happen
- **Likelihood**: Low/Medium/High
- **Impact**: Low/Medium/High
- **Mitigation**: what to do about it

Failure Modes Registry:
CODEPATH | FAILURE MODE | RESCUED? | TEST? | USER SEES? | LOGGED?
Any row where RESCUED=N + TEST=N + USER SEES=Silent → CRITICAL GAP

Dream state delta: CURRENT STATE → THIS PLAN → 12-MONTH IDEAL

## Phase 4: Present Plan

- **Context**: why this change is needed
- **Approach**: recommended implementation
- **Files**: exact files to modify/create
- **What already exists**: reusable code, patterns, utilities found in Phase 1
- **Error & Rescue Map**: table from Phase 2
- **ASCII diagrams**: data flow, state machines, dependency graphs as needed
- **Risks**: what could go wrong and how we handle it
- **Not in scope**: what we're deliberately excluding, and why
- **Testing**: how to verify it works

## Phase 5: STOP
WAIT for explicit "proceed" or approval before writing any code.

Rules:
- Do NOT start coding during planning
- Reuse existing code whenever possible
- Flag any architectural concerns early
- Keep the plan concise but complete
