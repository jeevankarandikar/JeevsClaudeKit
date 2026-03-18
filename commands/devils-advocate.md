Play devil's advocate for: $ARGUMENTS

## Agents & Skills
Dispatch these agents in parallel to find risks:
- `pr-review-toolkit:silent-failure-hunter` — error handling gaps, silent failures, fallback abuse
- `pr-review-toolkit:code-reviewer` — code quality issues that could become bugs
- `pr-review-toolkit:pr-test-analyzer` — missing test coverage for failure paths
Synthesize agent findings into the risk assessment below.

Before this change ships, think like a hacker and a pessimist:

## Premise Challenge
1. Is this the right problem? Could a different framing yield a simpler solution?
2. What happens if we do nothing? Real pain point or hypothetical?
3. Dream state mapping:
   CURRENT STATE → THIS CHANGE → 12-MONTH IDEAL
   Does this move toward or away from that?

## What Could Go Wrong?

1. **Edge Cases**: What inputs/states did we miss? (null, empty, concurrent, huge, malformed)
2. **Under Load**: What happens with 10x, 100x, 1000x the expected traffic?
3. **Bad Assumptions**: What are we assuming that might not be true in production?
4. **External Failures**: What if the database is slow? API is down? Network is flaky?
5. **Bad Data**: What if upstream sends garbage? What if the schema changes?
6. **Security**: Could this be exploited? Injected? Abused?
7. **Race Conditions**: What if two users hit this simultaneously?
8. **Rollback**: If this breaks, can we safely revert? What's the blast radius?

## For Each Risk Found
- **Risk**: What could happen
- **Likelihood**: Low/Medium/High
- **Impact**: Low/Medium/High
- **Mitigation**: What to do about it

## Failure Modes Registry
For each new codepath:
CODEPATH | FAILURE MODE | RESCUED? | TEST? | USER SEES? | LOGGED?
Any row where RESCUED=N + TEST=N + USER SEES=Silent → CRITICAL GAP

## Temporal Risk Assessment
- Hour 1 of outage: what breaks first? blast radius?
- Hours 2-3: cascade effects?
- Day 1 post-deploy: what will users report?
- Week 1: what slow-burn issues surface?

## Deployment Risk
- Can this be safely reverted with `git revert`?
- Old code + new code running simultaneously during deploy — what breaks?
- Should any part be behind a feature flag?
- Post-deploy verification checklist: first 5 minutes, first hour

Be pessimistic. Be thorough. Better to find issues now than in production at 3am.
