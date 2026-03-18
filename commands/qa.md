Systematic QA testing for: $ARGUMENTS

## Agents & Skills
- Use Playwright MCP tools (`browser_navigate`, `browser_snapshot`, `browser_click`, `browser_take_screenshot`) for all browser interactions
- If visual issues are found, dispatch `pr-review-toolkit:code-reviewer` agent on the relevant frontend files

Uses Playwright browser automation for visual and functional testing.

## Prerequisites
1. Check if Playwright plugin is enabled in settings. If not: STOP and tell the user to enable it.
2. Determine the dev server URL (from CLAUDE.md, package.json scripts, or ask the user).

## Step 1: Orient
1. Navigate to the root URL, take a screenshot
2. Map primary navigation — list all reachable pages/routes
3. Check browser console for errors on initial load
4. Note the tech stack visible in the page (framework, CSS approach)

## Step 2: Scope Selection
Choose a tier based on $ARGUMENTS or ask:
- **Quick** (homepage + 5 key pages, ~30 seconds): smoke test core flows
- **Standard** (8-12 pages, 2-3 minutes): systematic page-by-page testing
- **Exhaustive** (all discoverable pages, 5-10 minutes): full coverage including edge cases

## Step 3: Diff-Aware Mode (if applicable)
If there's an active branch with changes:
1. `git diff main...HEAD --name-only` to find changed files
2. Map changed files to affected pages/routes
3. Prioritize testing those pages first

## Step 4: Systematic Testing
For each page in scope:
1. Navigate and screenshot
2. Check console for errors/warnings
3. Test interactive elements: buttons, forms, links, dropdowns, modals
4. Test responsive behavior: desktop (1280px), tablet (768px), mobile (375px)
5. Verify text is readable, images load, layout doesn't break

## Issue Documentation
For each issue found, record:
- **ID**: QA-NNN
- **Severity**: critical (broken functionality) / high (major visual bug) / medium (minor visual) / low (polish)
- **Category**: visual / functional / ux / content / performance / console / accessibility
- **Page**: URL or route
- **Description**: what's wrong
- **Repro**: steps to reproduce
- **Screenshot**: if applicable

## Severity Definitions
- **Critical**: feature is broken, data loss possible, page won't load, security issue
- **High**: feature works but incorrectly, major layout break, form doesn't submit
- **Medium**: visual inconsistency, minor layout issue, content typo, slow interaction
- **Low**: polish item, spacing tweaks, hover state missing, minor alignment

## Health Score
Calculate 0-100 score:
- Start at 100
- Critical: -25 each
- High: -10 each
- Medium: -3 each
- Low: -1 each

## Report
1. **Health Score**: N/100
2. **Issues Found**: N (X critical, Y high, Z medium, W low)
3. **Top 3 to fix first**: ordered by severity then effort
4. **Full issue list**: sorted by severity
5. **Pages tested**: list with pass/fail status
