# jslab-basic

Docker Compose 기반 개발/운영 환경 구성 프로젝트.
JupyterLab + Nginx + PostgreSQL + Redis 서비스를 포함합니다.

---

## 디렉토리 구조

```
hc-basic/
├── docker-compose.yaml     # 메인 서비스 구성
├── nginx/                  # Nginx 설정 파일
├── pgsql/                  # PostgreSQL 데이터 볼륨
├── static/                 # 정적 파일 (jslab ↔ nginx 공유)
└── data/                   # 애플리케이션 데이터
```

---

## 서비스 구성

| 서비스 | 이미지 | 포트 | 설명 |
|--------|--------|------|------|
| `jslab` | `hubcane/jslab:basic` | 81, 5173, 8888, 8001, 1122(SSH) | JupyterLab 기반 개발 환경 |
| `nginx` | `hubcane/nginx:basic` | 80, 443, 1222(SSH) | 리버스 프록시 |
| `pgsql` | `postgres:16.13-trixie` | 5432 | PostgreSQL 데이터베이스 |
| `redis` | `redis:8.6.2-trixie` | 6379 | Redis 캐시/큐 |

---

## 시작하기

### 사전 요구사항

- Docker, Docker Compose

### 환경 변수 설정

```bash
cp .env.example .env
# .env 파일에 DB 비밀번호 등 설정
```

### 서비스 실행

```bash
cd /hc/hc-basic
docker compose up -d
```

### 서비스 중지

```bash
docker compose down
```

---

## 네트워크

모든 서비스는 `sd_con` bridge 네트워크를 공유합니다.
