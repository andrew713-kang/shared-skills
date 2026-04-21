---
name: strategy-consulting
description: MBB급 경영 전략 수립 파이프라인. PESTEL, Porter's 5 Forces, SWOT, BCG Matrix를 체인으로 연결하여 구조적 전략 분석을 수행합니다. 전략/경영 분석 요청 시 자동 트리거됩니다.
agents: [Consultant, Strategy, CEO, CSO]
trigger: 전략 수립, 경영 분석, 시장 진입 전략, 사업 타당성 분석, 경쟁 분석 요청 시
priority: critical
---

# 🏛️ Strategy Consulting Skill

## _McKinsey · BCG · Bain 수준의 구조적 전략 분석 엔진_

## 📋 When to Apply (발동 조건)

이 스킬은 다음 상황에서 자동 활성화됩니다:

- "전략 수립해줘", "사업 분석해줘" 등 경영 전략 관련 요청
- 신규 사업 타당성 검토 (Feasibility Study)
- 기존 사업의 포트폴리오 재편 / 피벗 전략
- 경쟁사 벤치마킹 및 차별화 전략 요청
- 투자자/이사회 대상 전략 보고서 작성

## 🎯 Mission (핵심 목표)

**데이터와 프레임워크에 기반한 실행 가능한 전략을 도출**하여, 의사결정자가 자신 있게 실행에 옮길 수 있는 수준의 보고서를 제공합니다.

## 🔗 Analysis Chain (분석 파이프라인)

> 아래 6단계는 반드시 순서대로 실행합니다. 각 단계의 결과물이 다음 단계의 입력이 됩니다.

### Step 1: PESTEL 거시환경 스캔

- **프레임워크**: [PESTEL 가이드](frameworks/pestel.md)
- **수행**: 정치(P), 경제(E), 사회(S), 기술(T), 환경(E), 법률(L) 6대 축 분석
- **검색**: Tavily로 최신 거시 경제 뉴스, 규제 변화 수집
- **결과물**: 6대 축별 핵심 트렌드 요약표

### Step 2: Porter's 5 Forces 산업 구조 분석

- **프레임워크**: [5 Forces 가이드](frameworks/five-forces.md)
- **수행**: 경쟁 강도, 공급자/구매자 교섭력, 대체재/신규 진입 위협 분석
- **검색**: Exa로 산업 리포트 및 경쟁사 동향 검색
- **결과물**: 산업 매력도 진단 (High/Medium/Low 등급)

### Step 3: 경쟁사 벤치마킹 (최소 3사)

- **수행**: 직접 경쟁사 3곳의 핵심 전략, 강점/약점, 차별화 포인트 비교
- **검색**: Tavily/Exa로 경쟁사 최신 뉴스, 재무 정보, 제품 전략 수집
- **결과물**: 경쟁사 비교 매트릭스

### Step 4: SWOT 종합 진단

- **프레임워크**: [SWOT Advanced 가이드](frameworks/swot-advanced.md)
- **수행**: Step 1~3의 데이터를 기반으로 내부(S/W) + 외부(O/T) 교차 분석
- **핵심**: 단순 나열이 아닌 **가중치 기반 정량적 SWOT** 수행
- **결과물**: SWOT 매트릭스 + SO/WO/ST/WT 전략 옵션

### Step 5: 전략 옵션 도출

- **프레임워크**: [BCG Matrix 가이드](frameworks/bcg-matrix.md)
- **수행**: BCG Matrix, Ansoff Matrix, 또는 Blue Ocean 캔버스 중 상황에 맞는 도구 선택
- **결과물**: 전략 옵션 3~5개 + 각각의 예상 효과/리스크

### Step 6: Action Plan + KPI 설정

- **수행**: 선택된 전략의 90일/180일/365일 실행 로드맵
- **포함**: 책임자, 예산 추정, 핵심 KPI, 리스크 시나리오(Best/Base/Worst)
- **결과물**: 실행 계획표 + 모니터링 체크포인트

## 🔍 AI Search Integration (실시간 검색 연동)

| 검색 엔진  | 검색 대상                                         | 활용 단계    |
| :--------- | :------------------------------------------------ | :----------- |
| **Tavily** | 최신 뉴스, 규제 변화, 경제 지표, 정책 동향        | Step 1, 3    |
| **Exa**    | 산업 리포트, 학술 논문, 기업 전략 문서, 혁신 사례 | Step 2, 3, 5 |

## ✅ Quality Gates (품질 기준)

### 반드시 포함 (Must Have)

- [ ] 모든 주장에 **출처(URL)** 첨부
- [ ] 경쟁사 최소 **3곳** 벤치마킹
- [ ] 리스크 시나리오 **3가지** (Best/Base/Worst)
- [ ] **MECE 원칙** 자체 검증 (중복·누락 없는지 체크)
- [ ] 실행 로드맵에 **정량적 KPI** 포함

### 금지 사항 (Anti-Patterns)

- ❌ 근거 없는 낙관적 전망 금지
- ❌ "경쟁사 없음" 주장 금지 (Blue Ocean이라도 간접 경쟁자 분석 필수)
- ❌ 단일 시나리오만 제시 금지
- ❌ 프레임워크 없는 직관적 분석 금지

## 📄 Output Template (결과물 형식)

### 1. Executive Summary (1페이지)

- 참조: [Executive Summary 템플릿](templates/executive-summary.md)

### 2. Full Strategy Report (상세)

- PESTEL 분석표 → 5 Forces 진단표 → 경쟁사 비교 → SWOT 가중치 → 전략 옵션 → 실행 로드맵

### 3. Action Matrix (실행 우선순위)

| 전략 항목 | 효과(Impact) | 실행 난이도 | 우선순위 | 담당       |
| :-------- | :----------- | :---------- | :------- | :--------- |
| [항목]    | H/M/L        | H/M/L       | 1~5      | [에이전트] |

## 🤝 Collaboration Matrix (협업 매트릭스)

| 호출 에이전트     | 역할               | 트리거 조건                  |
| :---------------- | :----------------- | :--------------------------- |
| **[Researcher]**  | 심층 리서치 보조   | Step 1~3에서 데이터 부족 시  |
| **[Data]**        | 정량 분석 지원     | SWOT 가중치 산정 시          |
| **[Finance]**     | 재무적 타당성 검증 | Step 5에서 투자 규모 산정 시 |
| **[Storyteller]** | 보고서 서사 구조화 | 최종 보고서 작성 시          |
| **[Global]**      | 해외 시장 인사이트 | 글로벌 진출 전략 포함 시     |
