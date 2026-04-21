---
name: office-productivity-mastery
description: PPT 제안서, 엑셀 재무 모델, 워드 계약서 작성을 자동화하고 표준화하는 오피스 실무 마스터 스킬. 문서 작성, 데이터 시각화, 보고서 편집 요청 시 자동 트리거됩니다.
agents: [Consultant, Data, Storyteller, Coder, Critic]
trigger: PPT 제작, 엑셀 분석, 보고서 작성, 계약서 검토, 데이터 시각화 요청 시
priority: high
---

# 📄 Office Productivity Mastery Skill (S.A.S. 2.0)

## _맥킨지급 비즈니스 문서 자동화 및 표준화 엔진_

## 📋 When to Apply (발동 조건)

- "투자 제안서 PPT 만들어줘", "재무 엑셀 모델 짜줘" 요청
- 복잡한 데이터의 시각화 (차트, 그래프)
- 계약서/보고서의 스타일링 및 서식 표준화
- 엑셀 매크로(VBA) 및 구글 스프레드시트 앱스스크립트 작성
- **[NEW] 실제 .pptx, .xlsx 파일 생성 요청 시 (Python 활용)**

## 🎯 Mission (핵심 목표)

**"문서 작업 시간을 1/10로 단축"**합니다. 내용은 AI가 채우고, 형식은 전문가 수준으로 자동 보정하여 **'즉시 보고 가능한(Ready-to-report)'** 결과물을 만듭니다.
단순 텍스트 제안을 넘어, **Python 코드를 통해 실제 다운로드 가능한 파일**을 생성합니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 문서 목적 및 청중 분석

- **To Whom**: 보고 대상 (경영진 vs 실무진 vs 외부 고객)
- **Objective**: 설득(Persuade) vs 정보 전달(Inform) vs 승인 요청(Approve)
- **Format**: PPT(발표용) vs Word(읽기용) vs Excel(분석용)

### Step 2: 구조 설계 (Storyline)

- **프레임워크**: [SCQA 구조 가이드](frameworks/scqa-structure.md)
- 장표별 핵심 메시지 (Lead Message) 추출
- 논리 흐름 (Pyramid Principle) 설계

### Step 3-A: PowerPoint (비주얼 스토리텔링)

- **프레임워크**: [컨설팅 장표 표준](frameworks/consulting-slides.md)
- 텍스트 → 도해(Diagram) 변환 프롬프트
- 차트 추천 (비교, 추이, 비중, 상관관계)
- 슬라이드 마스터 및 레이아웃 가이드

### Step 3-B: Excel (데이터 모델링)

- **프레임워크**: [재무 모델링 표준](frameworks/excel-modeling.md)
- 입력(Input) / 계산(Calc) / 출력(Output) 시트 분리
- 오류 방지 (Data Validation, IFERROR)
- 피벗 테이블 및 동적 차트 설계

### Step 3-C: Code-First Generation (Python Automation)

- **PowerPoint**: `python-pptx` 라이브러리를 사용하여 슬라이드, 텍스트 상자, 차트를 코드로 생성.
- **Excel**: `pandas` 및 `openpyxl`/`xlsxwriter`를 사용하여 데이터프레임을 엑셀로 변환하고 서식 적용.
- **Word**: `python-docx`를 사용하여 보고서 및 계약서 자동 생성.
- **Code Execution**: 작성된 Python 코드를 실행하여 실제 파일 생성 (.pptx, .xlsx, .docx).

### Step 4: 매크로 & 자동화 스크립트

- 반복 작업 자동화를 위한 VBA / Apps Script 코드 생성
- 데이터 정제 (Data Cleansing) 스크립트
- 자동 보고서 생성 (Excel to PPT) 로직

### Step 5: Red Team Review (Devil's Advocate)

- **Agent**: **[Critic]**
- **Action**: 작성된 문서/코드의 논리적 결함, 데이터 오류, 비주얼 가독성을 비판적으로 검토.
- **Guide**: [Red Teaming Framework](../agent-architect/frameworks/red-teaming.md) 적용.
- **Check**: "이 제안서가 경영진에게 까일 이유는 무엇인가?"

### Step 6: 최종 검수 (Review)

- 오탈자 및 스타일 일관성 체크
- 수식 정확성 검증 (Cross-check)
- 모바일/인쇄 가독성 확인

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                            | 활용 단계 |
| :--------- | :--------------------------------------------------- | :-------- |
| **Exa**    | 최신 비즈니스 인포그래픽 트렌드, 엑셀 함수 최적화 팁 | Step 3, 4 |
| **Tavily** | 산업별 표준 계약서 서식, 최신 보고서 양식 벤치마킹   | Step 2    |

## ✅ Quality Gates

### 반드시 포함

- [ ] **Lead Message**: 모든 장표 상단에 핵심 요약 한 문장 포함
- [ ] **MECE**: 누락이나 중복 없는 목차 구조
- [ ] **Source**: 모든 데이터의 출처 표기
- [ ] **단축키 가이드**: 사용자를 위한 작업 효율 팁 제공
- [ ] **Red Team Pass**: 치명적인 논리적 결함이 없음을 [Critic]이 승인했는가?

### 금지 사항

- ❌ "알아서 하세요" 식의 모호한 서식 금지 (표준 템플릿 준수)
- ❌ 하드코딩된 엑셀 수식 금지 (참조 활용)
- ❌ 읽을 수 없는 고밀도 텍스트 슬라이드 금지
- ❌ 실행 불가능한 "가상의" Python 코드 제공 금지 (반드시 검증)

## 🤝 Collaboration Matrix

| 호출 에이전트     | 역할                             | 트리거 조건               |
| :---------------- | :------------------------------- | :------------------------ |
| **[Coder]**       | Python 스크립트 작성 및 실행     | 파일 생성 요청 시         |
| **[Critic]**      | 결과물에 대한 비판적 검증        | 최종 전달 전 항상         |
| **[Designer]**    | PPT 디자인 테마 및 아이콘셋 제공 | Step 3-A 디자인 시        |
| **[Data]**        | 엑셀 데이터 분석 및 정제         | Step 3-B 데이터 처리 시   |
| **[Storyteller]** | 보고서 워딩 및 헤드라인 작성     | Step 2 스토리라인 설계 시 |
