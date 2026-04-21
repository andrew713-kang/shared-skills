---
name: creative-production-studio
description: 유튜브 대본, 숏폼 기획, SNS 마케팅 디자인, 영상 프롬프트를 생성하는 크리에이티브 제작 공장. 영상 제작, 디자인 기획, 콘텐츠 생성 요청 시 자동 트리거됩니다.
agents: [Producer, Designer, Marketing]
trigger: 영상 대본, 유튜브 기획, 썸네일, 카드뉴스, 디자인 요청, 영상 프롬프트
priority: high
---

# 🎬 Creative Production Studio Skill

## _멀티미디어 콘텐츠 기획 및 제작 AI 스튜디오_

## 📋 When to Apply (발동 조건)

- "유튜브 영상 대본 써줘", "쇼츠 아이디어 줘" 요청
- AI 영상 생성 도구(Sora, Runway, Pika)용 프롬프트 작성
- SNS 카드뉴스, 배너 광고, 상세페이지 기획
- 브랜드 홍보 영상 스토리보드 작성

## 🎯 Mission (핵심 목표)

**"텍스트를 시각적 경험으로 변환"**합니다. 단순한 글을 넘어, 카메라 앵글, 조명, 사운드, 디자인 레이아웃까지 지시하여 **'제작 가능한(Ready-to-produce)'** 결과물을 만듭니다.

## 🔗 Analysis Chain (분석 파이프라인)

### Step 1: 포맷 및 타겟 설정

- **Platform**: 유튜브(롱폼) vs 틱톡/쇼츠(숏폼) vs 인스타(이미지)
- **Target Emotion**: 재미, 감동, 정보, 충격, 공감
- **Hook Strategy**: 초반 3초 이탈 방지 전략

### Step 2: 스토리보드 & 스크립트

- **프레임워크**: [영상 기획 표준](frameworks/video-storyboard.md)
- **Scene**: 장면 번호 및 길이 (Duration)
- **Visual**: 화면 묘사 (앵글, 피사체, 움직임)
- **Audio**: 대사(Script), 나레이션(VO), 효과음(SFX), 배경음악(BGM)

### Step 3: AI 프롬프트 엔지니어링 (Video/Image)

- 미드저니(Midjourney) / 스테이블 디퓨전(SD) 이미지 프롬프트
- 런웨이(Runway) / 피카(Pika) 모션 브러시 프롬프트
- **파라미터**: 조명(Cinematic lighting), 스타일(Photorealistic), 비율(--ar 16:9)

### Step 4: 디자인 레이아웃 (SNS/Web)

- **프레임워크**: [전환 유도 디자인](frameworks/conversion-design.md)
- 헤드라인 배치, 시선 유도(Z-pattern, F-pattern)
- 컬러 팔레트 및 타이포그래피 가이드
- CTA(Call To Action) 버튼 디자인

### Step 5: 바이럴 요소 점검

- 썸네일 클릭률(CTR) 예측
- 공유 유발 요인(Shareability) 체크
- 트렌드 키워드 해시태그 추출

## 🔍 AI Search Integration

| 검색 엔진  | 검색 대상                                         | 활용 단계 |
| :--------- | :------------------------------------------------ | :-------- |
| **Exa**    | 바이럴 영상 레퍼런스, 최신 디자인 트렌드(Behance) | Step 1, 4 |
| **Tavily** | 유행하는 밈(Meme), 인기 챌린지, 배경음악 트렌드   | Step 1, 5 |

## ✅ Quality Gates

### 반드시 포함

- [ ] **Hook**: 시작 3초 내에 시청자를 사로잡는 장치 필수
- [ ] **CTA**: 영상/디자인 끝에 명확한 행동 유도(구독, 구매) 포함
- [ ] **Visual Detail**: 프롬프트 생성 시 조명, 카메라 앵글, 스타일 명시
- [ ] **Platform Fit**: 각 플랫폼(유튜브/인스타) 규격 및 알고리즘 최적화

### 금지 사항

- ❌ "재미있게 만들어줘" 식의 추상적 지시 금지 (구체적 연출 필요)
- ❌ 저작권 위반 소지가 있는 음원/이미지 사용 요청 금지
- ❌ 텍스트로만 가득 찬 지루한 영상 기획 금지

## 🤝 Collaboration Matrix

| 호출 에이전트     | 역할                              | 트리거 조건             |
| :---------------- | :-------------------------------- | :---------------------- |
| **[Storyteller]** | 대사 및 나레이션 윤문             | Step 2 스크립트 작성 시 |
| **[Marketing]**   | 타겟 오디언스 분석 및 키워드 제공 | Step 1 기획 시          |
| **[Legal]**       | 저작권 및 초상권 리스크 체크      | Step 5 검수 시          |
