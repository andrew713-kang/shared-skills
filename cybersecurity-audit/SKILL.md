---
name: cybersecurity-audit
description: 사이버보안 위협 분석, 취약점 진단, 보안 아키텍처 설계 파이프라인. 보안 감사, 데이터 보호, 개인정보보호 요청 시 자동 트리거됩니다.
agents: [CISO, Backend]
trigger: 보안 감사, 취약점 점검, 개인정보보호, GDPR/PIPA, 침해사고 대응 요청 시
priority: high
---

# 🔒 Cybersecurity Audit Skill

## _Zero-Trust 기반 보안 진단 및 방어 전략 엔진_

## 📋 When to Apply (발동 조건)

- "보안 점검해줘", "취약점 분석해줘" 등 보안 관련 요청
- 신규 시스템/서비스 출시 전 보안 검토
- 개인정보보호법(PIPA) / GDPR 준수 점검
- 침해사고(Incident) 발생 시 대응 가이드
- 보안 아키텍처 설계 및 리뷰

## 🎯 Mission (핵심 목표)

**'사고가 터진 후'가 아닌 '사고가 터지기 전'에 방어 체계를 구축**합니다. 비용 대비 효과가 가장 높은 보안 투자를 우선순위로 제시합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 자산 현황 및 위협 모델링

- **프레임워크**: [위협 모델링 가이드](frameworks/threat-modeling.md)
- 핵심 자산 식별 (데이터, 시스템, 인프라)
- 위협 행위자 분류 (외부 공격자, 내부자, 국가급)
- STRIDE 모델 적용 (Spoofing, Tampering, Repudiation, Info Disclosure, DoS, Elevation)

### Step 2: 취약점 진단

- **프레임워크**: [취약점 진단 가이드](frameworks/vulnerability-assessment.md)
- OWASP Top 10 기준 웹 취약점 체크
- 인증/인가, 암호화, 입력 검증, 세션 관리
- **검색**: Tavily로 최신 CVE(공통 취약점), CISA 경고 수집

### Step 3: 컴플라이언스 갭 분석

- PIPA(개인정보보호법) 준수 체크리스트
- GDPR (EU 대상 서비스 시)
- ISMS-P 인증 요건 (필요 시)
- **검색**: Tavily로 최신 법규 개정, 과징금 사례

### Step 4: 보안 아키텍처 권고

| 영역        | 핵심 조치                 | 우선순위 |
| :---------- | :------------------------ | :------- |
| 인증        | MFA, SSO, 패스키          | Critical |
| 데이터 보호 | 암호화(전송/저장), 마스킹 | Critical |
| 네트워크    | WAF, VPN, 세그먼테이션    | High     |
| 모니터링    | SIEM, 이상행동 탐지       | High     |
| 접근제어    | RBAC, 최소권한 원칙       | Critical |
| 백업        | 3-2-1 규칙, 오프라인 백업 | High     |

### Step 5: 사고 대응 계획 (Incident Response Plan)

- 탐지 → 분류 → 격리 → 근절 → 복구 → 사후 분석
- 보고 의무 (24시간 내 KISA/개인정보보호위원회 통보)
- 커뮤니케이션 플랜 (내부/외부/고객/미디어)

### Step 6: 보안 로드맵 + 비용 추정

- Quick Win (30일), Short-term (90일), Long-term (1년)
- 각 조치별 예상 비용 및 리스크 감소 효과

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                              | 활용 단계 |
| :--------- | :----------------------------------------------------- | :-------- |
| **Tavily** | CVE DB, CISA 경고, 최신 사이버 공격 동향, 법규 개정    | Step 2, 3 |
| **Exa**    | 보안 아키텍처 논문, Zero-Trust 구현 사례, OWASP 가이드 | Step 4    |

## ✅ Quality Gates

### 반드시 포함

- [ ] **OWASP Top 10** 전체 항목 점검
- [ ] 발견된 취약점에 **CVSS 심각도 등급** 부여
- [ ] **법규 준수** 체크리스트 포함 (PIPA/GDPR)
- [ ] **사고 대응 계획** 반드시 포함

### 금지 사항

- ❌ "보안 위험 없음" 결론 금지 (모든 시스템에 리스크 존재)
- ❌ 구체적 공격 코드나 익스플로잇 제공 금지
- ❌ 비용만 강조하고 보안 투자 ROI 누락 금지

## 🤝 Collaboration Matrix

| 호출 에이전트 | 역할                      | 트리거 조건               |
| :------------ | :------------------------ | :------------------------ |
| **[Backend]** | 서버/인프라 기술 검토     | Step 2 기술적 취약점 진단 |
| **[Legal]**   | 법규 준수 해석            | Step 3 컴플라이언스 검토  |
| **[PR]**      | 사고 시 대외 커뮤니케이션 | Step 5 사고 대응 플랜     |
| **[Finance]** | 보안 투자 비용/효과       | Step 6 예산 산정          |
