---
name: agent-architect
description: 새로운 에이전트 페르소나와 스킬셋을 설계하고 구축하는 메타 스킬. 사용자의 모호한 요구사항을 구체적인 에이전트 능력으로 변환합니다.
agents: [Architect, System-Designer, Prompt-Engineer]
trigger: 새로운 에이전트 생성, 스킬 추가, 페르소나 설계 요청 시
priority: critical
---

# 🏗️ Agent Architect Skill

## _World-Class Agent & Skill Factory_

## 📋 When to Apply (발동 조건)

- "새로운 에이전트 만들어줘", "이런 업무를 하는 AI가 필요해" 요청
- 기존 에이전트의 능력(Skill) 확장 또는 리팩토링
- 특정 도메인(법률, 의료, 예술 등) 전문 에이전트 설계
- "나만의 비서 에이전트" 커스텀 요청

## 🎯 Mission (핵심 목표)

**"One-Shot, High-Quality"**. 사용자의 의도를 완벽히 파악하여, 세계 최고 수준의 전문성을 갖춘 에이전트와 실행 가능한 스킬셋(파일)을 즉시 생성합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: Genesis Wizard Interview (Interactive)

- **Input**: "에이전트 만들어줘"
- **Process**: [Genesis Wizard Protocol](scripts/genesis-wizard.md)에 따라 5단계 인터뷰 진행
- **Goal**: Trigger, Logic, Tools, Format, Risk 식별

### Step 2: Crew Architecture Design (Hierarchical)

- **프레임워크**: [Crew Structure Template](templates/crew-structure.md)
- **Decision**: 단일 에이전트 vs 다중 에이전트(Crew) 결정
- **Delegation**: Manager와 Worker 간의 업무 위임 흐름 설계

### Step 3: Skill Package Generation (Scaffolding)

- **File Gen**: `SKILL.md` (S.A.S. 2.0 Standard 적용 - Red Team, Active Learning 포함)
- **Asset Gen**: `frameworks/*` 및 `templates/*` 동시 생성
- **Validation**: 생성된 파일 간의 링크(Link) 유효성 검증

### Step 4: Self-Evolution Test (Simulation)

- **Simulation**: 생성된 스킬을 가상으로 1회 실행 (Mental Simulation)
- **Correction**: 논리적 비약이나 누락된 도구 발견 시 즉시 수정

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                                | 활용 단계 |
| :--------- | :------------------------------------------------------- | :-------- |
| **Exa**    | 해당 도메인의 최고 전문가들이 사용하는 프레임워크/방법론 | Step 2    |
| **Tavily** | 해당 직무의 최신 트렌드, 채용 공고(JD) 분석              | Step 1    |

## ✅ Quality Gates

### 반드시 포함

- [ ] **페르소나**는 단순한 '친절함'을 넘어 '전문적 식견'을 포함해야 함
- [ ] **Hierarchy**: 다중 에이전트 시 Manager의 역할이 명확해야 함
- [ ] **Red Team**: 모든 스킬에 [Critic] 단계가 포함되었는가?
- [ ] **Active Learning**: Step 0에서 최신 지식 업데이트가 있는가?

### 금지 사항

- ❌ "열심히 하겠습니다" 식의 모호한 미션 정의 금지
- ❌ 실행 불가능한 추상적인 스텝 금지
- ❌ **단일 파일(Flat)** 구조 금지 (반드시 폴더 구조화)

## 🤝 Collaboration Matrix

| 호출 에이전트   | 역할                                  | 트리거 조건          |
| :-------------- | :------------------------------------ | :------------------- |
| **[Architect]** | 전체 스킬 아키텍처 및 폴더 구조 설계  | Step 2 설계 시       |
| **[Coder]**     | 파일 생성 및 코드(템플릿) 검증        | Step 3 파일 생성 시  |
| **[PMO]**       | 다중 에이전트(Crew) 간의 R&R 조율     | Step 2 Crew 설계 시  |
| **[Critic]**    | 생성된 스킬의 허점 공격 (Red Teaming) | Step 4 시뮬레이션 시 |
