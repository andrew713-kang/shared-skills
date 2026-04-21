# 기술 스택 선정 가이드 (Tech Stack Selection)

## 📌 선정 원칙

1. **문제 적합성 (Fitness for Purpose)**: "왜 이 기술인가?"에 대한 명확한 답이 있어야 함.
2. **생태계와 커뮤니티**: 문제 발생 시 해결책을 찾기 쉬운가? (StackOverflow, GitHub Stars)
3. **팀 숙련도**: 현재 팀원이 소화할 수 있는가? (Learning Curve)
4. **유지보수성**: 3년 뒤에도 이 코드를 읽고 고칠 수 있는가?

## 추천 스택 조합 (Best Practices)

### 1. 웹 애플리케이션 (SaaS/B2C)

| 계층         | 기술                | 선정 이유                                                   |
| :----------- | :------------------ | :---------------------------------------------------------- |
| **Frontend** | React (Next.js)     | SSR/SEO 강점, 압도적 생태계, Vercel 배포 용이               |
| **Styling**  | Tailwind CSS        | 빠른 개발 속도, 일관된 디자인 토큰, 적은 번들 사이즈        |
| **Backend**  | Node.js (NestJS)    | 프론트/백 언어 통일(TS), 모듈형 아키텍처, 엔터프라이즈 패턴 |
| **Database** | PostgreSQL          | 관계형 데이터의 표준, JSON 지원, 강력한 쿼리 기능           |
| **Auth**     | Supabase / NextAuth | 보안 구현 비용 절감, 소셜 로그인 통합 용이                  |

### 2. 고성능/대규모 트래픽 시스템

| 계층         | 기술             | 선정 이유                                               |
| :----------- | :--------------- | :------------------------------------------------------ |
| **Backend**  | Go (Golang)      | 뛰어난 동시성 처리(Goroutine), 빠른 컴파일, 적은 메모리 |
| **Database** | MySQL / MariaDB  | 읽기 중심 부하 분산(Replication) 용이                   |
| **Cache**    | Redis            | 인메모리 캐싱으로 DB 부하 감소                          |
| **Message**  | Kafka / RabbitMQ | 서비스 간 비동기 통신 및 결합도 감소                    |

### 3. 데이터 분석/AI 서비스

| 계층         | 기술                  | 선정 이유                                                |
| :----------- | :-------------------- | :------------------------------------------------------- |
| **Backend**  | Python (FastAPI)      | AI/ML 라이브러리(PyTorch, Pandas) 연동 최적, 비동기 지원 |
| **Database** | PostgreSQL (pgvector) | 벡터 검색 지원 (RAG 구현 용이)                           |
| **Serving**  | Docker / K8s          | 모델 배포 및 스케일링 관리 용이                          |

## 🚫 피해야 할 안티 패턴 (Anti-Patterns)

- **Hype Driven Development (HDD)**: 최신 유행이라서 도입 (예: 단순 앱에 MSA 도입)
- **Resume Driven Development**: 개발자 커리어를 위해 불필요하게 복잡한 기술 선정
- **Over-Engineering**: 미래의 불확실한 확장을 위해 현재 복잡도를 과도하게 높임
