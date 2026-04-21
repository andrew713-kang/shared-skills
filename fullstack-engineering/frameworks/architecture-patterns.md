# 아키텍처 패턴 가이드

## 1. 계층형 아키텍처 (Layered Architecture)

가장 보편적이고 시작하기 좋은 구조. 관심사의 분리(Separation of Concerns)가 핵심.

```mermaid
graph TD
    UI[Presentation Layer (Controller)] --> BL[Business Layer (Service)]
    BL --> DA[Data Access Layer (Repository)]
    DA --> DB[(Database)]
```

- **Controller**: 요청 수신, 유효성 검사, 응답 반환 (비즈니스 로직 ❌)
- **Service**: 핵심 비즈니스 로직, 트랜잭션 관리
- **Repository**: DB 제어, SQL/ORM 처리
- **Entity/Model**: 데이터 구조 정의

## 2. 클린 아키텍처 (Clean Architecture) / 헥사고날

비즈니스 로직을 외부(프레임워크, DB, UI)로부터 철저히 격리. 도메인 중심 설계(DDD)와 궁합이 좋음.

```mermaid
graph TD
    Web[Web Adapter] --> PortIn[Input Port]
    PortIn --> Domain[Domain Layer (Core)]
    Domain --> PortOut[Output Port]
    PortOut --> DBAdapter[DB Adapter]
    PortOut --> ExtAdapter[External API Adapter]
```

- **장점**: 프레임워크나 DB를 바꿔도 비즈니스 로직 수정 불필요. 테스트 용이.
- **단점**: 파일 수가 많아지고 초기 구현 복잡도 증가.

## 3. 마이크로서비스 아키텍처 (MSA)

시스템을 독립적으로 배포 가능한 작은 서비스 단위로 분할.

- **적합**: 50명 이상의 개발 조직, 도메인이 명확히 분리됨, 독립적 스케일링 필요
- **부적합**: 초기 스타트업, 트래픽이 적은 서비스 (모놀리식 우선 권장)
- **핵심 패턴**:
  - **API Gateway**: 진입점 단일화, 인증/인가 처리
  - **Circuit Breaker**: 장애 전파 차단
  - **Saga Pattern**: 분산 트랜잭션 처리

## 4. 서버리스 (Serverless)

서버 관리 없이 코드(함수) 단위로 실행. (AWS Lambda, Cloud Functions)

- **장점**: 유휴 비용 0, 무한 오토스케일링, 인프라 관리 불필요
- **단점**: Cold Start 지연, 벤더 종속성(Vendor Lock-in), 디버깅 어려움
