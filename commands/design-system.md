Design system creation for: $ARGUMENTS

## Agents & Skills
- Invoke `superpowers:brainstorming` skill to explore aesthetic directions before committing
- Invoke `frontend-design:frontend-design` skill for production-grade design decisions

Guided design system creation that produces a DESIGN.md file with all visual decisions documented.

## Step 1: Check Existing State
- Does DESIGN.md already exist? If yes, read it — we're updating, not starting fresh.
- Gather product context: README, package.json, directory structure, existing CSS/styles.
- Identify existing visual patterns: colors, fonts, spacing already in use.

## Step 2: Product Context
- What is this product? Who uses it?
- What feeling should it evoke? (professional, playful, technical, warm, minimal)
- Any brand constraints? (existing logos, colors, typography)
- Competitive landscape: what do similar products look like?

Optional: run WebSearch for competitive research if the user wants it.

## Step 3: Propose Design System
Present a complete system for approval:

### Aesthetic Direction
One sentence describing the visual philosophy.

### Typography
Propose 3 fonts with specific roles:
- **Headings**: font name, weight, rationale
- **Body**: font name, weight, rationale
- **Code/Mono**: font name, rationale

### Color Palette
- **Primary**: hex + usage
- **Secondary**: hex + usage
- **Accent**: hex + usage
- **Neutrals**: 5-point scale (50, 200, 400, 600, 900) + usage
- **Semantic**: success, warning, error, info
- **Dark mode**: if applicable, inverse palette

### Spacing Scale
Base unit and scale (e.g., 4px base: 4, 8, 12, 16, 24, 32, 48, 64, 96)

### Layout Approach
Max-width, grid system, breakpoints, container behavior.

### Motion
Transition durations, easing curves, what animates and what doesn't.

### Border Radius Hierarchy
Different radii for different contexts (buttons, cards, modals, pills).

### SAFE vs RISK
- **SAFE choices**: where to follow conventions (navigation, forms, data tables)
- **RISK choices**: where to differentiate (hero sections, branding, interactions)

## AI Slop Detection (anti-patterns to avoid)
- Purple/violet gradients as default accent
- 3-column icon-in-circle feature grids
- Centered everything with no visual hierarchy
- Uniform bubbly border-radius on all elements
- Generic hero copy ("Revolutionize your workflow")
- Stock photo backgrounds with text overlay
- Excessive drop shadows on every element

## Step 4: Preview
Generate a self-contained HTML file that previews:
- Typography samples at all heading levels + body
- Color swatches with hex values
- Spacing scale visualization
- Button variants (primary, secondary, ghost)
- A sample card component

Open it in the browser for the user to review.

STOP and wait for feedback before writing DESIGN.md.

## Step 5: Write DESIGN.md
Write the complete design system to DESIGN.md with:
- All decisions from Step 3
- Rationale for each choice
- Decision log (date + what was decided + why)

## Step 6: Update CLAUDE.md
Add a reference to DESIGN.md in the project's CLAUDE.md so future sessions know to consult it for visual decisions.
