<div align="center">

# 🤖 HiVibe
### Hi, your code. High, your vibe.

**AI 코드 분석부터 맞춤 학습, 성장 기록까지 이어지는 개발자 학습 플랫폼**

사용자가 작성한 코드를 분석하고, 결과를 이해하고, 다시 학습할 수 있도록 만든 2인 졸업 프로젝트입니다.

<br>

![Java](https://img.shields.io/badge/Java_21-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL_8.4-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-4285F4?style=flat-square&logo=googlegemini&logoColor=white)
![AWS](https://img.shields.io/badge/AWS_EC2%20%2B%20RDS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)

<br>

[**🗂️ ERD**](https://www.erdcloud.com/d/7p4ndiNspQ76nMNAj) · [**📋 API 명세서**](https://docs.google.com/spreadsheets/d/1NIX6SB2AjMwW5NXItQIA8Zd82Yj1FIDMqxP3N-ghlMY/edit?gid=0#gid=0) · [**🎨 Figma**](https://www.figma.com/design/4POXDn7CeHOPoGyaPHza7B/%ED%99%94%EB%A9%B4-%EC%84%A4%EA%B3%84%EC%84%9C?node-id=0-1&t=CuXokuIMxTU2mhj1-1)

</div>

> [!NOTE]
> **서비스 이용해 보기**  
> 주소: https://www.hivibe.cloud/

---

## 📌 At a Glance

| 항목 | 내용 |
| :-- | :-- |
| **개발 기간** | 2026.03 ~ 2026.09 |
| **팀 구성** | 2인 · 졸업 프로젝트 |
| **서비스** | AI 코드 진단 · 맞춤 학습 · 진단 이력 · 학습 노트 · 활동 및 성장 관리 |
| **담당 영역** | AI 분석 연동 및 응답 검증, DB 설계, 백엔드 API, 활동 로그, 프론트엔드 일부, AWS 배포 |

### ✨ 이 프로젝트에서 집중한 문제

| 핵심 과제 | 해결 방향 |
| :-- | :-- |
| 🧠 **LLM 응답의 불확실성** | 출력 규칙을 정의하고 서버에서 응답과 점수를 한 번 더 검증 |
| 🗃️ **데이터 무결성과 확장성** | 원본 코드·분석 결과·사용자 진단 이력을 역할에 따라 분리 |
| ⚙️ **사용자 활동 추적** | 진단·학습 도메인과 활동 로그를 분리해 연속 활동 일수 계산 |
| ☁️ **실제 운영 환경** | Nginx·EC2·RDS·systemd 구성 및 배포 중 발생한 오류 해결 |

> **핵심 경험 한 줄**  
> LLM의 결과를 그대로 사용하는 대신 **출력 규약·검증 로직·데이터 구조·운영 환경**을 함께 설계해 서비스에 안정적으로 연결했습니다.

---

## 🚀 What HiVibe Does

- 🔍 **AI 코드 진단** — 정확성·효율성·가독성·스타일 평가, 코드별 피드백과 등급 제공
- 💡 **개선 방향 제안** — 시간복잡도 분석과 최적화 코드 제공
- 🧩 **맞춤 학습** — 분석 결과를 바탕으로 한 빈칸 학습 및 힌트
- 📚 **학습 기록** — 진단 이력 복원, 노트·태그·즐겨찾기 관리
- 🏅 **성장 관리** — 활동 통계, 연속 활동 일수, 티어 및 13종 뱃지

### 🧭 서비스 흐름

```text
코드 입력 → AI 분석 → 응답 검증·점수 계산 → 결과 저장
                                      ↓
                         진단 이력 · 맞춤 학습 · 노트
                                      ↓
                             활동 기록 · 성장 관리
```

---

## 👩‍💻 My Contributions

아이디어 제안부터 구현·배포까지 참여했으며, 아래 영역을 직접 담당했습니다.

| 영역 | 기여 내용 |
| :-- | :-- |
| 🤖 **AI 분석** | FactChat API Gateway 기반 Gemini 연동, 평가 기준·출력 규칙 설정, 응답 파싱 및 서버 측 점수 보정 |
| 🗄️ **DB 설계** | 원본·분석·최적화 코드·진단 이력의 관계 설계, 사용자 활동 로그 구조 설계 |
| 🔧 **Backend** | 진단·노트·마이페이지·뱃지 API, 연관 데이터 삭제 및 집계 로직 구현 |
| 🎨 **Frontend** | 코드 진단 화면, 분석 결과·노트·마이페이지 연동 등 일부 기능 구현 |
| ☁️ **Infra** | EC2/RDS, Nginx, HTTPS, systemd, 환경변수 관리, 로컬 Docker Compose 구성 |

---

## 🏗️ Architecture

```text
                   사용자
                     │
             Next.js / TypeScript
                     │ REST API
                     ▼
            Spring Boot / Security
                     │
       ┌─────────────┼──────────────┐
       │             │              │
       ▼             ▼              ▼
    AI 진단       서비스 API     활동 로그
       │             │              │
       ▼             └──────┬───────┘
 FactChat Gateway           │
       │                    ▼
     Gemini             MySQL / RDS
       │
       ▼
 응답 파싱 · 검증 · 점수 보정
```

운영 환경에서는 **Nginx**가 요청을 Next.js(`3000`)와 Spring Boot(`8080`)로 전달하고, 각 애플리케이션을 **systemd** 서비스로 실행했습니다.

---

## 🔍 Key Engineering Challenges

기능 목록보다 개발 중 마주한 문제와 해결 과정에 초점을 맞췄습니다. 각 항목을 펼치면 구체적인 구현 내용을 확인할 수 있습니다.

### 01. 🧠 LLM 응답을 신뢰할 수 있는 서비스 데이터로 만들기

> **문제:** Gemini 응답의 형식이 일정하지 않거나 필수 정보가 누락되고, 하나의 코드 문제를 여러 항목에서 중복 감점하는 사례가 있었습니다.

**어떻게 해결했나요?**

- XML 기반 출력 규칙과 **정확성·효율성·가독성·스타일**별 평가 기준을 프롬프트에 명시했습니다.
- 네이밍·포맷 등의 동일 원인을 중복 감점하지 않도록 평가 기준을 구체화했습니다.
- 서버에서 필수 필드를 확인하고 각 점수를 **0~100** 범위로 보정했습니다.
- LLM이 반환한 총점 대신, 정확성 40% / 효율성 30% / 가독성 15% / 스타일 15%의 가중치를 적용해 총점을 다시 계산했습니다.
- 기준 이하 항목의 패널티, 누락값 기본 처리, API 지연·실패에 대한 예외 처리를 추가했습니다.

<details>
<summary><b>🛠️ 처리 흐름과 구현 상세 보기</b></summary>

<br>

```text
사용자 코드 + 언어
      ↓
평가 기준과 XML 출력 규칙을 포함한 프롬프트
      ↓
FactChat API Gateway → Gemini
      ↓
응답 파싱 · 필수 데이터 확인
      ↓
점수 범위 보정 · 가중치 총점 재계산
      ↓
DB 저장 및 사용자에게 피드백 제공
```

- 낮은 temperature를 적용하고, 원본 응답과 정규화 결과를 비교할 수 있도록 디버깅 로그를 구성했습니다.
- 실제 코드에서 확인할 수 있는 문제만 평가 근거로 사용하도록 프롬프트를 보완했습니다.
- 응답 오류를 서비스 내부 데이터 검증 단계에서 제어하도록 설계했습니다.

</details>

**💡 배운 점**  
프롬프트만으로 모델의 응답을 완전히 보장할 수 없다는 점을 경험했습니다. **LLM이 판단하는 영역**과 **서버가 데이터의 유효성을 검증하는 영역**을 나누는 설계가 중요했습니다.

### 02. 🗃️ 원본 코드와 AI 생성 데이터의 역할 분리

> **문제:** 원본 코드, 분석 결과, 최적화 코드, 사용자 진단 이력은 목적과 관리 방식이 달라 하나의 구조로 다루기 어려웠습니다.

```text
ORN_CD (원본 코드)
    ↓
ANLS (AI 분석 결과)
    ↓
OPT_CD (최적화 코드)
    ↓
DGNS (사용자 진단 이력 연결)
```

- 각 데이터를 역할에 따라 분리하고 진단 이력에서 다시 연결해 조회·복원할 수 있도록 설계했습니다.
- 학습 노트와 자유 노트를 모두 지원하기 위해 `OPT_CD_ID`를 nullable로 구성했습니다.
- 긴 코드와 마크다운 저장 시 발생한 truncation 오류는 컬럼을 `LONGTEXT`로 변경해 해결했습니다.

<details>
<summary><b>🛠️ FK 삭제 오류 해결 과정 보기</b></summary>

<br>

진단을 삭제할 때 연관 학습 데이터가 참조하고 있어 **FK 제약조건 오류**가 발생했습니다. 참조 관계를 확인하고 자식 데이터부터 순서대로 삭제하도록 로직을 수정했습니다.

```text
LrnSubm → LrnBlank → Concept → Lrn
        → Dgns → OptCd → Anls → OrnCd
```

</details>

**💡 배운 점**  
데이터 모델링에서는 저장 방식뿐 아니라 **조회·삭제·복원·확장**까지 함께 고려해야 한다는 점을 배웠습니다.

### 03. ⚙️ 사용자 활동 로그를 도메인 로직과 분리

> **문제:** 진단·학습 테이블에서 활동 통계를 직접 계산하면 활동 유형이 늘어날 때 집계 로직도 복잡해질 수 있었습니다.

```text
진단 완료 → DIAGNOSIS_COMPLETED ─┐
                                  ├─→ UserActivityLog
학습 완료 → LEARNING_COMPLETED ─┘          │
                                           ▼
                                날짜별 활동 · streak 계산
```

- `user_id`, `event_type`, `created_at`으로 최소한의 이벤트 정보를 기록했습니다.
- 같은 날 여러 활동이 있어도 **날짜 기준으로 중복 제거**한 뒤 연속 활동 일수를 계산했습니다.
- 진단·학습 데이터와 활동 추적 로직의 책임을 분리했습니다.

**💡 배운 점**  
활동 기록을 별도 구조로 분리하면 신규 활동 유형이 추가되어도 기존 도메인 로직에 대한 의존도를 줄일 수 있습니다.

### 04. ☁️ 배포부터 운영 오류 해결까지

> **목표:** 로컬에서 개발한 서비스를 실제 도메인에서 실행하고, 프론트엔드·API·DB가 올바르게 연결되도록 구성하기.

| 구성 요소 | 적용 기술 및 역할 |
| :-- | :-- |
| **Application** | AWS EC2 (Ubuntu), Next.js, Spring Boot |
| **Database** | AWS RDS / MySQL 8.4 |
| **Routing** | Nginx Reverse Proxy |
| **HTTPS** | Let's Encrypt / Certbot |
| **Process** | systemd (재부팅 후 서비스 실행) |
| **Local Dev** | Docker Compose (운영 배포 방식과 별도) |

<details>
<summary><b>🛠️ 실제로 해결한 배포 문제 4가지 보기</b></summary>

<br>

**① Nginx 라우팅 충돌**  
`www.hivibe.cloud` 접근 시 프론트 화면 대신 Spring Security의 `401 Unauthorized`가 표시됐습니다. 요청이 백엔드로 잘못 전달되는 것을 확인하고 도메인·경로별 라우팅을 분리했습니다.

```text
www.hivibe.cloud       → Next.js :3000
hivibe.cloud/api/**    → Spring Boot :8080
hivibe.cloud/oauth2/** → Spring Boot :8080
```

**② Next.js 환경변수 반영 문제**  
운영 화면에서 로컬 API로 요청하던 문제를 조사해 `NEXT_PUBLIC_` 환경변수가 빌드 시점에 반영된다는 점을 확인했습니다. 운영 API 주소를 설정하고 다시 빌드·배포했습니다.

**③ CORS 오류**  
Spring Security 설정에 실제 프론트 Origin인 `https://www.hivibe.cloud`가 누락되어 있었습니다. Origin을 추가하고 `OPTIONS` preflight 응답과 관련 헤더를 검증했습니다.

**④ EC2 메모리 부족**  
`t3.micro`에서 의존성 설치·빌드 중 프로세스가 종료되는 문제를 겪었습니다. **2GB Swap**을 추가해 설치와 production build를 완료했습니다.

</details>

**💡 배운 점**  
서비스 운영에서는 코드뿐 아니라 **환경변수, 네트워크 라우팅, 브라우저 보안 정책, 서버 자원**을 함께 이해해야 했습니다. 오류가 발생한 계층을 구분해 원인을 찾는 경험을 쌓았습니다.

---

## 🧰 Features & APIs

| 기능 | 주요 구현 내용 |
| :-- | :-- |
| 🔍 **AI 진단** | 4개 영역별 평가·등급, 근거, 시간복잡도, 개선 코드 |
| 🧩 **맞춤 학습** | 빈칸 채우기, 힌트 |
| 🕘 **진단 이력** | 결과 저장·목록·상세 조회·복원·삭제 |
| 📝 **노트** | 학습/자유 노트 CRUD, 태그, 즐겨찾기 |
| 👤 **마이페이지** | 프로필, 활동 통계, 연속 활동 일수, 티어 |
| 🏅 **뱃지** | 진단·학습·노트 기반 13종 뱃지 |

<details>
<summary><b>📋 주요 REST API 보기</b></summary>

<br>

```http
POST   /diagnosis         # 진단 결과 저장
GET    /diagnosis         # 진단 목록
GET    /diagnosis/{id}    # 상세 조회 및 결과 복원
DELETE /diagnosis/{id}    # 진단 삭제

GET    /mypage/profile
PATCH  /mypage/profile
PATCH  /mypage/phone
PATCH  /mypage/settings
```

노트 CRUD·즐겨찾기, 활동 로그, 뱃지 자동 검사 기능도 구현했습니다.

</details>

---

## 📁 Project Structure

<details>
<summary><b>📂 폴더 구조 펼쳐보기</b></summary>

<br>

```text
SH_Hivibe/
├── frontend/
│   ├── app/
│   ├── components/
│   │   ├── diagnosis/
│   │   ├── learning/
│   │   ├── mypage/
│   │   ├── notes/
│   │   ├── shared/
│   │   └── ui/
│   ├── hooks/
│   ├── lib/
│   └── types/
└── server/src/main/java/com/hivibe/server/
    ├── activity/
    ├── ai/
    ├── badge/
    ├── config/
    ├── dgns/
    ├── domain/
    ├── lrn/
    ├── mypage/
    ├── note/
    └── repository/
```

</details>

---

## 💻 Getting Started

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

**Docker Compose (로컬 통합 실행)**

```bash
docker compose up --build
```

> [!IMPORTANT]
> 환경변수 및 외부 AI·OAuth 인증 정보는 별도로 준비해야 합니다. 위 명령어는 실행 예시이며 필요한 설정이 없다면 정상 실행되지 않을 수 있습니다. 운영환경은 Docker Compose가 아닌 **EC2 + systemd + Nginx**로 구성했습니다.

---

## 📎 Design & Documentation

| 자료 | 링크 |
| :-- | :-- |
| 🎨 화면 설계서 | [Figma에서 보기](https://www.figma.com/design/4POXDn7CeHOPoGyaPHza7B/%ED%99%94%EB%A9%B4-%EC%84%A4%EA%B3%84%EC%84%9C?node-id=0-1&t=CuXokuIMxTU2mhj1-1) |
| 🗄️ ERD | [ERDCloud에서 보기](https://www.erdcloud.com/d/7p4ndiNspQ76nMNAj) |
| 📋 API 명세서 | [Google Sheets에서 보기](https://docs.google.com/spreadsheets/d/1NIX6SB2AjMwW5NXItQIA8Zd82Yj1FIDMqxP3N-ghlMY/edit?gid=0#gid=0) |

---

## 🌱 Retrospective & Next Steps

이번 프로젝트에서 가장 크게 배운 것은 **기능을 단순히 구현하는 일과 그 기능을 믿고 사용할 수 있게 만드는 일은 다르다**는 점입니다.

- **LLM:** 결과를 그대로 저장하기보다 출력 규약과 서버 검증을 함께 설계했습니다.
- **DB:** 데이터의 생명주기와 FK 참조 관계를 고려해야 했습니다.
- **운영:** 프론트·백엔드·프록시·DB 사이에서 오류 지점을 구분하고 해결하는 경험을 쌓았습니다.

**앞으로 보강하고 싶은 부분**

- [ ] 고정 코드 샘플을 활용한 LLM 평가 결과 회귀 테스트
- [ ] 누락·비정상 응답에 대한 파서 단위 테스트
- [ ] 환경변수 예제와 초기 설정 가이드
- [ ] 공통 검증 로직의 독립 모듈화 검토

> 위 체크리스트는 **추후 개선 계획**으로, 현재 구현 완료한 기능은 아닙니다.
