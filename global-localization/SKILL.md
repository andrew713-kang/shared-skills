---
name: global-localization
description: 국가별 시장 진입 전략, 현지화(L10n) 가이드, 글로벌 규제 체크를 수행하는 해외 진출 전문 스킬. 해외 진출, 번역, 현지화, 글로벌 마케팅 요청 시 자동 트리거됩니다.
agents: [Global, Translator, Legal]
trigger: 해외 진출, 글로벌 마케팅, 앱 현지화, 다국어 번역, 해외 규제
priority: high
---

# 🌏 Global Expansion & Localization Skill

## _실패 없는 글로벌 시장 진입 및 현지화 전략_

## 📋 When to Apply (발동 조건)

- "미국 시장 진출 전략 짜줘", "일본 런칭 준비해줘" 요청
- 서비스/제품의 다국어 번역 및 L10n(현지화) 작업
- 해외 현지 법인 설립 및 파트너 발굴
- GDPR, CCPA 등 글로벌 규제 준수 여부 확인

## 🎯 Mission (핵심 목표)

**"언어의 장벽을 넘어 문화(Culture)에 스며듭니다."** 단순 번역을 넘어, 해당 국가의 문화, 법규, 사용자 습관에 완벽히 맞춘 **Total Localization**을 수행하여 리스크를 최소화하고 성공 확률을 높입니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 시장 적합성 평가 (Market Fit)

- **Target Market**: 진출 국가의 시장 규모 및 성장성 (TAM/SAM/SOM)
- **Competitor**: 현지 경쟁사 및 글로벌 플레이어 분석
- **Cultural Nuance**: 문화적 금기 사항, 선호 색상/숫자, 라이프스타일

### Step 2: 진입 전략 수립 (Entry Strategy)

- **프레임워크**: [글로벌 진입 모드](frameworks/entry-mode.md)
- **Mode**: 수출 vs 라이선싱 vs 조인트벤처(JV) vs 직접투자(FDI)
- **Channel**: 현지 유통망 및 파트너사 발굴 (총판, 에이전시)

### Step 3: 현지화 가이드 (Localization - L10n)

- **프레임워크**: [L10n 체크리스트](frameworks/l10n-checklist.md)
- **Language**: 전문 번역가 수준의 자연스러운 현지어 변환
- **Currency/Unit**: 화폐, 단위(ft/m), 날짜 표기법, 주소 체계 변환
- **UI/UX**: 우횡서(RTL) 지원, 텍스트 길이 변화에 따른 레이아웃 대응

### Step 4: 규제 및 법률 검토 (Compliance)

- **프레임워크**: [글로벌 규제 맵](frameworks/global-compliance.md)
- **Data Privacy**: GDPR(유럽), CCPA(캘리포니아), PIPA(한국/일본)
- **Tax/Legal**: 현지 세무 이슈, 법인세, 고용 노동법

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                        | 활용 단계 |
| :--------- | :----------------------------------------------- | :-------- |
| **Exa**    | 현지 소비자 반응(SNS), 경쟁사 현지화 전략 사례   | Step 1, 3 |
| **Tavily** | 국가별 최신 무역 규제, 법률 변동 사항, 관세 정보 | Step 2, 4 |

## ✅ Quality Gates

### 반드시 포함

- [ ] **Cultural Check**: 문화적으로 민감한 표현이나 이미지 금지 여부 확인
- [ ] **Native Review**: 현지인이 보기에 어색함이 없는 자연스러운 표현 사용
- [ ] **Regulation**: 필수 인증(CE, FDA 등) 및 개인정보 처리 방침 확인

### 금지 사항

- ❌ 기계적인 직역(Literal Translation) 금지
- ❌ 특정 국가의 정치, 종교적 이슈를 자극하는 콘텐츠 포함 금지
- ❌ 현지 결제 시스템(Visa, WeChat, Line Pay 등) 고려 없는 UX 설계 금지

## 🤝 Collaboration Matrix

| 호출 에이전트    | 역할                                | 트리거 조건         |
| :--------------- | :---------------------------------- | :------------------ |
| **[Translator]** | 다국어 번역 및 감수                 | Step 3 현지화 시    |
| **[Legal]**      | 국가별 법률 리스크 검토             | Step 4 규제 확인 시 |
| **[Marketing]**  | 현지 마케팅 채널 및 인플루언서 전략 | Step 2 진입 전략 시 |
