Systematic QA testing for: $ARGUMENTS

Detects platform automatically:
- `.xcodeproj` / `.xcworkspace` found → iOS mode (Xcode simulator)
- Web project (package.json with dev server) → Browser mode (Playwright)

---

## iOS Mode

### Step 1: Build & Run
1. Detect scheme: `xcodebuild -list -json` → pick the app scheme
2. Build for simulator: `xcodebuild -scheme <scheme> -destination 'platform=iOS Simulator,name=iPhone 16' build`
3. If build fails: STOP and report errors (use `/build` to fix)

### Step 2: Code-Level QA
Search the codebase for common iOS issues:
- Force unwraps (`!`) outside of IBOutlets — flag each one
- Missing `@MainActor` on view model mutations
- Network calls without error handling
- Missing loading states (ProgressView) for async operations
- Hardcoded strings that should be localized
- Missing accessibility labels on interactive elements
- Views without `.task {}` cleanup or cancellation handling

### Step 3: Architecture Review
- Are all views using the MVVM pattern consistently?
- Are services properly injected (not instantiated in views)?
- Is navigation handled consistently?
- Are models Codable/Identifiable where needed?

### Step 4: Report (iOS)
- Build status: PASS/FAIL
- Code issues found: N (by severity)
- Architecture issues: N
- Top 3 to fix first

---

## Browser Mode (Playwright)

### Prerequisites
1. Check if Playwright plugin is enabled. If not: STOP.
2. Determine the dev server URL (from CLAUDE.md, package.json, or ask).

### Step 1: Orient
1. Navigate to root URL, take a screenshot
2. Map primary navigation — list all reachable pages/routes
3. Check browser console for errors on initial load

### Step 2: Scope Selection
Choose tier based on $ARGUMENTS or ask:
- **Quick** (homepage + 5 key pages): smoke test core flows
- **Standard** (8-12 pages): systematic page-by-page
- **Exhaustive** (all discoverable pages): full coverage

### Step 3: Diff-Aware Mode
If there's an active branch:
1. `git diff main...HEAD --name-only` to find changed files
2. Map changed files to affected pages
3. Prioritize testing those pages first

### Step 4: Systematic Testing
For each page:
1. Navigate and screenshot
2. Check console for errors/warnings
3. Test interactive elements: buttons, forms, links, dropdowns, modals
4. Test responsive: desktop (1280px), tablet (768px), mobile (375px)
5. Verify text readable, images load, layout intact

### Issue Documentation
For each issue:
- **Severity**: critical / high / medium / low
- **Category**: visual / functional / ux / content / performance / console / accessibility
- **Page**: URL or route
- **Description**: what's wrong

### Health Score (0-100)
Start at 100. Critical: -25, High: -10, Medium: -3, Low: -1.

### Report (Browser)
1. Health score: N/100
2. Issues found: N (by severity)
3. Top 3 to fix first
4. Full issue list sorted by severity
