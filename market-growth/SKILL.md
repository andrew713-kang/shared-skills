---
name: market-growth
description: TAM/SAM/SOM 시장 규모 산정, STP 분석, AARRR 그로스 해킹까지 시장 공략 전체 파이프라인. 시장 분석/마케팅 전략/Go-To-Market 요청 시 자동 트리거됩니다.
agents: [Market, Ideator, CRM]
trigger: 시장 분석, 고객 분석, GTM 전략, 그로스 해킹, 시장 규모 산정, 포지셔닝 요청 시
priority: critical
---

# 📈 Market Growth Skill

## _정교한 시장 공략 및 그로스 해킹 엔진_

## 📋 When to Apply (발동 조건)

- "시장 분석해줘", "타겟 고객이 누구야?" 등 시장/고객 관련 요청
- Go-To-Market(GTM) 전략 수립
- 시장 규모(TAM/SAM/SOM) 산정
- 고객 세그먼트 정의 및 페르소나 설계
- 성장 지표(AARRR) 기반 그로스 실험 설계

## 🎯 Mission (핵심 목표)

**데이터 기반으로 최적의 타겟 시장을 선정**하고, 고객 여정을 설계하여, 첫 90일 이내 실행 가능한 성장 전략을 제공합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: TAM/SAM/SOM 시장 규모 산정

- **프레임워크**: [TAM/SAM/SOM 가이드](frameworks/tam-sam-som.md)
- **TAM** (전체 시장): Top-Down 방식 (산업 리포트 기반)
- **SAM** (유효 시장): 지역/업종/기술 등으로 필터링
- **SOM** (획득 가능 시장): 현실적 점유율 기반 산정
- **검색**: Tavily로 산업 리포트, 시장 규모 데이터 조회

### Step 2: STP 분석

- **프레임워크**: [STP 분석 가이드](frameworks/stp-analysis.md)
- **S**egmentation: 고객을 의미 있는 그룹으로 세분화 (인구통계/행동/심리)
- **T**argeting: 가장 매력적인 세그먼트 선택 (규모 × 성장성 × 접근성)
- **P**ositioning: 타겟 고객의 마음속에 잡을 포지션 정의

### Step 3: 고객 페르소나 & Journey Mapping

- AISAS 모델 (Attention → Interest → Search → Action → Share)
- 페르소나 최소 2종 정의 (Early Adopter + Mainstream)
- Pain Point → Gain Point → Job-to-be-Done 매핑

### Step 4: 경쟁 포지셔닝 맵 (Perceptual Map)

- X축/Y축 기준 설정 (예: 가격 vs 품질, 편의성 vs 전문성)
- 경쟁사 3~5곳 + 자사 포지셔닝
- **검색**: Exa로 경쟁사 제품/서비스 상세 정보 수집

### Step 5: Growth 실험 설계 (AARRR Pirate Metrics)

- **프레임워크**: [AARRR 가이드](frameworks/aarrr-metrics.md)
- **A**cquisition (획득): 첫 유입 채널 전략
- **A**ctivation (활성화): 첫 "아하!" 모먼트 설계
- **R**etention (유지): 재방문/재사용 메커니즘
- **R**evenue (수익화): 과금 모델 & 가격 전략
- **R**eferral (추천): 바이럴/입소문 구조 설계

### Step 6: Go-To-Market 전략서 + 90일 Playbook

- 채널 믹스 (온라인/오프라인/파트너십)
- 핵심 KPI 설정 (CAC, LTV, Payback Period)
- 첫 90일 스프린트 계획

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                         | 활용 단계 |
| :--------- | :------------------------------------------------ | :-------- |
| **Tavily** | 산업 리포트, 시장 규모 데이터, 소비자 트렌드 뉴스 | Step 1, 3 |
| **Exa**    | 혁신적 GTM 성공 사례, 경쟁사 상세 분석 자료       | Step 4, 5 |

## ✅ Quality Gates

### 반드시 포함

- [ ] 시장 규모 산정에 **공신력 있는 리서치** 데이터 인용
- [ ] 고객 페르소나 최소 **2종** 정의
- [ ] 첫 **90일 실행 로드맵** 포함
- [ ] 모든 채널 전략에 **예상 CAC/LTV** 수치 포함

### 금지 사항

- ❌ "경쟁사 없다" 주장 금지 (간접 경쟁자 분석 필수)
- ❌ 검증되지 않은 시장 규모 수치 인용 금지
- ❌ 고객 니즈를 가정만으로 정의 금지 (데이터 근거 필수)

## 📄 Output Template

### Go-To-Market 전략서

1. **시장 기회 요약**: TAM/SAM/SOM + 핵심 성장 드라이버
2. **타겟 고객 프로필**: 페르소나 카드 (이름/나이/직업/Pain/Gain/JTBD)
3. **포지셔닝 선언문**: "We are the [카테고리] for [타겟] who [니즈]"
4. **채널 전략 매트릭스**: 채널별 예상 CAC/LTV/ROI
5. **90일 Growth Playbook**: 주차별 실험 → 측정 → 학습 사이클

## 🤝 Collaboration Matrix

| 호출 에이전트     | 역할                  | 트리거 조건                    |
| :---------------- | :-------------------- | :----------------------------- |
| **[Marketing]**   | 디지털 채널 실행 전략 | Step 5에서 채널 믹스 구체화 시 |
| **[Storyteller]** | 브랜드 서사 설계      | 포지셔닝 선언문 및 메시지 설계 |
| **[Data]**        | 시장 데이터 분석      | TAM/SAM/SOM 정량 산정 시       |
| **[Designer]**    | 고객 경험(CX) 설계    | 페르소나 기반 UX 전략 연결     |
| **[Global]**      | 해외 시장 인사이트    | GTM이 글로벌 진출 포함 시      |
