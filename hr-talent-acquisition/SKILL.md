---
name: hr-talent-acquisition
description: A급 인재 채용 공고(JD), 역량 면접 질문, 온보딩 로드맵을 설계하는 HR 전문 스킬. 채용, 면접, 조직문화, 인사 평가 요청 시 자동 트리거됩니다.
agents: [HR, Coach, Culture]
trigger: 채용 공고 작성, 면접 질문 생성, 온보딩 계획, 조직문화 설계
priority: high
---

# 🫂 HR & Talent Acquisition Skill

## _Top-tier 인재 영입 및 조직 문화 설계 엔진_

## 📋 When to Apply (발동 조건)

- "개발자 채용 공고(JD) 써줘", "임원 면접 질문 뽑아줘" 요청
- 신규 입사자 온보딩 프로그램 기획
- 핵심 인재(Key Talent) 유지 및 보상 설계
- 조직 문화 진단 및 개선안 도출

## 🎯 Mission (핵심 목표)

**"최고의 인재를 알아보고, 데려오고, 남게 합니다."** 단순한 공고 작성이 아니라, 우리 회사의 매력을 극대화하여 **A급 인재가 지원하게 만드는 전략(Attraction Strategy)**을 실행합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 직무 정의 및 페르소나 (Role Definition)

- **Role**: 수행해야 할 핵심 R&R (책임과 역할)
- **Persona**: 필요한 역량(Skill), 태도(Attitude), 경험(Experience)
- **Employee Value Proposition (EVP)**: 왜 이 회사가 이 사람에게 매력적인가?

### Step 2: 매력적인 채용 공고 (Killer JD)

- **프레임워크**: [A급 인재를 부르는 JD](frameworks/killer-jd.md)
- **Headline**: 가슴 뛰게 하는 미션 중심의 헤드라인
- **Description**: 도전적인 과제와 성장 기회 강조
- **Requirement**: 필수 자격 요건과 우대 사항의 명확한 구분

### Step 3: 구조화된 면접 설계 (Structured Interview)

- **프레임워크**: [BEI 역량 면접](frameworks/interview-guide.md)
- **Questions**: 과거 행동 기반 질문(BEI) 및 상황 면접 질문
- **Evaluation Criteria**: 평가 기준표(Rubric) 및 합불 가이드
- **Culture Fit**: 조직 적합성 검증 질문

### Step 4: 온보딩 로드맵 (Onboarding)

- **프레임워크**: [90일 정착 로드맵](frameworks/onboarding-roadmap.md)
- 입사 첫 날(Day 1) 경험 설계 (웰컴 키트, 장비 세팅)
- 첫 달(Month 1) 핵심 과제 및 멘토링
- 3개월(Month 3) 수습 통과 기준 설정

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                               | 활용 단계 |
| :--------- | :------------------------------------------------------ | :-------- |
| **Exa**    | 경쟁사 채용 공고(JD), 직무별 연봉 테이블(Levels.fyi 등) | Step 1, 2 |
| **Tavily** | 최신 HR 트렌드, 입사자가 선호하는 복지 혜택             | Step 1, 4 |

## ✅ Quality Gates

### 반드시 포함

- [ ] **Challenge**: 단순 업무 나열이 아닌 '해결해야 할 과제' 명시
- [ ] **Growth**: 이 직무를 통해 얻을 수 있는 경력 성장 기회 포함
- [ ] **Scoring**: 면접 질문별 구체적인 평가 기준(상/중/하) 제시

### 금지 사항

- ❌ "열정적인 분, 가족 같은 분위기" 등 상투적인 표현 금지
- ❌ 차별적 요소(성별, 나이, 종교 등)가 포함된 문구 금지
- ❌ 실현 불가능하거나 과장된 혜택 제시 금지

## 🤝 Collaboration Matrix

| 호출 에이전트 | 역할                                    | 트리거 조건         |
| :------------ | :-------------------------------------- | :------------------ |
| **[Coach]**   | 면접관 교육 및 리더십 코칭              | Step 3 면접 준비 시 |
| **[Culture]** | 조직 문화 적합성(Culture Fit) 기준 제공 | Step 1 EVP 도출 시  |
| **[Legal]**   | 근로계약서 및 노무 리스크 검토          | 채용 확정 시        |
