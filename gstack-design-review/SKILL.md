---
name: gstack-design-review
description: |
  80-item live site visual audit with CSS-only fixes.
  Ported from gstack by Garry Tan. Requires /gstack-browse daemon running.

  Triggers: design review, visual audit, design audit, UI audit, 디자인 리뷰, 시각 감사,
  デザインレビュー, 視覚監査, 设计审查, 视觉审计,
  revisión de diseño, auditoría visual, revue de design, audit visuel,
  Design-Review, visuelle Prüfung, revisione del design, audit visivo

  Do NOT use for: code-only reviews, API testing, or projects without UI.
---

# Design Review — Visual Audit & Atomic Fixes

> 80-item visual audit of live site with CSS-only atomic fixes.
> Prerequisite: `/gstack-browse` daemon must be running.

## Audit Categories (80 items)

### Typography (12 items)

- Font family consistency
- Font size hierarchy (h1 > h2 > h3 > body)
- Line height readability (1.4-1.6 for body)
- Letter spacing appropriateness
- Font weight contrast
- Text color contrast (WCAG AA: 4.5:1 minimum)
- Heading capitalization consistency
- Paragraph max-width (45-75 characters)
- Link text distinguishability
- Code font consistency
- List styling consistency
- Text truncation handling

### Color & Theme (10 items)

- Primary color usage consistency
- Background/foreground contrast
- Hover/focus state visibility
- Active state feedback
- Error state color (red family)
- Success state color (green family)
- Warning state color (amber family)
- Dark mode consistency (if applicable)
- Color-blind safe palette
- Brand color adherence

### Layout & Spacing (15 items)

- Grid alignment consistency
- Section spacing rhythm
- Component padding consistency
- Margin collapse handling
- Max-width container usage
- Mobile responsive breakpoints
- Sticky/fixed element behavior
- Z-index stacking order
- Overflow handling
- Whitespace balance
- Card/component alignment
- Footer positioning
- Header layout
- Sidebar proportions
- Content area width

### Interactive Elements (15 items)

- Button size (minimum 44x44px touch target)
- Button hover/focus states
- Form input focus indicators
- Checkbox/radio styling
- Select dropdown appearance
- Loading state indicators
- Disabled state visibility
- Error message placement
- Success feedback
- Navigation active state
- Dropdown menu alignment
- Modal overlay darkness
- Toast/notification placement
- Scroll behavior
- Transition smoothness

### Accessibility (10 items)

- Focus visible indicators
- Skip navigation link
- Image alt text presence
- Form label association
- ARIA landmarks
- Keyboard navigation order
- Screen reader text
- Color-only information
- Motion preferences
- Touch target size

### Content & Assets (8 items)

- Image aspect ratio consistency
- Icon size consistency
- Avatar/thumbnail sizing
- Placeholder content
- Empty state design
- Loading skeleton
- Error page design
- 404 page design

### Consistency (10 items)

- Component style reuse
- Border radius consistency
- Shadow depth consistency
- Animation timing consistency
- Icon style consistency (outline vs filled)
- Spacing scale adherence
- Color palette adherence
- Typography scale adherence
- State pattern consistency
- Platform convention adherence

## Workflow

### Phase 1-6: Baseline Audit

- Navigate to each page, take screenshots
- Score each of the 80 items (pass/warn/fail)
- Document findings with specific CSS selectors

### Phase 7: Triage

- Sort by impact: high > medium > polish
- Group by page for efficient fixing

### Phase 8: Fix Loop (CSS-only)

- Apply CSS-only fixes (no structural HTML changes)
- One commit per fix (atomic rollback)
- Re-screenshot after each fix

### Phase 9-11: Final Audit & Report

## Safety Rules

| Rule                  | Description                                     |
| --------------------- | ----------------------------------------------- |
| CSS-only fixes        | No structural HTML or JS changes                |
| Max 30 fixes per run  | Stop if risk exceeds 20%                        |
| One commit per fix    | Atomic rollback capability                      |
| Revert on regression  | Undo immediately if fix breaks something        |
| DESIGN.md calibration | Use project design system as baseline if exists |

## Integration with bkit

- Use during Phase 8 (Review) of bkit development pipeline
- Complements `/gstack-qa` (functional) with visual quality checks
- Results feed into PDCA Check phase
