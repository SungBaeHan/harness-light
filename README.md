# harness-light

시간 제한이 있는 **Coding Interview에서 Claude Code와 함께 개발하기 위한 경량 AI Development Harness**.

Markdown 문서만으로 구성되어 있으며, AI가 다음 순서를 일관되게 따르도록 만드는 것이 목적이다.

```text
Requirement Analysis → Scope Control → Minimum Implementation
→ Execution → Verification → Critical/Major Fix → Technical Explanation
```

> **Working Software First. Production Reasoning Second.**

---

## 배경

개인 장기 프로젝트(LLM 기반 웹 서비스)에서 Claude·Codex 등 AI 에이전트와 함께 개발하며 운영하던 하네스가 원본이다.
원본에서 Coding Interview에 맞지 않는 요소를 의도적으로 제거하고 최소 실행 구조만 남겼다.

제거한 것:

- Ticket / GitHub Issue / Branch / PR workflow
- 프로젝트 고유 Architecture, 특정 Database·Framework 강제
- 별도 Analysis Report, CI/CD·배포 검증
- 장기 프로젝트용 Documentation workflow

남긴 것:

- 과제 원문을 요구사항의 원본으로 두는 우선순위 규칙
- 요구사항 범위 통제 (MUST / SHOULD / PRODUCTION 분리)
- 최소 End-to-End 우선 구현
- **실행으로 확인한 것만 완료로 인정**하는 검증 원칙
- Human Engineer가 방향을 확인하는 Checkpoint

```text
Generated ≠ Implemented ≠ Verified
Executed + Expected Result Observed = Verified
```

---

## 구성

| 파일 | 역할 |
| --- | --- |
| `CLAUDE.md` | Claude Code 진입 지시 |
| `docs/README.md` | Human Engineer용 상세 사용 설명서 (면접 절차, 90분 운영 가이드 포함) |
| `docs/AI_ENTRYPOINT.md` | Claude의 시작점, 문서 읽기 순서 |
| `docs/AI_AGENT_RULES.md` | 행동 규칙과 Guardrail |
| `docs/AI_DEV_PROMPT.md` | 분석부터 최종 검증까지의 Execution Protocol |
| `docs/DEVELOPMENT_GUIDE.md` | 시간 제한 상황의 개발 전략 |
| `docs/SSOT.md` | 해석한 요구사항·가정·범위·구현 상태 (과제 시작 후 채움) |
| `docs/ARCHITECTURE.md` | 현재 과제의 아키텍처·기술 결정 (과제 시작 후 채움) |
| `docs/QA_AND_DONE.md` | 검증 전략과 Definition of Done |

---

## 사용 방법

1. 과제 작업 루트에 `CLAUDE.md`와 `docs/`를 복사한다.
2. 과제 원문을 `task/ORIGINAL_TASK.md`에 그대로 저장한다. (AI는 이 파일을 수정하지 않는다)
3. 과제 루트에서 Claude Code를 실행하고 다음과 같이 시작한다.

```text
Read docs/AI_ENTRYPOINT.md and follow the coding interview harness.

task/ORIGINAL_TASK.md contains the original interview task.
Treat it as the authoritative task source and do not modify it.

Before substantial implementation, show me the interpreted requirements,
minimum scope, and architecture so I can verify the direction.
```

상세 절차는 [`docs/README.md`](docs/README.md)를 참고한다.

---

## 원칙

- 면접 과제와 면접관의 지시가 항상 이 하네스보다 우선한다.
- 문서를 미리 채우지 않는다. 과제를 받은 뒤 필요한 만큼만 작성한다.
- 복잡도는 실제 필요가 생길 때 추가한다. 새 프로젝트의 Bootstrap으로 쓸 때도 경량 상태에서 시작한다.
- AI는 구현을 돕지만, 요구사항·기술 판단·최종 승인의 책임은 Human Engineer에게 있다.
