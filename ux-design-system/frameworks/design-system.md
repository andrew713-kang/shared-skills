# 디자인 시스템 구축 가이드

## 개요

UI 컴포넌트와 디자인 토큰을 **체계적으로 관리**하는 시스템.
비유: LEGO 블록처럼 **표준화된 부품을 조합**하여 다양한 화면을 빠르게 만드는 것.

## 디자인 토큰 체계

### 1. 색상 (Color)

```
--color-primary: #...;       /* 주요 브랜드 색상 */
--color-secondary: #...;     /* 보조 색상 */
--color-success: #...;
--color-warning: #...;
--color-error: #...;
--color-bg-primary: #...;    /* 배경색 */
--color-text-primary: #...;  /* 텍스트 */
```

### 2. 타이포그래피 (Typography)

| 토큰        | 용도        | 크기     | 무게     |
| :---------- | :---------- | :------- | :------- |
| `heading-1` | 페이지 제목 | 2rem     | Bold     |
| `heading-2` | 섹션 제목   | 1.5rem   | SemiBold |
| `body`      | 본문        | 1rem     | Regular  |
| `caption`   | 보조 텍스트 | 0.875rem | Regular  |

### 3. 간격 (Spacing)

4px 기반 시스템: 4, 8, 12, 16, 24, 32, 48, 64, 96

### 4. 모서리 (Border Radius)

`none(0)`, `sm(4px)`, `md(8px)`, `lg(16px)`, `full(9999px)`

## 핵심 컴포넌트 목록

| 컴포넌트   | 변형(Variants)                                  | 접근성 요구               |
| :--------- | :---------------------------------------------- | :------------------------ |
| Button     | Primary/Secondary/Ghost/Danger + Size(sm/md/lg) | Focus ring, ARIA label    |
| Input      | Text/Password/Search/Textarea + Error state     | Label 연결, Error message |
| Card       | Default/Elevated/Outlined                       | Semantic HTML             |
| Modal      | Dialog/Alert/Drawer                             | Focus trap, ESC close     |
| Toast      | Success/Error/Warning/Info                      | Auto-dismiss, ARIA live   |
| Table      | Default/Striped/Sortable                        | Caption, scope 속성       |
| Navigation | Top/Side/Bottom/Breadcrumb                      | ARIA navigation           |

## 오픈 표준 우선 원칙

- **Radix UI**: 접근성 내장 헤드리스 컴포넌트
- **Shadcn UI**: 복사-붙여넣기 방식 컴포넌트
- **Lucide Icons**: 오픈소스 아이콘 라이브러리
- **CSS Custom Properties**: 프레임워크 비종속 토큰 관리
