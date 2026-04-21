# API 설계 명세서 (API Specification)

**서비스명**: [서비스] | **버전**: v1.0 | **작성일**: [날짜]

## 1. 기본 원칙

- **Base URL**: `https://api.example.com/v1`
- **Content-Type**: `application/json`
- **인증 방식**: Bearer Token (JWT)
- **에러 응답**: RFC 7807 (Problem Details) 준수

## 2. 공통 응답 구조

```json
{
  "success": true, // 성공 여부
  "data": { ... }, // 실제 데이터
  "error": null    // 에러 발생 시 에러 객체
}
```

## 3. 엔드포인트 목록

### [GET] /users/{id}

- **설명**: 사용자 정보 조회
- **권한**: 본인 또는 관리자
- **요청 파라미터**:
  - `id` (path): 사용자 UUID
- **성공 응답 (200 OK)**:
  ```json
  {
    "id": "uuid",
    "email": "user@example.com",
    "name": "홍길동"
  }
  ```
- **에러 응답**:
  - `401 Unauthorized`: 토큰 없음/만료
  - `403 Forbidden`: 권한 없음
  - `404 Not Found`: 사용자 없음

### [POST] /users

- **설명**: 회원 가입
- **요청 바디**:
  ```json
  {
    "email": "user@example.com",
    "password": "strongPassword123!",
    "name": "홍길동"
  }
  ```
- **성공 응답 (201 Created)**:
  ```json
  {
    "id": "uuid"
  }
  ```

## 4. 상태 코드 (Standard Status Codes)

| 코드 | 의미                  | 사용 예시             |
| :--- | :-------------------- | :-------------------- |
| 200  | OK                    | 조회/수정 성공        |
| 201  | Created               | 생성 성공             |
| 204  | No Content            | 삭제 성공 (바디 없음) |
| 400  | Bad Request           | 입력값 검증 실패      |
| 401  | Unauthorized          | 인증 실패             |
| 403  | Forbidden             | 권한 없음             |
| 404  | Not Found             | 리소스 없음           |
| 500  | Internal Server Error | 서버 내부 오류        |
