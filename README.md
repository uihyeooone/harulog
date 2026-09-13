# harulog

하루 기록 앱. 프론트엔드 개발자가 백엔드를 배우기 위해 8주 동안 키우는 서비스.
학습 계획은 [backend-todo_1.md](backend-todo_1.md) 참고.

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

# 2. 환경변수 파일 준비
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

---

## 프론트엔드와 백엔드는 어떻게 다른가

> **TODO (Week 0-7)**: todo 문서의 표를 보지 말고, 자기 말로 다시 써볼 것.
> 베껴 쓰면 남는 게 없다. 5년간 프론트에서 겪은 일과 엮어서 쓰기.

| | 프론트엔드 | 백엔드 |
|---|---|---|
| 누가 쓰나 | | |
| 데이터 | | |
| 동시에 실행 | | |
| 잘못되면 | | |
| 배포 | | |

---

## 설계 근거 기록

> 배우면서 내린 결정과 그 이유를 여기에 쌓는다. 나중에 면접에서 설명할 수 있어야 한다.

### DB 설계 (Week 2)
- [ ] 순차 id의 문제와 대응
- [ ] `TIMESTAMPTZ`를 쓰는 이유
- [ ] 소프트 삭제의 대가
- [ ] 기분 범위를 코드와 DB 양쪽에 건 이유

### DB 커넥션 총량 계산 (Week 3)
```
서버 _대 × 프로세스 _개 × (pool_size _ + max_overflow _) = _개
PostgreSQL 기본 허용치 = 100개 → ?
```

### 성능 측정 결과 (Week 6)
- [ ] 인덱스 전/후
- [ ] OFFSET vs 커서 페이지네이션
- [ ] 부하 테스트 (평균 / p95 / p99 / RPS / 실패율)
