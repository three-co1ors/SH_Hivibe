# 🤖 HiVibe — AI 기반 코드 분석 및 학습 웹 플랫폼 (진행 중)

## Hi, your code. High, your vibe.

> HiVibe는 사용자가 작성한 코드를 AI가 분석하고, 더 나은 방향을 제안하는 학습형 코드 분석 플랫폼입니다.

<br>

<img src="https://img.shields.io/badge/Java_21-0087c1?style=flat-square&logoColor=white"/> <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white"/> <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white"/> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white"/> <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white"/> <img src="https://img.shields.io/badge/Gemini%20API-4285F4?style=flat-square&logo=google&logoColor=white"/>

<br>


## 📌 프로젝트 개요
 
| 항목 | 내용 |
|------|------|
| 개발 기간 | 2026.03 ~ 진행 중 (졸업 프로젝트) |
| 팀 구성 | 2인 |
| 담당 파트 | 아이디어 제안, 분석, 노트, 마이페이지, 뱃지, 프론트엔드 일부, 배포 |
| 배포 | Railway (운영 중) |
 
<br>
 
## 🔗 배포 URL
 
| 환경 | URL |
|---|---|
| 프론트엔드 | https://hivibe-production-a5f6.up.railway.app |
| 백엔드 | https://hivibe-production.up.railway.app |
 
<br>
 
## 📎 설계 문서
 
| 문서 | 링크 |
|------|------|
| 🎨 화면 설계서 (Figma) | [바로가기](https://www.figma.com/design/4POXDn7CeHOPoGyaPHza7B/%ED%99%94%EB%A9%B4-%EC%84%A4%EA%B3%84%EC%84%9C?node-id=0-1&t=CuXokuIMxTU2mhj1-1) |
| 🗄 ERD | [바로가기](https://www.erdcloud.com/d/7p4ndiNspQ76nMNAj) |
| 📋 API 명세서 | [바로가기](https://docs.google.com/spreadsheets/d/1NIX6SB2AjMwW5NXItQIA8Zd82Yj1FIDMqxP3N-ghlMY/edit?gid=0#gid=0) |
 
<br>
 
## 🛠 기술 스택
 
| 구분 | 기술 |
|------|------|
| Backend | Java 21, Spring Boot |
| Frontend | Next.js, TypeScript |
| Database | MySQL (AWS RDS) |
| AI | Gemini API |
| Infra | Docker, Railway |
 
<br>
 
## 📱 주요 기능
 
- **코드 진단** — 코드 입력 → Gemini API 분석 → 점수(S/A/B/C/F) + 4가지 항목별 피드백 + 최적화 코드 제공
- **진단 이력** — 이전 진단 불러오기 (원본 코드 + AI 분석 결과 복원) / 목록 및 상세 조회 / 삭제
- **노트** — 학습 내용 자유 기록 (CRUD), 즐겨찾기, 태그, 학습 노트 / 자유 노트 구분
- **마이페이지** — 프로필, 진단 횟수·평균 등급 통계, 뱃지 시스템
- **뱃지** — 진단/학습/노트 활동 기반 13종 뱃지 자동 지급 및 획득 팝업
<br>
 
## 👩‍💻 박성하(three-co1ors) 담당 파트
 
### 1. Gemini API 연동 — 비정형 AI 응답의 정형화 및 외부 API 통신 설계
 
```
사용자 코드 입력
    ↓
[Spring Boot] 프롬프트 조립 (언어, 코드, 분석 기준)
    ↓
[Gemini API] 분석 결과 반환
    ↓
응답 파싱 → 정확성 / 효율성 / 가독성 / 스타일 점수 + 항목별 피드백 + 최적화 코드
    ↓
DB 저장 (ORN_CD → ANLS → OPT_CD 순차 저장, @Transactional)
```
 
- XML 태그 기반 출력 형식을 프롬프트에 명시하여 비정형 AI 응답을 정형화, 파싱 안정성 확보
- 언어별 분석 기준 프롬프트 커스터마이징
- `temperature: 0.0` 설정으로 동일 코드 재분석 시 일관된 점수 응답 확보
- `AiResponseDto` — 12개 필드 record, `getGrade()`로 totalScore → S/A/B/C/F 변환
- Gemini API 지연/장애 시 DB 커넥션 고갈 방지를 위해 API 호출 타임아웃 설정 및 예외 핸들링 적용
- 프론트엔드에서 `AbortController` 기반 분석 취소 기능 구현 (진행 중 요청 중단)
---
 
### 2. DB 설계 — 확장성을 고려한 AI 데이터 분리 아키텍처
 
```
ORN_CD (원본 코드 — 사용자 입력 데이터)
  └── ANLS (AI 분석 결과 — 4항목 점수 + reason + totalScore)
        └── OPT_CD (AI 최적화 코드 + 설명)
              └── DGNS (User ↔ Anls 연결 — 유저별 진단 이력 추적)
```
 
원본 데이터(사용자 입력)와 AI 생성 데이터(분석 결과, 최적화 코드)를 테이블 단계별로 분리하여 이력 독립 조회 및 재분석이 가능하도록 설계. 추후 AI 모델 변경 시 ANLS/OPT_CD만 교체하면 되는 확장성을 고려.
 
`DGNS` 테이블은 뱃지 시스템의 유저별 진단 횟수 집계, 스트릭 계산, 언어 다양성 추적에도 활용.
 
---
 
### 3. 진단 API
 
- `POST /diagnosis` — 진단 결과 저장 (`DiagnosisService`, `@Transactional`)
- `GET /diagnosis` — 진단 목록 조회 (`DiagnosisListItemDto`)
- `GET /diagnosis/{id}` — 진단 상세 조회 + AI 분석 결과 복원 (`DiagnosisDetailDto`)
- `DELETE /diagnosis/{id}` — 진단 삭제 (연관 Lrn/LrnBlank/LrnSubm/OptCd/Anls/OrnCd 순차 삭제)
---
 
### 4. 마이페이지 API
 
- `GET /mypage/profile` — 프로필 + 진단 횟수 + 평균 등급 포함 응답 (`MypageService`, `DgnsRepository`)
- `PATCH /mypage/profile` — 프로필 이미지 / 닉네임 수정
- `PATCH /mypage/phone` — 휴대폰 번호 저장
- `PATCH /mypage/settings` — 복습 알림 / 마케팅 수신 동의 설정 저장
- 프로필 이미지 정적 파일 서빙 (`WebConfig.java` 리소스 핸들러 설정)
---
 
### 5. 노트 API
 
| 기능 | 메서드 | 설명 |
|------|--------|------|
| 노트 생성 | POST | 제목 + 내용(LONGTEXT) + 태그 저장 (학습 노트 / 자유 노트 구분) |
| 노트 목록 조회 | GET | 전체 / 타입별 (LEARNING, MANUAL) / 즐겨찾기 필터 |
| 노트 단건 조회 | GET | 상세 조회 (AI 요약 포함) |
| 노트 수정 | PATCH | 낙관적 업데이트 |
| 노트 삭제 | DELETE | |
| 즐겨찾기 | PATCH | 토글 |
 
- `OPT_CD_ID nullable = true` 처리로 학습 노트 / 자유 노트 동시 지원
 
---
 
### 6. 뱃지 시스템
 
- 총 13종 뱃지 설계 및 구현 (진단 8종 + 노트 2종 + 학습 3종)
- 뱃지 조건 체크 및 자동 지급 (`BadgeService.checkAndAward()`, `checkAndAwardWithLearning()`)
- `DgnsRepository` 커스텀 JPQL 쿼리로 유저별 최고 점수, 언어 DISTINCT, 연속 일수(streak) 계산
- 진단 저장 / 노트 저장 / 학습 완료 직후 자동 뱃지 체크 트리거
- `newlyAchieved` 필드로 신규 획득 뱃지 식별 → 프론트 획득 팝업 연동
 
| 카테고리 | 뱃지 | 조건 |
|---|---|---|
| 진단 | 🔍 First Scan | 첫 진단 완료 |
| 진단 | ⚡ Speed Optimizer | 90점 이상 달성 |
| 진단 | 💯 Perfectionist | 100점 달성 |
| 진단 | 🏆 Grade S | S등급 달성 |
| 진단 | 🌐 Polyglot | 3개 이상 언어 분석 |
| 진단 | 🔥 On Fire | 7일 연속 분석 |
| 진단 | 📅 Consistent | 30일 연속 분석 |
| 진단 | 🎖️ Code Veteran | 진단 50회 이상 |
| 노트 | 📚 Bookworm | 노트 10개 저장 |
| 노트 | 📖 Note Master | 노트 30개 저장 |
| 학습 | 🎓 First Learner | 첫 학습 완료 |
| 학습 | ✨ Perfect Answer | 빈칸 채우기 100% 정답 |
| 학습 | 💪 Study Hard | 학습 10회 완료 |
 
---
 
### 7. 배포 — Docker + Railway
 
- `Dockerfile` 작성 (백엔드: eclipse-temurin 멀티스테이지 빌드 / 프론트엔드: node 멀티스테이지 빌드)
- `docker-compose.yml` 작성으로 로컬 전체 환경 단일 명령어 실행 가능
- `application-prod.yml` 작성으로 배포 환경 설정 분리 (민감 정보 환경변수 처리)
- Railway 배포 (백엔드 + 프론트엔드), AWS RDS 연결
- `server.forward-headers-strategy: framework` 설정으로 Railway 프록시 환경에서 HTTPS 정상 인식
- `NEXT_PUBLIC_` 변수 빌드 시점 주입 (`ARG` / Build Arguments) 문제 해결
- Google OAuth2 배포 환경 리디렉션 URI 등록 및 `OAuth2SuccessHandler` 환경변수 기반 처리
- Gemini 모델 업데이트 대응 (`gemini-pro` → `gemini-1.5-flash`)
 
---
 
### 8. Spring Security / CORS 정책 설정
 
- RESTful API 설계에 맞게 CORS 허용 메서드에 `PATCH` 추가 (`SecurityConfig`)
- 401/403 응답을 OAuth2 리다이렉트 대신 JSON으로 반환하여 클라이언트 에러 처리 일관성 확보
- 배포 환경 도메인 CORS 허용 목록 추가
---
 
### 9. 프론트엔드 — Next.js
 
- 모놀리식 `LeetCodeIDE.tsx` → 기능별 컴포넌트 분리 리팩터링
- `prism-react-renderer` 기반 syntax highlighting (Java/Python/JS/TS/C/C++ 6개 언어)
- `AbortController` 기반 AI 분석 취소 기능
- 진단 패널 — `getComplexityData()`로 Big-O 기반 시간복잡도 그래프 시각화
- 이전 진단 불러오기 다이얼로그 (`LoadDiagnosisDialog`) — 원본 코드 + AI 분석 결과 동시 복원
- 진단 저장 다이얼로그 리디자인 — 등급/점수 미리보기 카드, 4개 항목 점수 칩 표시
- 뱃지 언락 팝업 (`newlyAchieved` 필드명으로 Jackson 직렬화 충돌 해결)
- 마이페이지 프로필 / 통계 / 뱃지 화면 — 실제 API 연동
- 노트 편집 모드 + 즐겨찾기 낙관적 업데이트
- 노트 삭제 / 진단 삭제 `AlertDialog` 적용
- 태그 입력 칩(Chip) 기반 UX
- 클라이언트 사이드 auth guard (메인 페이지)
- 사이드바 닉네임 동기화 (`refreshKey` 패턴)
- 전역 한글 폰트 fix — Pretendard를 CSS 변수 스택(`font-syne`, `font-space`) fallback으로 추가
- 랜딩 페이지 코드 프리뷰 — Prism 기반 `MiniCodeBlock` 컴포넌트 구현
- 회원가입 성공 후 자동 로그인 → `/main` 바로 이동
<br>
 
## 🔧 트러블슈팅
 
### 1. 비정형 AI 응답 데이터의 정형화 및 파싱 안정성 확보
 
**문제:** Gemini API 응답 형식이 요청마다 달라 파싱 실패 반복 발생.
 
**원인:** LLM은 본질적으로 비정형 텍스트를 반환하기 때문에, 별도의 출력 형식 강제 없이는 응답 구조가 일관되지 않음.
 
**해결:** 프롬프트에 XML 태그 기반 출력 형식을 명시하여 파싱 가능한 정형 응답 구조를 강제. 이후 파싱 실패율이 크게 감소.
 
---
 
### 2. 외부 API(Gemini) 지연 시 DB 커넥션 고갈 위험 방지
 
**문제:** Gemini API 응답이 장시간 지연될 경우, `@Transactional` 내에서 DB 커넥션을 계속 점유하여 전체 서버 응답성이 저하될 수 있음.
 
**원인:** AI API 호출과 DB 저장 로직이 동일 트랜잭션 안에 묶여 있어, 외부 API 지연이 곧 커넥션 풀 고갈로 이어지는 구조적 위험 존재.
 
**해결:** Gemini API 호출에 타임아웃을 설정하고, API 호출 실패 시 예외를 명시적으로 처리하여 트랜잭션이 불필요하게 길어지지 않도록 제어.
 
---
 
### 3. 대용량 텍스트(코드 및 마크다운) 처리를 위한 DB 스키마 최적화
 
**문제:** 코드가 포함된 긴 노트 저장 시 truncation 오류 발생.
 
**원인:** `note_cn` 컬럼이 `TINYTEXT`(최대 255 bytes)로 설정되어 있었고, 코드 스니펫이나 마크다운을 포함한 노트 특성상 255자를 쉽게 초과.
 
**해결:** `LONGTEXT`로 변경하여 최대 4GB까지 저장 가능하도록 스키마 수정.
 
```sql
ALTER TABLE note MODIFY COLUMN note_cn LONGTEXT;
```
 
---
 
### 4. Spring Security와 RESTful API의 CORS 정책 정교화
 
**문제:** 노트 수정 요청(PATCH)에서만 CORS 오류 발생.
 
**원인:** Spring Security CORS 설정의 허용 메서드 목록이 `GET`, `POST`, `DELETE`만 포함하고 있었고, RESTful 설계상 수정 작업에 사용한 `PATCH`가 누락되어 있었음.
 
**해결:** `SecurityConfig`의 CORS 허용 메서드에 `PATCH` 추가.
 
---
 
### 5. ObjectMapper 빈 설정 오류로 인한 LocalDateTime 직렬화 실패
 
**문제:** 날짜 필드가 포함된 API 응답에서 직렬화 실패.
 
**원인:** `AppConfig.java`에서 `new ObjectMapper()`로 빈을 직접 생성하였고, 이 경우 Spring Boot의 자동 설정이 적용되지 않아 `JavaTimeModule`이 미등록 상태로 동작.
 
**해결:** `ObjectMapper` 빈에 `JavaTimeModule`을 명시적으로 등록.
 
---
 
### 6. 뱃지 언락 팝업 — Jackson boolean 직렬화 충돌
 
**문제:** 뱃지 언락 여부를 나타내는 필드가 항상 `false`로 반환.
 
**원인:** `isNew`로 필드명을 지정할 경우, Jackson이 `boolean` 타입의 getter(`isNew()`)를 `new` 필드로 잘못 매핑하는 직렬화 충돌 발생.
 
**해결:** 필드명을 `newlyAchieved`로 변경하여 Jackson의 getter 네이밍 컨벤션 충돌 회피.
 
---
 
### 7. 전역 한글 폰트 일관성 확보 — CSS 변수 스택 fallback 설계
 
**문제:** 배포 후 일부 컴포넌트에서 한글이 시스템 기본 폰트로 표시.
 
**원인:** `font-syne`, `font-space` 등 CSS 변수로 선언된 폰트 스택에 한글 폰트 fallback이 누락되어, 해당 변수를 사용하는 컴포넌트에서 한글을 렌더링할 수 없었음.
 
**해결:** `globals.css`에서 모든 폰트 변수 스택에 Pretendard를 fallback으로 추가. 컴포넌트별 개별 수정 없이 전역 적용.
 
---
 
### 8. 사이드바 닉네임 미동기화 — 컴포넌트 간 상태 공유 패턴
 
**문제:** 마이페이지에서 닉네임 수정 후 사이드바에 즉시 반영되지 않음.
 
**원인:** 사이드바와 마이페이지가 별도 컴포넌트로 분리되어 있어, 마이페이지의 수정 완료 이벤트가 사이드바에 전달되지 않음.
 
**해결:** `refreshKey` 상태를 공통 상위 컴포넌트에서 관리하고, 프로필 수정 완료 시 `refreshKey`를 갱신하여 사이드바를 강제 리렌더링.
 
---
 
### 9. 진단 삭제 시 연관 데이터 순서 의존성 — FK 제약조건 위반
 
**문제:** 진단 삭제 시 `Cannot delete or update a parent row: a foreign key constraint fails` 오류 발생.
 
**원인:** 진단(DGNS) → 학습(LRN) → 제출이력(LRN_SUBM), 빈칸(LRN_BLANK) 등 FK로 연결된 테이블이 있어, 부모 레코드를 먼저 삭제하면 자식 레코드가 참조 무결성을 위반.
 
**해결:** 삭제 순서를 자식 → 부모 순으로 명시적 제어.
```
LrnSubm → LrnBlank → Concept → Lrn → Dgns → OptCd → Anls → OrnCd
```
 
---
 
### 10. Railway 배포 환경에서 OAuth2 redirect_uri가 http로 전달되는 문제
 
**문제:** 배포 후 Google OAuth2 로그인 시 `redirect_uri_mismatch` 오류 발생. 실제 요청 URI가 `http://`로 전달됨.
 
**원인:** Railway는 리버스 프록시를 통해 요청을 받기 때문에, Spring Boot 입장에서는 클라이언트 요청이 `http`로 들어오는 것처럼 보임. 이로 인해 Spring Security가 redirect_uri를 `http://`로 생성.
 
**해결:** `application-prod.yml`에 `server.forward-headers-strategy: framework` 설정 추가. Spring이 `X-Forwarded-Proto` 헤더를 신뢰하여 실제 프로토콜(https)을 올바르게 인식.
 
---
 
### 11. Next.js NEXT_PUBLIC_ 환경변수가 배포 환경에서 undefined로 나오는 문제
 
**문제:** Railway Variables에 `NEXT_PUBLIC_API_URL`을 추가했음에도 런타임에서 `undefined`로 나와 API 호출 URL이 `/undefined/api/...`로 잘못 생성됨.
 
**원인:** Next.js의 `NEXT_PUBLIC_` 접두사 변수는 런타임이 아닌 **빌드 시점**에 번들에 인라인으로 주입됨. Variables에만 추가하면 런타임 환경변수로만 등록되어 빌드된 번들에 반영되지 않음.
 
**해결:** Dockerfile에서 `ARG NEXT_PUBLIC_API_URL` + `ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL`로 빌드 시점 주입. Railway Build Arguments에도 별도 등록.
 
<br>
 
## 📂 프로젝트 구조
 
```
SH_Hivibe/
├── frontend/
│   ├── app/
│   │   ├── features/          # 기능별 페이지
│   │   ├── library/
│   │   ├── login/
│   │   ├── main/
│   │   ├── oauth2/callback/
│   │   ├── signup/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   ├── diagnosis/         # 코드 진단 컴포넌트
│   │   ├── dialogs/           # 뱃지 언락 등 다이얼로그
│   │   ├── layout/
│   │   ├── learning/
│   │   ├── mypage/            # 마이페이지 컴포넌트
│   │   ├── notes/             # 노트 컴포넌트
│   │   ├── shared/
│   │   ├── ui/
│   │   ├── leetcode-ide.tsx   # 코드 에디터 (리팩토링 대상)
│   │   └── theme-provider.tsx
│   ├── hooks/
│   ├── lib/
│   ├── public/
│   ├── styles/
│   └── types/
│
└── server/
    └── src/main/java/com/hivibe/server/ # 각 폴더에 (controller, dto, service)
        ├── ai/                # Gemini API 연동
        ├── badge/             # 뱃지 시스템
        ├── config/            # Spring 설정
        ├── dgns/              # 진단 (Diagnosis)
        ├── domain/            # 공통 도메인
        ├── lrn/               # 학습 (Learning)
        ├── mypage/            # 마이페이지
        ├── note/              # 노트
        ├── repository/        # DB 접근
        ├── sign/              # 인증
        └── ServerApplication.java
```
 
## 🗄 DB 설계
 
**핵심 테이블 구조**
 
```
users
  - user_id, email, name, profile_image, review_alarm_yn
 
ORN_CD (원본 코드)
  - orn_cd_id, user_id, code, language, created_at
 
ANLS (분석 결과)
  - anls_id, orn_cd_id, total_score
  - accuracy_score, accuracy_reason
  - efficiency_score, efficiency_reason
  - readability_score, readability_reason
  - style_score, style_reason
  - created_at
 
OPT_CD (최적화 코드)
  - opt_cd_id, anls_id, optimized_code, explanation
 
DGNS (진단 이력 — User ↔ Anls 연결)
  - dgns_id, user_id, anls_id, dgns_nm, dgns_dt
 
notes
  - note_id, user_id, opt_cd_id (nullable), title, note_cn (LONGTEXT), is_favorite, tags, created_at, updated_at
 
badges
  - badge_id, user_id, badge_key, achieved_at
  - UNIQUE (user_id, badge_key)
```
 
> **3-테이블 저장 플로우 설계 의도:**  
> 원본 데이터(사용자 입력)와 AI 생성 데이터(분석 결과, 최적화 코드)를 테이블 단계별로 분리.
> 이력 독립 조회 및 재분석이 가능하며, 추후 AI 모델 변경 시 ANLS/OPT_CD 레이어만 교체하면 되는 확장성을 고려한 구조.
 
<br>
 
<br>
 
## 🚀 실행 방법
 
**Backend**
```bash
cd server
./gradlew bootRun
```
 
**Frontend**
```bash
cd frontend
npm install
npm run dev
```
 
**Docker (전체 환경)**
```bash
docker compose up --build
```
