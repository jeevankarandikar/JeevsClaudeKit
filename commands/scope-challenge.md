Challenge the scope and premise of: $ARGUMENTS

## Agents & Skills
- Invoke `superpowers:brainstorming` skill to explore the problem space before committing to a direction
- Dispatch `feature-dev:code-explorer` agent to find existing code that already solves parts of the problem

Before any work begins, think like a founder deciding where to invest limited resources.

## Premise Challenge
1. Is this the right problem? Could a different framing yield a simpler or more impactful solution?
2. What happens if we do nothing? Is this a real pain point or a hypothetical one?
3. Who benefits most from this? Users? Developers? The codebase?
4. What existing code already partially or fully solves each sub-problem?
5. Is there a 3rd-party tool, library, or service that handles this better than building it?

## Existing Code Leverage Check
Search the codebase for:
- Functions, modules, or patterns that overlap with the proposed work
- Prior attempts at solving similar problems (check git log)
- Utilities that could be composed instead of building from scratch

## Dream State Mapping
CURRENT STATE → THIS PLAN → 12-MONTH IDEAL
- Does this move toward the ideal, or is it a detour?
- What would need to change later to reach the ideal?
- Are we building something we'll want to tear down?

## Scope Options
Present three options with effort, risk, and what gets deferred:

### A) EXPAND — push scope up
What's the 10x version for 2x effort? What would we build if we knew we'd use it for 3 years?

### B) HOLD — scope is right
Make the plan bulletproof. What's missing? What's underestimated?

### C) REDUCE — strip to minimum
What's the smallest thing that ships value? What can we defer without losing the core benefit?

For each option: estimated effort, risk level, what gets deferred, and what we learn.

## Temporal Interrogation
- Hour 1 (foundations): what does the implementer need to know up front?
- Hour 2-3 (core logic): what ambiguities will they hit?
- Hour 4-5 (integration): what will surprise them?
- Hour 6+ (polish/tests): what will they wish they'd planned for?

Surface ambiguities NOW, not as "figure it out later."

## STOP
Present all three options and wait for the user to select before proceeding to any planning or implementation.
