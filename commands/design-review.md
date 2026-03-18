Visual design review for: $ARGUMENTS

## Agents & Skills
- Dispatch `pr-review-toolkit:type-design-analyzer` agent if the diff touches component types/interfaces
- Use Playwright MCP tools (`browser_navigate`, `browser_take_screenshot`, `browser_snapshot`) for visual verification
- Invoke `frontend-design:frontend-design` skill for design quality assessment

Reviews frontend code in the current diff for visual quality, consistency, and AI slop.

## Prerequisites
1. Check if the diff touches frontend files (.tsx, .jsx, .vue, .svelte, .html, .css, .scss, .less, .tailwind).
   If no frontend files changed: say so and stop.
2. If DESIGN.md exists, read it for calibration.
3. If Playwright is enabled, use it for visual verification. Otherwise, review code only.

## Pass 1: Auto-Fixable Issues
These can be fixed without discussion:
- `outline: none` without a replacement focus style
- `!important` in new CSS (flag, almost always wrong)
- Body text below 16px
- Missing `alt` attributes on images
- Hardcoded color values that should use design tokens
- `px` values that don't match the spacing scale

## Pass 2: Needs Input
These require discussion or judgment:

### AI Slop Detection
Check for these common AI-generated design patterns:
- [ ] Purple/violet gradients as default accent
- [ ] 3-column feature grids with icons in circles
- [ ] Centered-everything layout with no visual hierarchy
- [ ] Uniform border-radius on all elements
- [ ] Generic hero copy ("Revolutionize your workflow", "Seamlessly integrate")
- [ ] Icons-in-circles as the only visual element
- [ ] Excessive shadows on every component

### Typography
- [ ] Body text ≥ 16px
- [ ] Heading hierarchy is clear (h1 > h2 > h3 visually)
- [ ] No more than 2-3 font families
- [ ] No blacklisted fonts (Comic Sans, Papyrus, Impact for body text)
- [ ] Line height appropriate (1.4-1.7 for body text)

### Spacing
- [ ] Values follow the defined spacing scale
- [ ] No fixed widths without responsive fallback
- [ ] Text containers have max-width (45-75ch for readability)
- [ ] Consistent padding/margin patterns

### Interaction States
- [ ] Hover states on interactive elements
- [ ] Focus styles present (keyboard navigation)
- [ ] Active/pressed states
- [ ] Disabled states are visually distinct
- [ ] Touch targets ≥ 44px on mobile

### DESIGN.md Violations (if DESIGN.md exists)
- [ ] Colors match the palette
- [ ] Fonts match the type system
- [ ] Spacing matches the scale
- [ ] Border radii match the hierarchy

## Output Format
`Design Review: N issues (X auto-fixable, Y need input, Z possible AI slop)`

For each issue:
- File:line
- Category (auto-fix / needs-input / ai-slop)
- What's wrong
- Suggested fix

End with positive observations — things done well visually.
