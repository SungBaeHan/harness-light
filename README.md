# harness-light

**Claude Code 등 AI 코딩 에이전트와 함께 개발할 때 쓰는 경량 AI Development Harness**.

Markdown 파일 3개로 구성되어 있어 별도 도구나 플러그인 없이 어떤 프로젝트에도 복사해서 쓸 수 있다.
AI가 다음 순서를 일관되게 따르도록 만드는 것이 목적이다.

```text
Understand → Scope → Plan → [Human Checkpoint] → Implement → Run → Verify → Review → Summarize
```

> **Working Software First. Production Reasoning Second.**

---

## 언제 쓰나

- 시간 제한이 있는 개발 과제 (코딩 테스트·과제형 면접, 해커톤)
- 프로토타입·PoC처럼 빠르게 동작하는 결과가 필요한 작업
- 새 프로젝트의 초기 Bootstrap — 경량 상태로 시작해 필요할 때 프로세스를 추가

---

## 구성

| 파일 | 읽는 쪽 | 역할 |
| --- | --- | --- |
| `CLAUDE.md` | AI | 진입 지시, 정본 우선순위 |
| `docs/RULES.md` | AI | 작업 흐름, 범위 통제, 검증, 리뷰, 멈춤 조건 — 규칙은 이 파일 하나 |
| `docs/SSOT.md` | AI·사람 | 요구사항 해석·가정·설계·상태·검증 결과를 기록하는 템플릿 |
| `task/ORIGINAL_TASK.md` | AI·사람 | 과제·요구사항 원문 (사용자가 작성, AI는 수정 금지) |

규칙은 한 곳에만 둔다. 같은 규칙이 여러 문서에 있으면 고칠 때 어긋나기 때문이다.

---

## 사용 방법

1. 작업 루트에 `CLAUDE.md`와 `docs/`를 복사한다.
2. 과제·요구사항 원문을 `task/ORIGINAL_TASK.md`에 그대로 저장한다.
3. 작업 루트에서 Claude Code를 실행하고 시작한다.

```text
Follow CLAUDE.md. The task is in task/ORIGINAL_TASK.md.
Analyze the task and repository, then show me the plan before implementing.
```

4. **Checkpoint** — AI가 보여준 계획을 확인한다. 하네스에서 사람이 개입하는 가장 중요한 지점이다.

```text
[ ] 문제를 제대로 이해했는가?
[ ] MUST 요구사항이 빠지지 않았는가?
[ ] 요구하지 않은 기능을 추가하지 않았는가?
[ ] Minimum E2E가 실제 문제를 증명하는가?
[ ] 설계가 과도하지 않은가? 시간 안에 구현 가능한가?
[ ] Acceptance Criteria를 실제로 검증할 수 있는가?
```

틀린 부분은 이 시점에 바로 고친다. 예: *"RabbitMQ는 쓰지 말고 in-memory queue로 시작해. RabbitMQ는 PRODUCTION으로 기록해."*

5. 방향이 맞으면 진행시킨다. 이후 AI는 구현 → 실행 → 검증 → 리뷰 → 요약까지 연속으로 진행한다.

---

## 시간 운영 예시 (90분 기준)

고정 일정이 아니라 점검 시점 가이드다. 시간표보다 동작하는 상태를 우선한다.

| 시점 | 할 일 | 점검 질문 |
| --- | --- | --- |
| 0–10분 | 분석, 범위, 계획 | 방향이 맞는가? |
| 10–55분 | 핵심 경로 구현, 실행-수정 반복 | Core E2E가 실제로 동작하는가? |
| 55–70분 | 남은 MUST, 주요 검증, 테스트 | |
| 70–80분 | Critical/Major 리뷰와 수정 | 더 만들 것인가, 동작하는 결과를 지킬 것인가? |
| 80–90분 | 최종 검증, SSOT 요약 정리 | |

---

## AI 사용 과정을 보여줘야 할 때

과제 제출이나 리뷰에서 AI 활용 과정을 보여줘야 한다면, AI가 무엇을 만들었는지보다 **사람이 무엇을 판단하고 검증했는지**가 드러나게 한다.

- 과제 원문(`ORIGINAL_TASK.md`)과 AI의 해석(`SSOT.md`)을 구분해 둔다.
- Checkpoint에서 사람이 고친 내용을 남긴다.
- `SSOT.md`의 Verification 표에 실제 실행 명령과 결과를 남긴다.

---

## 프로젝트가 커지면

처음부터 모든 프로세스를 넣지 않는다. 실제 필요가 생길 때 복사한 프로젝트 쪽에 추가한다.

```text
tickets/ · ADR/ · reports/ · runbook/ · CI/CD rules · PR workflow · project-specific agent rules
```

**Complexity should be introduced by actual project needs.**

---

## 배경

개인 장기 프로젝트(LLM 기반 웹 서비스)에서 Claude·Codex 등 AI 에이전트와 함께 개발하며 운영하던 하네스가 원본이다.
원본에서 티켓·PR workflow, 프로젝트 고유 아키텍처, 리포트·배포 검증 같은 프로젝트 종속 요소를 걷어내고, 다음만 남겼다.

- 과제 원문을 요구사항의 원본으로 두는 우선순위 규칙
- MUST / SHOULD / PRODUCTION 범위 통제
- 최소 End-to-End 우선 구현
- **실행으로 확인한 것만 완료로 인정**하는 검증 원칙
- 사람이 방향을 확인하는 Checkpoint

```text
Generated ≠ Implemented ≠ Verified
Executed + Expected Result Observed = Verified
```

---

## License

[MIT](LICENSE) — 자유롭게 복사·수정·재배포할 수 있다.
