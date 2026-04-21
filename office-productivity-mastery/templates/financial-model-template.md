# Excel Financial Model Template

## 1. Assumptions (가정)

| 항목                | 단위 | Year 1 | Year 2 | Year 3 | 비고 |
| :------------------ | :--- | :----- | :----- | :----- | :--- |
| **Revenue Drivers** |      |        |        |        |      |
| 가격 (Price)        | KRW  | [입력] | [입력] | [입력] |      |
| 판매량 (Volume)     | EA   | [입력] | [입력] | [입력] |      |
| 성장률 (Growth)     | %    | [입력] | [입력] | [입력] |      |
| **Cost Drivers**    |      |        |        |        |      |
| 원가율 (COGS %)     | %    | [입력] | [입력] | [입력] |      |
| 판관비율 (SG&A %)   | %    | [입력] | [입력] | [입력] |      |

## 2. Income Statement (추정 손익계산서)

| 항목                            | Year 1    | Year 2    | Year 3    | 수식 로직    |
| :------------------------------ | :-------- | :-------- | :-------- | :----------- |
| **Revenue (매출)**              | [Formula] | [Formula] | [Formula] | P \* Q       |
| **COGS (매출원가)**             | [Formula] | [Formula] | [Formula] | Rev \* COGS% |
| **Gross Profit (매출이익)**     | [Formula] | [Formula] | [Formula] | Rev - COGS   |
| **SG&A (판관비)**               | [Formula] | [Formula] | [Formula] | Rev \* SG&A% |
| **Operating Profit (영업이익)** | [Formula] | [Formula] | [Formula] | GP - SG&A    |
| _Margin (%)_                    | [Formula] | [Formula] | [Formula] | OP / Rev     |

## 3. Key Metrics (핵심 지표)

- **CAGR (연평균 성장률)**: [수식]
- **BEP (손익분기점)**: [수식]
