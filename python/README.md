# harulog · python

FastAPI 버전. 공통 커리큘럼·설계 근거·프론트/백 차이표는 [../README.md](../README.md) 참고.

## 스택

| 무엇 | 뭘 쓰나 |
|---|---|
| 언어 | 파이썬 3.12 (uv로 관리) |
| 웹 프레임워크 | FastAPI |
| DB | PostgreSQL 16 |
| DB 다루는 도구 | SQLAlchemy + Alembic |
| 임시 저장소 | Redis |
| 실행 환경 | Docker Compose |
| 테스트 | pytest |

## 시작하기

```bash
# 1. 의존성 설치 (.venv 자동 생성)
uv sync

# 2. 환경변수 파일 준비 (.env는 이미 있음, 새로 받은 사람만)
cp .env.example .env

# 3. DB / Redis 띄우기 (Week 2에서 docker-compose.yml 작성 후)
docker compose up -d

# 4. 서버 실행 (Week 1에서 app/main.py 작성 후)
uv run uvicorn app.main:app --reload
```

## 자주 쓰는 명령

```bash
uv run ruff check .          # 린트
uv run ruff format .         # 포맷
uv run pytest -q             # 테스트
uv add <패키지>              # 의존성 추가
uv add --dev <패키지>        # 개발용 의존성 추가
```
