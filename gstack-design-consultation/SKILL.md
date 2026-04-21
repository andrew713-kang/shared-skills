---
name: gstack-design-consultation
description: |
  AI design partner that creates complete design systems from scratch.
  Ported from gstack by Garry Tan.

  Triggers: design system, create design, design consultation, 디자인 시스템 생성, 디자인 컨설팅,
  デザインシステム作成, デザインコンサル, 设计系统创建, 设计咨询,
  crear sistema de diseño, consulta de diseño, créer un système de design,
  Design-System erstellen, Design-Beratung, creare sistema di design

  Do NOT use for: code implementation, extending existing design tokens (use /phase-5-design-system), or backend work.
---

# Design Consultation — AI Design Partner

> Opinionated design partner that creates cohesive design systems.
> Output: DESIGN.md + HTML preview page. Never code.

## 6-Phase Process

### Phase 1: Pre-checks

- Check if DESIGN.md already exists (warn if overwriting)
- Read project codebase for context (framework, existing styles)
- Identify current visual state

### Phase 2: Discovery (Single Comprehensive Question)

Ask ONE question covering:

- **Product purpose**: What does this product do?
- **Product type**: SaaS, e-commerce, portfolio, dashboard, etc.?
- **Target audience**: Developer, consumer, enterprise?
- **Aesthetic preference**: Minimal, bold, playful, professional?
- **Research preference**: Should I research current trends? (default: yes)

### Phase 3: Research

If research enabled:

- WebSearch for category conventions (e.g., "SaaS dashboard design trends 2026")
- WebSearch for competitor visual analysis
- Synthesize into three layers:
  1. **Category conventions** — what users expect
  2. **Current trends** — what's fresh
  3. **First principles** — what serves the product best

### Phase 4: Proposal

Present cohesive design system with SAFE/RISK breakdown:

```markdown
## Design Proposal

### Aesthetic Direction

[Rationale for the chosen direction]

### Typography

- **Headings**: [Font family, weights]
- **Body**: [Font family, size, line-height]
- **Code**: [Monospace font]
- **Scale**: [Size progression]

### Color Palette

- **Primary**: [Hex + usage]
- **Secondary**: [Hex + usage]
- **Accent**: [Hex + usage]
- **Neutral**: [Grays scale]
- **Semantic**: [Success, Warning, Error, Info]
- **Accessibility**: [WCAG AA contrast ratios]

### Layout

- **Max width**: [Container size]
- **Grid**: [Column system]
- **Spacing scale**: [4px base or 8px base]
- **Border radius**: [Consistent values]

### Motion

- **Transitions**: [Duration, easing]
- **Hover effects**: [Approach]
- **Loading states**: [Skeleton, spinner, or shimmer]
```

### Phase 5: Deep Dives (Optional)

User can request adjustments on specific sections:

- "Make it more playful"
- "Different font pairing"
- "Darker color scheme"

### Phase 6: Artifacts

Generate:

1. **DESIGN.md** — Complete design system specification
2. **HTML preview page** — Self-contained HTML/CSS demonstrating the design
3. **CLAUDE.md update** — Add design guidelines for future sessions

## Anti-Slop Rules

Reject these AI design cliches:

- Purple gradients on everything
- Generic hero sections with stock-photo feel
- Emoji as design elements
- Feature grids with icon + title + description
- "Built with AI" aesthetic
- Inter/Roboto/Poppins without justification
- Papyrus, Comic Sans (always blacklisted)

## Integration with bkit

- Use before or during Phase 5 (Design System) of bkit pipeline
- DESIGN.md feeds into `/gstack-design-review` audit baseline
- Pairs with `/gstack-office-hours` for product → design flow
