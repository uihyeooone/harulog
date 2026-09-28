# harulog · java

`harulog`을 자바/스프링부트로도 만들어보는 트라이얼. 파이썬(FastAPI) 버전은 [../python/](../python/)에
그대로 두고, 이 폴더 안에서만 독립적으로 진행한다. 공통 커리큘럼·설계 근거·프론트/백 차이표는
[../README.md](../README.md) 참고. `docs/backend-todo_1.md`의 개념(트랜잭션, 커넥션 풀, 인증,
인덱스 등)은 언어를 안 타므로 그대로 따라가되, 코드 예시는 스프링 방식으로 새로 짠다.

## 스택

| 무엇 | 뭘 쓰나 |
|---|---|
| 언어 | Java 21 (LTS) |
| 웹 프레임워크 | Spring Boot 4.1 (Spring MVC) |
| 빌드 도구 | Maven (`./mvnw`) |
| 입력 검증 | Bean Validation (`spring-boot-starter-validation`) — Pydantic의 스프링 버전 |
| 보일러플레이트 감소 | Lombok |
| 개발 편의 | DevTools (코드 저장 시 자동 재시작, `uvicorn --reload`의 스프링 버전) |

> **DB 관련 의존성(`spring-data-jpa`, `postgresql`)은 아직 안 넣었다.** 파이썬 커리큘럼 Week 1이
> DB 없이 메모리 저장부터 시작하는 것과 동일하게, Week 2에 해당하는 단계에서 추가한다.
> (미리 넣으면 DB 없이 서버가 아예 안 켜진다 — 실제로 한번 겪어보고 뺐다.)

## 시작하기

```bash
# JDK 21 PATH (이미 ~/.zshrc에 등록됨, 새 터미널이면 자동 적용)
java -version   # openjdk 21.0.12 이상 나오면 OK

# 컴파일
./mvnw compile

# 실행 (Ctrl+C로 종료)
./mvnw spring-boot:run
```

지금 상태로 띄우면 정의된 컨트롤러가 없어서 어떤 주소든 `404`가 뜬다 — 정상이다.
Week 1에 해당하는 첫 작업은 `GET /api/v1/health`용 `@RestController`를 직접 만드는 것.

## 확인된 것 (환경 세팅 단계)

- [x] JDK 21 설치 및 `JAVA_HOME` 등록
- [x] `./mvnw compile` 성공
- [x] `./mvnw spring-boot:run` → 8080 포트로 Tomcat 기동 확인
- [x] 서버 종료까지 정상 확인
- [ ] `GET /api/v1/health` 컨트롤러 (직접 작성)

## 파이썬 버전과 매핑 (참고용)

| 파이썬 (FastAPI) | 자바 (Spring Boot) |
|---|---|
| `uv` | Maven (`./mvnw`) |
| Pydantic `BaseModel` | Bean Validation + DTO (record 또는 Lombok) |
| `Depends` | 생성자 주입 (`@RequiredArgsConstructor` 등) |
| SQLAlchemy | Spring Data JPA (Hibernate) |
| Alembic | Flyway 또는 Liquibase |
| `async def` (코루틴) | 서블릿 스레드풀 (요청마다 스레드 하나, 기본은 동기) |
| `pytest` | JUnit 5 |
