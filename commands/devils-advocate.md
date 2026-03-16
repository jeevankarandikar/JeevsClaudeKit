Play devil's advocate for: $ARGUMENTS

Before this change ships, think like a hacker and a pessimist:

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

Be pessimistic. Be thorough. Better to find issues now than in production at 3am.
