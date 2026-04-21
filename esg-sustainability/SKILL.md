---
name: esg-sustainability
description: ESG 경영 전략, 지속가능성 보고, 탄소중립 로드맵 수립 파이프라인. ESG 평가, 규제 대응, 지속가능 경영 요청 시 자동 트리거됩니다.
agents: [ESG, Compliance]
trigger: ESG 분석, 탄소중립, 지속가능성 보고, ESG 평가 대응, 그린워싱 방지 요청 시
priority: high
---

# 🌱 ESG & Sustainability Skill

## _글로벌 규제 대응 및 지속가능 경영 전략 엔진_

## 📋 When to Apply (발동 조건)

- "ESG 전략 수립해줘", "탄소중립 로드맵" 등 요청
- ESG 평가 기관(KCGS, MSCI, S&P) 등급 향상 전략
- 지속가능성 보고서 작성 (GRI, SASB, TCFD 표준)
- EU Taxonomy, CSRD 등 글로벌 규제 대응
- 공급망 ESG 리스크 진단

## 🎯 Mission (핵심 목표)

**ESG를 비용이 아닌 경쟁 우위로 전환**합니다. 규제 대응을 넘어 투자 유치, 브랜드 강화, 리스크 감소로 연결하는 전략을 제공합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: ESG 현황 진단 (Materiality Assessment)

- **프레임워크**: [ESG 진단 가이드](frameworks/esg-assessment.md)
- E(환경): 탄소배출, 에너지 효율, 폐기물 관리
- S(사회): 인권, 노동, 다양성, 지역사회 기여
- G(거버넌스): 이사회 독립성, 윤리경영, 내부통제
- **이중 중요성(Double Materiality)** 평가: 재무적 영향 + 사회적 영향

### Step 2: 글로벌 규제 스캔

- **프레임워크**: [ESG 규제 매핑 가이드](frameworks/esg-regulations.md)
- **검색**: Tavily로 EU CSRD, EU Taxonomy, K-ESG, SEC 기후공시 최신 동향
- 규제 타임라인 매핑 (의무화 시점, 적용 범위)

### Step 3: 벤치마킹 (산업 Best Practice)

- 동종 업계 ESG 선도 기업 3곳 분석
- 평가 기관별 등급 비교 (KCGS, MSCI, CDP)
- **검색**: Exa로 ESG 우수 사례, 지속가능성 보고서 수집

### Step 4: 개선 전략 수립

| E (환경)         | S (사회)          | G (거버넌스)     |
| :--------------- | :---------------- | :--------------- |
| 탄소 감축 로드맵 | 인권 실사 체계    | 이사회 다양성    |
| 재생에너지 전환  | 공급망 노동 관리  | ESG 위원회 설치  |
| 순환경제 모델    | 지역사회 프로그램 | 반부패 체계 강화 |

### Step 5: 보고서 프레임워크 선택 + 작성 가이드

- GRI Standards (범용), SASB (산업별), TCFD (기후), ISSB (국제)
- 각 프레임워크의 요구 공시 항목 체크리스트

### Step 6: KPI 설정 + 이행 로드맵

- 단기(1년)/중기(3년)/장기(2050) 목표 설정
- 탄소중립 경로 (SBTi 기반)
- Greenwashing 방지 체크포인트

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                    | 활용 단계 |
| :--------- | :------------------------------------------- | :-------- |
| **Tavily** | EU CSRD, K-ESG, SEC 기후공시, 탄소 가격 동향 | Step 2    |
| **Exa**    | ESG 보고서 사례, 학술 연구, CDP 데이터       | Step 3, 5 |

## ✅ Quality Gates

### 반드시 포함

- [ ] **이중 중요성(Double Materiality)** 평가 수행
- [ ] 최소 **1개 이상** 글로벌 보고 표준 적용
- [ ] **정량적 KPI** (Scope 1/2/3 배출량 등) 포함
- [ ] 그린워싱 방지 **자체 검증 체크리스트** 적용

### 금지 사항

- ❌ 실적 없이 "탄소중립 선언" 권고 금지 (그린워싱)
- ❌ Scope 3 배출량 누락 금지
- ❌ 단기 비용만 강조하고 장기 가치 무시 금지

## 🤝 Collaboration Matrix

| 호출 에이전트 | 역할                    | 트리거 조건              |
| :------------ | :---------------------- | :----------------------- |
| **[Finance]** | ESG 투자 비용/수익 분석 | 재무적 영향 산정 시      |
| **[Legal]**   | 규제 준수 법적 검토     | Step 2 규제 해석 시      |
| **[SCM]**     | 공급망 ESG 리스크       | 공급망 ESG 진단 시       |
| **[PR]**      | ESG 커뮤니케이션        | 보고서 발간/대외 소통 시 |
| **[Data]**    | 탄소 배출량 데이터 분석 | KPI 산정 시              |
