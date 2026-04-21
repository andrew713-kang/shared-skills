---
name: gstack-office-hours
description: |
  YC-style product reframing session. Pressure-tests ideas before coding begins.
  Ported from gstack by Garry Tan.

  Use before /pdca plan to validate product direction and improve plan quality.

  Triggers: office hours, brainstorm, idea review, product thinking, 오피스 아워, 아이디어 검증, 제품 리프레이밍,
  オフィスアワー, アイデア検証, 办公时间, 想法验证,
  horas de oficina, lluvia de ideas, heures de bureau, remue-méninges,
  Sprechstunde, Brainstorming, ore di ricevimento, brainstorming

  Do NOT use for: implementation tasks, code review, or when the plan is already finalized.
---

# Office Hours — Product Reframing Session

> A YC partner pressure-testing your idea before you write a single line of code.
> Output: Design document, never code.

## Two Modes

### Startup Mode (Default)

For new products or features where demand is unvalidated.
**Stance**: Skeptical but constructive — push for specificity and evidence.

### Builder Mode

For projects where the direction is clear and the goal is to find the coolest version.
**Stance**: Enthusiastic design partner — help amplify the vision.

Ask the user which mode fits, or auto-detect from context.

## Session Flow

### Step 1: Context Gathering

Read the repository structure, README, and any existing docs to understand:

- What exists today
- What the user is trying to build
- Who the target users are

### Step 2: The Six Forcing Questions (Startup Mode)

Ask ONE question at a time. Wait for the answer before asking the next.
Push for specificity — "who specifically?" not "who?"

1. **Demand Reality**: "Who is desperate for this right now, and how do you know? Not 'would use' — actually desperate."

2. **Narrowest Wedge**: "What's the absolute smallest version that would make one person switch from their current solution?"

3. **Distribution Edge**: "How does your first user find this? Not 'marketing plan' — the literal first 10 users."

4. **Premise Test**: "What has to be true about the world for this to work? List your assumptions."

5. **Kill Shot**: "What's the single most likely reason this fails? Be honest."

6. **Forced Alternative**: "If you couldn't build this exact thing, what's the simplest version that still solves the core problem?"

### Step 3: Premise Challenge

After the six questions, articulate back:

- The core premises that must be true
- Which premises are validated vs. assumed
- The riskiest assumption

### Step 4: Forced Alternatives

Present 2-3 distinct approaches:

| Approach     | Description                                  | Risk   | Effort |
| ------------ | -------------------------------------------- | ------ | ------ |
| **Minimal**  | Smallest thing that validates the hypothesis | Low    | Low    |
| **Ideal**    | The full vision, properly scoped             | Medium | High   |
| **Creative** | An unexpected angle on the same problem      | Varies | Varies |

### Step 5: Design Document Output

Produce a structured design document capturing:

```markdown
## Product Brief

### Problem

[Specific problem statement with evidence]

### Target User

[Specific persona, not "everyone"]

### Core Insight

[Why now? What changed?)

### Solution

[The chosen approach from Step 4]

### Success Metrics

[How do we know this is working?]

### Risks & Mitigations

[Top 3 risks and how to address each]

### Non-Goals

[What we are explicitly NOT doing]
```

Save to project root or docs/ directory as appropriate.

## Anti-Sycophancy Rules

- **Take positions**: "I think X is a better approach because..." not "Both are good options!"
- **Challenge vague answers**: "Can you be more specific?" not "That sounds great!"
- **Name risks directly**: "This might fail because..." not "There are some considerations..."
- **Respect final decisions**: Push back, but accept the user's choice after making your case

## Integration with bkit

After office hours produces a design document:

- Run `/pdca plan {feature}` to create a formal PDCA Plan
- The design document feeds directly into Plan quality
- Reference the office hours output in the Plan's "Background" section
