Agentic feature planning for: $ARGUMENTS

## Agents & Skills
- Invoke `superpowers:brainstorming` skill during Phase 0 (scope challenge)
- Invoke `superpowers:writing-plans` skill during Phase 2-3 (design and plan presentation)
- Dispatch `feature-dev:code-architect` agent for Phase 1 (codebase research) and Phase 2 (architecture design)
- Dispatch `feature-dev:code-explorer` agent to find existing patterns and reusable code

Before writing ANY code, follow this sequence:

## Phase 0: Scope & Premise Challenge
1. Is this the right problem? Could a different framing yield a simpler or more impactful solution?
2. What happens if we do nothing? Real pain point or hypothetical?
3. What existing code already partially or fully solves each sub-problem?
4. Complexity check: if the plan touches >8 files or adds >2 new classes, challenge whether fewer moving parts can achieve the same goal.

Select scope mode:
- A) EXPAND — push scope up. what's the 10x version for 2x effort?
- B) HOLD — scope is right. make the plan bulletproof.
- C) REDUCE — strip to the minimum that ships value.

STOP and wait for mode selection before proceeding.

## Phase 1: Research & Analysis
1. Search the codebase for related implementations, patterns, and utilities
2. Read relevant files to understand existing architecture
3. Identify reusable functions, components, and abstractions
4. Research best practices for this type of feature
5. List required dependencies (existing and new)

## Phase 2: Design
1. Define the approach with clear steps
2. List all files to create or modify
3. Map out data flow and component interactions
4. Identify potential breaking changes
5. Consider edge cases and error scenarios
6. Estimate scope (small/medium/large)
7. For non-trivial data flows, draw ASCII diagrams showing: happy path, nil/missing path, empty path, error/upstream-failure path
8. Build an Error & Rescue Map for methods that can fail:
   METHOD | FAILURE MODE | HANDLED? | USER SEES?
9. List interaction edge cases: double-submit, navigate-away, stale state, timeout, concurrent access

## Phase 2.5: Temporal Interrogation
- Hour 1 (foundations): what does the implementer need to know up front?
- Hour 2-3 (core logic): what ambiguities will they hit?
- Hour 4-5 (integration): what will surprise them?
- Hour 6+ (polish/tests): what will they wish they'd planned for?
Surface ambiguities NOW, not as "figure it out later."

## Phase 3: Present Plan
Present findings as a structured plan:
- **Context**: Why this change is needed
- **Approach**: Recommended implementation
- **Files**: Exact files to modify/create
- **What already exists**: Reusable code, patterns, and utilities found in Phase 1
- **Error & Rescue Map**: Table from Phase 2
- **ASCII Diagrams**: Data flow, state machines, dependency graphs as needed
- **Risks**: What could go wrong
- **Not in scope**: What we're deliberately excluding, and why
- **Testing**: How to verify it works
- **Dream state delta**: CURRENT STATE → THIS PLAN → 12-MONTH IDEAL

## Phase 4: STOP
WAIT for explicit "proceed" or approval before writing any code.

Rules:
- Do NOT start coding during planning
- Reuse existing code whenever possible
- Flag any architectural concerns early
- Keep the plan concise but complete
