# 🧙‍♂️ The Genesis Wizard: Interactive Skill Generation

## Philosophy

**"Don't build files, build capabilities."**
This script acts as a "Wizard" that interviews the user and generates a complete, folder-ready skill package.

## 📜 The 5-Step Interview Protocol

### Step 1: Identity & Trigger

> **Wizard**: "새로운 스킬을 정의합니다. **누가(Agent)**, **언제(Trigger)** 이 스킬을 사용합니까?"
> **User**: "마케터가, 인스타그램 광고 문구를 쓸 때."
> **Result**: `trigger: ("instagram ad copy", "social media marketing")`

### Step 2: The Logic (Chain of Thought)

> **Wizard**: "이 작업을 수행하는 **전문가의 사고 과정**은 어떻게 됩니까? 1, 2, 3단계로 알려주세요."
> **User**: "1. 타겟 페르소나 분석, 2. 경쟁사 벤치마킹, 3. 카피라이팅."
> **Result**: `Analysis Chain: Step 1, Step 2, Step 3`

### Step 3: The Tools (Explicit Definition)

> **Wizard**: "이 과정에서 필요한 **외부 도구**나 **데이터**는 무엇입니까?"
> **User**: "유행하는 밈 검색(Exa), 경쟁사 인스타 피드 확인(Tavily)."
> **Result**: `AI Search Integration`

### Step 4: The Format (Deliverable)

> **Wizard**: "결과물은 어떤 **형태**입니까? (마크다운 보고서, 코드 파일, 디자인 시안)"
> **User**: "인스타 업로드용 텍스트와 이미지 프롬프트."
> **Result**: `templates/insta-caption.md`

### Step 5: The Red Team (Critic)

> **Wizard**: "이 결과물이 **실패**한다면 그 원인은 무엇일까요?"
> **User**: "톤앤매너가 브랜드와 안 맞거나, 너무 광고 같아서 거부감 들 수 있음."
> **Result**: `Quality Gates` & `[Critic]` Check

---

## 🏗️ Auto-Generation Structure (The Magic)

Wizard collects inputs and generates:

1.  **`SKILL.md`**: The core logic file.
2.  **`frameworks/{step-name}.md`**: The specialized knowledge (automatically retrieved from S.A.S. library or generated).
3.  **`templates/{output}.md`**: The standard output format.

> **Command to Trigger**: `/architect` (This activates the interview mode)
