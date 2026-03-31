# 잡잡한 세상 (Job Q&A)

> 숭실대학교 서버프로그래밍 3조 — 현직자들이 취업 정보를 나누는 iOS 커뮤니티 앱

---

## Summary

**잡잡한 세상**은 현직자들이 회사 생활, 취업 준비, 직무 정보를 자유롭게 공유하고 질문할 수 있는 Q&A 커뮤니티 앱입니다.  
카테고리별 게시판, 댓글/대댓글, 좋아요 기능을 제공하며, 회사 단위 커뮤니티로 운영됩니다.

---

## Features

- **회원가입 / 로그인** — JWT 기반 인증, bcrypt 비밀번호 해싱
- **게시글** — 카테고리별 작성, 조회, 수정, 삭제
- **댓글 / 대댓글** — 계층형 댓글 구조 (parent_comment_id)
- **좋아요** — 게시글·댓글 좋아요 토글
- **마이페이지** — 내 게시글, 댓글, 좋아요 목록 조회
- **회사 커뮤니티** — 회사별로 분리된 커뮤니티 공간

---

## Tech Stack

| 영역 | 기술 |
|------|------|
| iOS | Swift 5, SwiftUI, Moya (네트워킹) |
| Backend | Python 3.10, Flask 3.1, gunicorn |
| Database | MySQL 8.0, SQLAlchemy ORM |
| 인증 | JWT (PyJWT 2.8), bcrypt |
| 인프라 | Docker, Docker Compose |
| iOS 소셜 로그인 | Firebase Auth, Kakao SDK, Google Sign-In, Naver Login |

---

## Architecture

### Backend — 4계층 구조

```
app/
├── presentation/     # Flask routes, JWT 미들웨어, 직렬화
├── application/      # 비즈니스 로직 (Service)
├── persistence/      # 데이터 접근 (Repository)
└── database/         # ORM 모델, DB 세션
```

요청 흐름: `Client → Presentation → Application → Persistence → Database`

---

## Database Schema

| 테이블 | 설명 |
|--------|------|
| `companies` | 회사 정보 |
| `users` | 사용자 (회사 소속) |
| `categories` | 게시글 카테고리 |
| `boards` | 게시글 |
| `comments` | 댓글 / 대댓글 |
| `board_likes` | 게시글 좋아요 |
| `comment_likes` | 댓글 좋아요 |

ERD: [`docs/db/ERD.png`](docs/db/ERD.png)

---

## How to Run

### Backend (Docker)

> 자세한 내용은 [`docs/backend/setup.md`](docs/backend/setup.md) 참고

```bash
git clone https://github.com/SSU-ServerProgramming/Job_Q-A.git
cd Job_Q-A/backend/docker

# 환경 변수 파일 생성
cp .env.backend.example .env.backend
cp .env.db.example .env.db
# .env 파일 내 DB_USER, DB_PASSWORD 등 수정

# 개발 서버 실행
make dev-build
```

### iOS

```bash
cd ios/job_qa
pod install
open Crewing.xcworkspace
```

---

## Project Structure

```
Job_Q-A/
├── backend/
│   ├── app/
│   │   ├── presentation/   # Flask routes & 미들웨어
│   │   ├── application/    # Service 레이어
│   │   ├── persistence/    # Repository 레이어
│   │   └── database/       # ORM 모델
│   ├── db/                 # schema.sql, seed.sql
│   ├── docker/             # Dockerfile, docker-compose
│   ├── requirements.txt
│   └── Makefile
├── ios/
│   └── job_qa/
│       ├── Crewing/        # SwiftUI 소스 코드
│       ├── Podfile
│       └── Podfile.lock
├── docs/
│   ├── backend/            # API 명세, 설정 가이드
│   ├── db/                 # ERD
│   └── ios/
└── design/                 # Figma 디자인
```

---

## Team

| 이름 | 역할 |
|------|------|
| 김수민 | iOS |
| 김우진 | iOS |
| 김준석 | Backend |
| 김태영 | Backend |

> 숭실대학교 서버프로그래밍 3조
