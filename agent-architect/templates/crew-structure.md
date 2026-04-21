# 👥 Crew Structure Template (Hierarchical Manager)

## Overview

Based on **Agentic Patterns** (like CrewAI/AutoGen), this template defines how multiple agents collaborate under a Manager.

## 1. The Manager (Orchestrator)

- **Role**: Project Manager / Team Lead
- **Responsibility**:
  1.  Breaks down the user request into sub-tasks.
  2.  Delegates sub-tasks to specific agents.
  3.  Aggregates results and ensures quality.
- **Agent**: `[PMO]` or `[Architect]`

## 2. The Workers (Specialists)

| Role           | Agent           | Task                         | Tool                |
| :------------- | :-------------- | :--------------------------- | :------------------ |
| **Researcher** | `[Researcher]`  | Gather raw data & facts      | `Tavily Search`     |
| **Analyst**    | `[Consultant]`  | Analyze data & find insights | `Mental Frameworks` |
| **Creator**    | `[Storyteller]` | Write final report           | `File Write`        |
| **Critic**     | `[Critic]`      | Review & critique            | `Red Team`          |

## 3. Delegation Logic (Process Flow)

### Step 1: Planning (Manager)

> "Analyze the request: '[User Goal]'. Breakdown into 3 tasks."

### Step 2: Execution (Parallel/Sequential)

> **Task A (Research)** -> Assigned to `[Researcher]`
> **Task B (Drafting)** -> Assigned to `[Storyteller]` (Wait for Task A)

### Step 3: Review (Critic)

> **Task C (Quality Check)** -> Assigned to `[Critic]` input is Task B output.

### Step 4: Finalize (Manager)

> "Compile all outputs into `[Final_Report.md]`."

## 4. Usage in SKILL.md

```markdown
## 🤝 Collaboration Matrix (Crew Mode)

| Role      | Agent        | Trigger | Input        | Output        |
| :-------- | :----------- | :------ | :----------- | :------------ |
| **Lead**  | [PMO]        | Start   | User Request | Final Report  |
| **Sub 1** | [Researcher] | Step 1  | Topic        | Research Data |
| **Sub 2** | [Critic]     | Step 3  | Draft        | Feedback      |
```
