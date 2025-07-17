# .github

## ✅ 문서 목적

이 문서는 프론트엔드 2명, 백엔드 2명으로 구성된 소규모 개발팀이 안정적이고 효율적인 Git 협업을 수행할 수 있도록 브랜치 전략, 커밋 규칙, 충돌 방지 방식 등을 정의합니다.

---

## 1. 브랜치 전략 개요

### 📌 기본 브랜치

| 브랜치 | 설명 |
| --- | --- |
| `main` | 운영 환경에 배포되는 최종 코드 (항상 안정 상태 유지) |
| `develop` | 기능 통합 및 테스트용 브랜치 (배포 전 중간 단계) |

### 📌 작업 브랜치

| 브랜치 명 | 예시 | 설명 |
| --- | --- | --- |
| `feature/FE-이름-작업명` | `feature/FE-hyun-login-ui` | 프론트엔드 기능 작업 |
| `feature/BE-이름-작업명` | `feature/BE-jiwoo-user-api` | 백엔드 기능 작업 |
| `bugfix/*` | `bugfix/BE-token-error` | 개발 중 발견된 버그 수정 |
| `hotfix/*` | `hotfix/payment-failure` | 운영 중 발생한 긴급 수정 (main에서 분기) |
| `release/*` | `release/v1.0.0` | 배포 직전 QA 및 문서 점검용 |

---

## 2. Git 작업 흐름

### 👣 브랜치 생성

```bash
git checkout develop
git pull origin develop
git checkout -b feature/FE-hyun-login-ui

```

### 👣 커밋 & 푸시

```bash
git add .
git commit -m "feat: 로그인 UI 구현"
git push origin feature/FE-hyun-login-ui

```

### 👣 PR 작성

- 대상 브랜치: `develop`
- 리뷰어: 최소 1인
- 병합 방식: **Squash Merge**

---

## 3. 커밋 메시지 컨벤션 (Conventional Commits)

| 타입 | 설명 | 예시 |
| --- | --- | --- |
| `feat` | 새로운 기능 추가 | `feat: 회원가입 API 구현` |
| `fix` | 버그 수정 | `fix: 로그인 오류 해결` |
| `refactor` | 리팩토링 | `refactor: 중복 코드 정리` |
| `docs` | 문서 작업 | `docs: README 업데이트` |
| `style` | 포맷 변경 (기능 X) | `style: 코드 정렬 및 세미콜론 추가` |
| `test` | 테스트 코드 추가 | `test: 로그인 테스트 추가` |
| `chore` | 빌드/설정 파일 | `chore: ESLint 설정 추가` |

---

## 4. 협업 및 역할 분담

### 🧑‍💻 역할

| 파트 | 분담 방식 |
| --- | --- |
| 프론트엔드 | 화면 단위 또는 기능 단위 분리 |
| 백엔드 | 도메인 기반 API 분리 (예: auth, post, user 등) |

### 📌 협업 시 주의사항

- 기능 간 인터페이스는 미리 정의하고 공유
- 공통 코드 수정 전 간단한 공유 필수
- merge 후에도 develop을 기준으로 최신 상태 유지 권장

---

## 5. 🔁 충돌 방지 전략 (유연한 협업 환경 대응)

### ✅ 1. 브랜치 분기 전 develop 최신화

```bash
git checkout develop
git pull origin develop
git checkout -b feature/작업명

```

### ✅ 2. PR 전 develop 병합으로 충돌 사전 확인

```bash
git checkout develop
git pull origin develop
git checkout feature/작업명
git merge develop

```

- 충돌이 발생하면 본인 작업 브랜치에서 직접 해결
- PR 메시지 또는 커뮤니케이션 채널(Slack, Notion 등)에 충돌 여부 공유

### ✅ 3. PR은 순차적으로 머지

- 동시에 여러 PR을 병합하는 것을 지양
- 하나씩 머지 → develop 최신화 → 다음 PR 머지 순서 권장

---

## 6. 브랜치 보호 및 PR 규칙

| 항목 | 권장 설정 |
| --- | --- |
| `main`, `develop` 브랜치 보호 | ✅ 강제 push 금지 |
| PR 리뷰어 | 최소 1인 지정 |
| 병합 방식 | ✅ **Squash Merge** 사용 |
| 자동 테스트(CI) | 가능 시 연동 (선택 사항) |

---

## 7. 브랜치 구조 예시

```
main ───────▶ 배포용 코드
   ↑
release/v1.0.0

develop ───────────▶ 통합 개발용
   ↑       ↑
feature/FE-hyun-login-ui
feature/BE-jiwoo-user-api

```

---

## ✅ 부록: 팀 협업 팁

- GitHub Projects 또는 Notion으로 기능 진행 현황 관리 (To Do / Doing / Done)
- PR 템플릿을 만들어 리뷰 체크리스트 포함
- 일정 단위로 기능 점검 및 통합 테스트 주기 설정 권장

---

필요 시 `.md` 파일로 저장하거나, Notion/Google Docs용 템플릿 형태로도 제공해드릴 수 있어요. 원하시면 말씀해주세요!
