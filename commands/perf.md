Performance analysis for: $ARGUMENTS

Analyze the specified code for performance issues:

## 1. Time Complexity
- Identify Big O notation for key operations
- Flag any O(n^2) or worse algorithms
- Suggest more efficient alternatives with benchmarks

## 2. Database & I/O
- N+1 query problems
- Missing indexes (check query patterns)
- Unnecessary round trips
- Unbatched operations
- Connection pool sizing

## 3. Memory
- Unbounded data structures
- Memory leaks (event listeners, closures, caches)
- Large object allocations in hot paths
- Missing cleanup/disposal

## 4. Async & Concurrency
- Blocking operations on main thread
- Sequential operations that could be parallel
- Promise/async-await anti-patterns
- Race conditions under load

## 5. Caching & Network
- Missing caching opportunities
- Cache invalidation issues
- Redundant API calls
- Payload size optimization

## Output
For each issue found:
1. **Location**: File and line
2. **Problem**: What's wrong and why it matters
3. **Impact**: Estimated performance cost
4. **Fix**: Specific code change with before/after
5. **Measurable improvement**: How to verify the fix works
