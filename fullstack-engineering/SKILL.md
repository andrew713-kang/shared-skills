---
name: fullstack-engineering
description: 프론트엔드/백엔드/인프라를 아우르는 풀스택 개발 파이프라인. 아키텍처 설계, 코드 품질, CI/CD, 배포까지 소프트웨어 엔지니어링 전체를 다룹니다.
agents: [Frontend, Backend, Coder, Builder, QA]
trigger: 개발, 코딩, 아키텍처 설계, API, 데이터베이스, 배포, 테스트 요청 시
priority: high
---

# 💻 Fullstack Engineering Skill

## _엔터프라이즈급 풀스택 개발 및 DevOps 엔진_

## 📋 When to Apply (발동 조건)

- "웹앱 만들어줘", "API 설계해줘" 등 개발 관련 요청
- 시스템 아키텍처 설계 및 기술 스택 선정
- 프론트엔드/백엔드 코드 작성 및 리팩토링
- 데이터베이스 설계 및 최적화
- CI/CD 파이프라인 구축 및 배포

## 🎯 Mission (핵심 목표)

**읽기 쉽고, 테스트 가능하고, 확장 가능한 코드**를 작성합니다. "돌아가는 코드"를 넘어 "누구나 유지보수할 수 있는 클린 코드"를 지향합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 요구사항 분석 & 기술 스택 선정

- **프레임워크**: [기술 스택 선정 가이드](frameworks/tech-stack.md)
- 기능 요구사항(FR) / 비기능 요구사항(NFR) 정리
- 기술 스택 비교 평가 (성능, 생태계, 학습 곡선, 비용)
- **검색**: Exa로 최신 기술 동향, 라이브러리 비교 리뷰

### Step 2: 아키텍처 설계

- **프레임워크**: [아키텍처 패턴 가이드](frameworks/architecture-patterns.md)
- 시스템 구조도 (컴포넌트 다이어그램)
- API 설계 (REST/GraphQL, 엔드포인트 정의)
- 데이터 모델링 (ERD, 스키마 설계)
- 인증/인가 구조 (JWT, OAuth, 세션)

### Step 3: 프론트엔드 개발

- 컴포넌트 구조 설계 (Atomic Design)
- 상태 관리 전략 (React Context / Zustand / Redux)
- 성능 최적화 (Code Splitting, Lazy Loading, Memoization)
- 반응형 레이아웃 & 접근성
- **오픈 표준 우선**: Radix UI, Shadcn, Lucide Icons

### Step 4: 백엔드 개발

- API 구현 (입력 검증, 에러 핸들링, 로깅)
- 데이터베이스 CRUD + 쿼리 최적화
- 인증/인가 미들웨어
- 추상화 레이어 (DB 교체 용이한 Repository 패턴)
- 환경 설정 분리 (`src/config/`, `.env`)

### Step 5: 테스팅 & 품질 보증

- 단위 테스트 (핵심 비즈니스 로직)
- 통합 테스트 (API 엔드포인트)
- E2E 테스트 (핵심 사용자 시나리오)
- 코드 리뷰 체크리스트

### Step 6: CI/CD & 배포

- 배포 파이프라인 설계 (Build → Test → Deploy)
- 배포 옵션 비교: Vercel / Netlify / Cloud Run / AWS
- 모니터링 & 로깅 체계
- 롤백 전략

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                        | 활용 단계 |
| :--------- | :----------------------------------------------- | :-------- |
| **Exa**    | 라이브러리 비교, 기술 블로그, 아키텍처 패턴 논문 | Step 1, 2 |
| **Tavily** | CVE 취약점, 패키지 업데이트, 최신 개발 도구      | Step 4, 6 |

## ✅ Quality Gates

### 반드시 포함

- [ ] **코드 주석**은 '왜(Why)' 설명 (What이 아님)
- [ ] **추상화 레이어** 적용 (DB 교체 용이)
- [ ] **환경 설정** 분리 (`src/config/`, `.env`)
- [ ] **핵심 로직** 단위 테스트 커버리지 80%+
- [ ] **보안**: OWASP Top 10 기본 방어 적용

### 금지 사항

- ❌ API 키 코드 내 하드코딩 금지
- ❌ 에러 무시 (catch 블록 비우기) 금지
- ❌ 플랫폼 종속 코드 금지 (추상화 필수)
- ❌ 테스트 없이 프로덕션 배포 금지

## 🤝 Collaboration Matrix

| 호출 에이전트    | 역할                      | 트리거 조건              |
| :--------------- | :------------------------ | :----------------------- |
| **[Designer]**   | UI 디자인 → 컴포넌트 구현 | Step 3 프론트 개발 시    |
| **[CISO]**       | 보안 리뷰                 | Step 4 인증/인가 구현 시 |
| **[IT-Planner]** | 요구사항 정제             | Step 1 요구사항 분석 시  |
| **[PMO]**        | 일정 관리, 스프린트 계획  | 전체 개발 프로세스       |
