# 재무 모델링 표준 (Financial Modeling Standards)

## 개요

오류가 없고(Error-free), 수정이 쉬우며(Flexible), 누구나 이해할 수 있는(Readable) 엑셀 모델링 규칙입니다.
FAST(Flexible, Appropriate, Structured, Transparent) 표준을 기반으로 합니다.

## 1. 시트 구조 (Worksheet Structure)

하나의 시트에 모든 것을 넣지 말고, **역할별로 시트를 분리**하십시오.

1. **Cover**: 모델 개요, 버전, 작성자, 목차
2. **Inputs (Assumption)**: 모든 가정치(가격, 성장률, 원가율 등)를 입력하는 곳
   - _규칙_: 하드코딩(숫자 직접 입력)은 오직 이 시트에서만 허용!
3. **Calcs (Engine)**: 실제 계산이 일어나는 곳
   - _규칙_: 이 시트에는 숫자 입력 금지. 오직 수식(Formula)만 존재해야 함.
4. **Outputs (Dashboard)**: 결과물을 요약하여 보여주는 곳 (차트, 요약표)

## 2. 서식 코딩 (Formatting Codes)

색상을 통해 셀의 성격을 구분하십시오.

- **파란색 글씨 (Blue)**: 하드코딩된 숫자 (입력값) → _수정 가능_
- **검은색 글씨 (Black)**: 수식 (Formula) → _수정 금지_
- **초록색 글씨 (Green)**: 다른 시트 참조 (Link)
- **빨간색 글씨 (Red)**: 오류 또는 중요 체크 포인트

## 3. Best Practices

- **단일 행 수식 (Single Row Formula)**: 같은 행의 수식은 끝까지 동일해야 함. 중간에 수식 바꾸지 말 것.
- **복잡한 수식 분해**: `IF` 문이 3중 이상 중첩되면 별도 계산 열(Helper Column)을 만들어 쪼갤 것.
- **오류 체크 (Error Check)**: 합계 검증(Balance Check) 라인을 만들어 `Assets - Liabilities - Equity = 0`인지 항상 확인.
