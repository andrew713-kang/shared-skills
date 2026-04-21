# Skill Architecture Guide

## 개요

모든 에이전트 스킬은 **일관된 구조**를 가져야 합니다.
사용자가 어떤 에이전트를 호출하든 예상을 벗어나지 않는 **통일된 경험**을 제공하기 위함입니다.

## 1. 파일 구조 (File Structure)

```text
skills/
└── [skill-name]/
    ├── SKILL.md           # 스킬 정의서 (Main Entry)
    ├── frameworks/        # 사고 모델 및 가이드라인
    │   ├── [framework].md
    │   └── ...
    ├── templates/         # 결과물 양식
    │   ├── [template].md
    │   └── ...
    └── resources/         # 참고 자료 (데이터, 리스트)
        ├── [resource].md
        └── ...
```

## 2. SKILL.md 필수 구성 요소

### Frontmatter (YAML)

- `name`: 스킬 폴더명과 일치 (kebab-case)
- `description`: 한 줄 요약 (한글)
- `agents`: [주 에이전트, 보조 에이전트]
- `trigger`: 발동 키워드
- `priority`: critical / high / medium / low

### 본문 (Body)

1. **When to Apply**: 사용자가 언제 이 스킬을 호출해야 하는지 명시
2. **Mission**: 이 스킬이 해결해야 할 문제의 본질
3. **Analysis Chain (Step-by-Step)**: 사고의 흐름 (최소 3~6단계)
4. **AI Search Integration**: 외부 검색이 필요한 지점 명시
5. **Quality Gates**: 품질 보증 체크리스트 (5개 내외)
6. **Collaboration Matrix**: 타 에이전트와의 협업 포인트

## 3. Framework & Template 원칙

### Framework (사고 모델)

- "어떻게 생각해야 하는가?"를 가이드합니다.
- 단순 지식이 아닌 **구조화된 사고틀**을 제공합니다.
- 예: SWOT 분석, PESTEL, 디자인 씽킹 등

### Template (결과물 양식)

- "무엇을 만들어야 하는가?"를 정의합니다.
- 사용자가 바로 채워 넣을 수 있는 **빈칸(Placeholder)**을 포함합니다.
- 마크다운 표, 체크리스트 등을 적극 활용합니다.
