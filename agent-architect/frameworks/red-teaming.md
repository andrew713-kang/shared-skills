# Red Teaming & Critical Verification Framework

## 1. Philosophy: "The Best Defense is a Good Attack"

**Red Teaming** is the practice of rigorously challenging plans, policies, systems, and assumptions by adopting an adversarial approach.
In S.A.S., the **[Critic]** agent (Red Team) exists not to stop the project, but to **bulletproof** it.

> "If we don't find the flaws, the market (or the enemy) will."

## 2. The 4-Step Red Teaming Loop

### Step 1: Pre-mortem (사전 부검)

- **Concept**: Assume the project has _already failed_ 6 months from now.
- **Question**: "What went wrong?" (Don't ask "What _might_ go wrong?")
- **Action**: List top 3 fatal failure causes (e.g., "Competitor slashed price by 50%", "Tech stack couldn't scale").

### Step 2: Assumption Inversion (가정 뒤집기)

- **Concept**: Identify the core belief holding the plan together.
- **Question**: "What if this fundamental truth is actually false?"
- **Action**:
  - Belief: "Users want more features."
  - Inversion: "What if users actually want _less_ friction, even with fewer features?"

### Step 3: Stress Testing (스트레스 테스트)

- **Concept**: Apply extreme pressure to the model.
- **Question**: "Will this hold up under 10x load / 0x budget / 50% team turnover?"
- **Action**: Simulate "Worst Case Scenarios".

### Step 4: The 10th Man Rule (제10의 사나이)

- **Concept**: If 9 people agree, the 10th person _must_ disagree.
- **Action**: The [Critic] agent serves as the designated dissenter, obligated to find a counter-argument even if the plan looks perfect.

## 3. Application in S.A.S. Workflows

### When to trigger [Critic]?

1.  **Strategic Decisions**: Market entry, pricing, M&A.
2.  **Code Architecture**: Before writing >1000 lines of code.
3.  **Security Review**: Before deployment.

### Output Format: "The Risk Report"

Every Red Team session must produce a concise report:

1.  **Critical Vulnerabilities**: Top 3 logic holes.
2.  **Blind Spots**: Things we didn't even think about.
3.  **Mitigation Strategy**: How to fix them (or accept the risk).
