---
name: [skill-name]
description: [한 줄 요약]
agents: [[Main-Agent], [Sub-Agent]]
trigger: [키워드 1], [키워드 2], [상황]
priority: high
---

# 🛠️ [Skill Name] Skill

## _[한 줄 부제 / 슬로건]_

## 📋 When to Apply (발동 조건)

- "[상황 1]" 요청 시
- [구체적 트리거 상황]
- [해결하고자 하는 문제]

## 🎯 Mission (핵심 목표)

**[핵심 가치]**를 달성합니다. [어떻게] 하여 [무엇을] 해결합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 0: Context & Framework Check (Active Learning)

- **Search**: [Skill Domain] 관련 최신 트렌드/법규/기술 변화 검색
- **Update**: 기존 프레임워크가 유효한지 판단하고, 필요 시 보완

### Step 1: [단계명]

- [활동 1]
- **프레임워크**: [[가이드 문서]](frameworks/guide.md)
- **검색**: [검색 키워드/대상]

### Step 2: [단계명]

- [활동 1]
- [활동 2]

...

### Step X: Red Team Review (Devil's Advocate)

- **Agent**: **[Critic]**
- **Action**: [결과물]에 대한 비판적 검증 및 논리적 허점 공격
- **Guide**: [Red Teaming Framework](../agent-architect/frameworks/red-teaming.md)

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상     | 활용 단계 |
| :--------- | :------------ | :-------- |
| **Exa**    | [검색 대상 1] | Step [N]  |
| **Tavily** | [검색 대상 2] | Step [M]  |

## ✅ Quality Gates

### 반드시 포함

- [ ] **[조건 1]**
- [ ] **[조건 2]**
- [ ] **Red Team Pass**: [Critic]의 검증을 통과했는가?

### 금지 사항

- ❌ [금지 1]
- ❌ [금지 2]

## 🤝 Collaboration Matrix

| 호출 에이전트 | 역할   | 트리거 조건      |
| :------------ | :----- | :--------------- |
| **[Critic]**  | 레드팀 | 최종 제출 전     |
| **[Agent]**   | [역할] | Step [N] 수행 시 |
