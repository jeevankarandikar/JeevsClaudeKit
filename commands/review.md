Comprehensive code review for: $ARGUMENTS

Review the specified code/PR thoroughly across these dimensions:

## 1. Code Quality
- Naming clarity (functions, variables, classes)
- Cyclomatic and cognitive complexity
- DRY violations
- Dead code or unused imports
- Consistent patterns with rest of codebase

## 2. Correctness & Robustness
- Error handling completeness
- Input validation at system boundaries
- Edge cases (null, empty, extreme values, concurrent access)
- Race conditions or async pitfalls
- Off-by-one errors, boundary conditions

## 3. Testing
- Test coverage for new/changed code
- Missing test scenarios
- Test quality (do they actually verify behavior?)
- Integration vs unit test balance

## 4. Security (OWASP Top 10)
- Input sanitization
- Authentication/authorization checks
- Sensitive data exposure
- SQL injection, XSS, command injection
- Insecure dependencies

## 5. Performance
- Obvious bottlenecks (N+1 queries, unnecessary loops)
- Database query efficiency
- Memory leaks or unbounded growth
- Async/await correctness

## 6. Documentation
- Public API docs present
- Complex logic explained
- README updates if needed

## Output Format
Summarize findings as a structured list:
- **Critical**: Must fix before merge
- **Warning**: Should fix, not blocking
- **Suggestion**: Nice to have improvements
- **Positive**: Things done well (acknowledge good work)
