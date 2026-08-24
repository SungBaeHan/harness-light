# Coding Interview AI Harness

이 디렉터리는 **시간 제한이 있는 Coding Interview에서 Claude와 함께 개발하기 위한 경량 AI Development Harness**이다.

기존 장기 프로젝트용 개발 하네스에서 다음 요소들을 제거하고 Coding Interview에 필요한 최소 실행 구조만 남겼다.

- Ticket-driven workflow
- GitHub Issue / Branch / PR workflow
- 프로젝트 고유 Architecture 강제
- 특정 Database / Framework 강제
- 별도 Analysis Report 생성
- CI/CD 및 Production 배포 검증
- 장기 프로젝트용 Documentation workflow

이 하네스의 목적은 프로세스를 많이 만드는 것이 아니다.

목표는 다음 순서를 AI가 일관되게 수행하도록 만드는 것이다.

```text
Interview Task
      ↓
Requirement Analysis
      ↓
Scope Control
      ↓
Minimum Architecture
      ↓
Implementation
      ↓
Execution
      ↓
Verification
      ↓
Focused Self-Review
      ↓
Critical / Major Fix
      ↓
Final Verification
      ↓
Technical Explanation
```

핵심 원칙은 다음과 같다.

> **Working Software First. Production Reasoning Second.**

---

# 1. Recommended Interview Workspace

면접 과제를 받으면 별도의 작업 루트를 만든다.

권장 구조:

```text
coding-interview/
├── task/
│   └── ORIGINAL_TASK.md
│
├── docs/
│   ├── README.md
│   ├── AI_ENTRYPOINT.md
│   ├── AI_AGENT_RULES.md
│   ├── AI_DEV_PROMPT.md
│   ├── DEVELOPMENT_GUIDE.md
│   ├── SSOT.md
│   ├── ARCHITECTURE.md
│   └── QA_AND_DONE.md
│
└── application source...
```

`task/ORIGINAL_TASK.md`에는 면접관이 제공한 **과제 원문을 가능한 그대로 보존**한다.

이 파일은 요구사항의 원본이다.

Claude는 이 파일을 읽고 분석할 수 있지만 임의로 수정하거나 재작성하지 않는다.

Claude가 해석한 요구사항, 가정, 범위, 구현 상태는 `docs/SSOT.md`에 기록한다.

---

# 2. Document Roles

## README.md

### 역할

Human Engineer를 위한 하네스 사용 설명서.

다음을 설명한다.

- 하네스 목적
- 각 문서 역할
- 실제 면접 작업 절차
- Claude 시작 방법
- 시간 제한 상황에서의 운영 원칙
- 최종 검증 및 인터뷰 준비 방법

Claude의 직접적인 실행 규칙은 README가 아니라 `AI_ENTRYPOINT.md`부터 시작한다.

---

## AI_ENTRYPOINT.md

### 역할

Claude의 **Bootstrap / Entry Point**.

Claude가 repository에 처음 들어왔을 때:

- 어떤 문서를 읽어야 하는지
- 어떤 순서로 읽어야 하는지
- 과제를 어떻게 받아들여야 하는지
- repository를 어떻게 조사해야 하는지
- 언제 구현을 시작해야 하는지

를 정의한다.

### 핵심 역할

```text
Claude Start
    ↓
Read Harness
    ↓
Understand Task
    ↓
Inspect Repository
    ↓
Define Minimum Solution
    ↓
Start Execution
```

Claude에게 처음 지시할 때 이 파일을 진입점으로 사용한다.

---

## AI_AGENT_RULES.md

### 역할

Claude의 **행동 규칙과 Guardrail**.

다음을 통제한다.

- 요구사항 임의 확대 금지
- 불필요한 Architecture 금지
- 최소 E2E 우선
- 불필요한 Dependency 금지
- 생성한 코드의 실제 실행 의무
- Critical / Major 중심 Self-Review
- 시간 부족 시 Scope 축소
- Secret 및 Credential 보호
- Human control 유지

Claude는 구현을 지원하지만 최종 기술적 판단과 승인 책임은 Human Engineer에게 있다.

---

## AI_DEV_PROMPT.md

### 역할

Claude가 과제를 **실제로 수행하는 Execution Protocol**.

전체 실행 순서를 정의한다.

```text
Understand
   ↓
Scope
   ↓
Design
   ↓
Implement
   ↓
Run
   ↓
Verify
   ↓
Self-Review
   ↓
Fix
   ↓
Final Verify
   ↓
Summarize
```

### 주요 기능

- Interview Task 분석
- MUST / SHOULD / PRODUCTION 분리
- Minimum E2E 정의
- Architecture 결정
- 구현 계획
- Core implementation
- 실행 검증
- Self-review
- Critical / Major 수정
- 최종 검증
- 결과 요약

일상적인 단계마다 Human approval을 기다리지 않는다.

Blocking decision이 있을 때만 Human에게 질문한다.

---

## DEVELOPMENT_GUIDE.md

### 역할

시간 제한 상황에서 **어떤 개발 전략을 사용할 것인지** 정의한다.

`AI_DEV_PROMPT.md`가 실행 순서를 정의한다면 `DEVELOPMENT_GUIDE.md`는 개발 전략을 정의한다.

### 핵심 전략

```text
Requirement First
      ↓
Minimum End-to-End
      ↓
Working Implementation
      ↓
Verification
      ↓
Hardening
      ↓
Final Review
```

처음부터 Production Architecture를 구현하지 않는다.

예:

```text
Interview
In-memory Queue

Production
RabbitMQ / Kafka / SQS
```

Interview Implementation과 Production Architecture를 분리한다.

---

## SSOT.md

### 역할

현재 Coding Interview 과제의 **Single Source of Truth**.

면접 시작 전에는 Template 상태로 존재한다.

과제를 받은 후 Claude가 실제 문제를 기준으로 내용을 채운다.

### 기록 대상

- Original Interview Task
- Objective
- Required Functionality
- Constraints
- Acceptance Criteria
- MUST / SHOULD / PRODUCTION
- Ambiguities
- Assumptions
- Repository State
- Minimum E2E
- Technical Decisions
- Implementation Status
- Verification Status
- Known Limitations
- Production Considerations

### 중요한 원칙

```text
Planned ≠ Implemented
Implemented ≠ Verified
```

검증하지 않은 기능을 PASS로 기록하지 않는다.

---

## ARCHITECTURE.md

### 역할

현재 Interview Task를 위해 선택한 **실제 Architecture**를 기록한다.

면접 시작 전에는 특정 Architecture를 정의하지 않는다.

### 미리 강제하지 않는 것

- FastAPI
- Node.js
- REST
- Database
- Message Queue
- Microservices
- Docker
- Kubernetes
- Worker
- GPU
- Frontend

Architecture는 실제 문제에서 도출한다.

### 기록 대상

- Architecture Drivers
- Constraints
- Components
- Responsibilities
- Control Flow
- Data Flow
- State Model
- Interfaces
- Persistence
- Concurrency
- Worker Model
- ML / GPU Processing
- Technical Decisions
- Interview Simplifications
- Production Evolution

필요하지 않은 섹션은 사용하지 않는다.

---

## QA_AND_DONE.md

### 역할

**무엇을 검증해야 완료라고 판단할 것인지** 정의한다.

### 핵심 원칙

```text
Generated
    ≠
Implemented

Implemented
    ≠
Verified

Executed + Expected Result Observed
    =
Verified
```

### 검증 우선순위

```text
Application Start
      ↓
Core End-to-End
      ↓
MUST Requirements
      ↓
Acceptance Criteria
      ↓
Critical Failure
      ↓
Automated Tests
      ↓
Secondary / Edge Cases
```

코드가 보기 좋다고 완료로 판단하지 않는다.

실제로 실행하고 결과를 확인한다.

---

# 3. Canonical Reading Order

Claude는 다음 순서로 문서를 읽는다.

```text
AI_ENTRYPOINT.md
       ↓
SSOT.md
       ↓
ARCHITECTURE.md
       ↓
AI_AGENT_RULES.md
       ↓
DEVELOPMENT_GUIDE.md
       ↓
AI_DEV_PROMPT.md
       ↓
QA_AND_DONE.md
```

단, `AI_ENTRYPOINT.md`를 읽은 이후에는 그 안에 정의된 순서를 따른다.

문서를 반복해서 계속 읽을 필요는 없다.

---

# 4. Before the Interview

면접 전에 `harness-light`의 `docs/`를 사용할 수 있도록 준비한다.

아직 과제를 받지 않은 상태에서는:

- Architecture를 만들지 않는다.
- Application code를 만들지 않는다.
- Framework를 선택하지 않는다.
- SSOT를 임의로 채우지 않는다.

Claude를 미리 실행한다면 다음 정도만 지시한다.

```text
Read docs/AI_ENTRYPOINT.md and follow the coding interview harness.

Do not implement anything until the interview task is provided.
```

---

# 5. Actual Interview Procedure — Human Engineer

이 절은 **실제 면접에서 Human Engineer가 수행할 작업 순서**다.

전체 흐름:

```text
[1] 과제 수령
        ↓
[2] 과제용 Root Directory 생성
        ↓
[3] harness-light/docs 복사
        ↓
[4] ORIGINAL_TASK.md 생성
        ↓
[5] Claude 실행
        ↓
[6] Harness + Task 분석 지시
        ↓
[7] Claude의 Requirement Interpretation 검토
        ↓
[8] SSOT / Architecture 초기화
        ↓
[9] Minimum E2E / Scope 확인
        ↓
[10] 구현 시작
        ↓
[11] Run → Verify → Fix 반복
        ↓
[12] Core E2E 확인
        ↓
[13] MUST 구현
        ↓
[14] Tests
        ↓
[15] Critical / Major Self-Review
        ↓
[16] Final Verification
        ↓
[17] SSOT 최종 갱신
        ↓
[18] Interview Briefing 확보
        ↓
[19] Technical Interview
```

---

# 6. Step 1 — Preserve the Original Task

과제를 받으면 먼저 원문을 보존한다.

```text
task/ORIGINAL_TASK.md
```

PDF나 별도 문서로 제공된 경우 원본 파일 자체를 `task/` 아래에 둘 수도 있다.

중요한 것은 **면접관이 준 요구사항과 Claude가 해석한 요구사항을 분리하는 것**이다.

```text
task/ORIGINAL_TASK.md
        =
Original Requirement

docs/SSOT.md
        =
Interpreted / Structured Requirement
```

Claude가 `ORIGINAL_TASK.md`를 임의로 수정하지 않도록 한다.

---

# 7. Step 2 — Start Claude

Claude를 과제 루트에서 실행한다.

최초 프롬프트 예:

```text
Read docs/AI_ENTRYPOINT.md and follow the coding interview harness.

task/ORIGINAL_TASK.md contains the original interview task.
Treat it as the authoritative task source and do not modify it.

Analyze the task and repository first.

Initialize only the necessary parts of:
- docs/SSOT.md
- docs/ARCHITECTURE.md

Identify:
- objective
- required functionality
- constraints
- acceptance criteria
- MUST / SHOULD / PRODUCTION
- important assumptions
- minimum end-to-end flow
- proposed architecture
- implementation plan

Do not over-document.

Before substantial implementation, show me the interpreted requirements,
minimum scope, and architecture so I can verify the direction.
```

---

# 8. Step 3 — Human Checkpoint

이 단계가 **가장 중요한 Human intervention point**다.

Claude가 만든 내용을 확인한다.

특히 다음을 본다.

```text
[ ] 문제를 제대로 이해했는가?
[ ] MUST 요구사항이 빠지지 않았는가?
[ ] 요구하지 않은 기능을 추가하지 않았는가?
[ ] Minimum E2E가 실제 문제를 증명하는가?
[ ] Architecture가 과도하지 않은가?
[ ] 기술 선택이 시간 안에 구현 가능한가?
[ ] Acceptance Criteria를 실제로 검증할 수 있는가?
```

잘못된 부분이 있다면 이 시점에 바로 수정한다.

예:

```text
The requirement interpretation is mostly correct,
but do not introduce RabbitMQ for the interview implementation.

Use an in-memory queue first and record RabbitMQ as a production consideration.

Proceed with the minimum end-to-end implementation.
```

방향이 맞으면 구현을 진행시킨다.

---

# 9. Do Not Fully Populate Documentation First

면접 시작 직후 모든 문서를 완성하지 않는다.

초기 `SSOT.md`에서는 다음 정도면 충분하다.

```text
Original Task
Objective
Required Functionality
Constraints
Acceptance Criteria
MUST
Important Assumptions
Minimum End-to-End Flow
Implementation Plan
```

`ARCHITECTURE.md` 역시 필요한 부분만 기록한다.

문서는 구현을 지원해야 한다.

문서 작성 자체가 별도의 프로젝트가 되어서는 안 된다.

---

# 10. Ticket Policy

**단일 시간 제한 Coding Interview에서는 기본적으로 Ticket을 만들지 않는다.**

사용하는 흐름은:

```text
Interview Task
      ↓
SSOT
      ↓
Architecture
      ↓
Implementation
      ↓
Verification
```

이다.

SSOT에 이미:

- 요구사항
- Acceptance Criteria
- Scope
- Implementation Plan
- Current Status

가 존재하기 때문에 다시 Ticket으로 구조화하면 중복 작업이 된다.

따라서 Coding Interview에서는:

```text
NO
SSOT
 ↓
Ticket
 ↓
Implementation
```

보다는:

```text
YES
SSOT
 ↓
Implementation
```

을 사용한다.

### 장기 프로젝트에서는?

이 하네스를 일반 프로젝트의 Bootstrap으로 사용하는 경우에는 필요에 따라 다음 단계에서 Ticket workflow를 추가할 수 있다.

```text
Harness-Light
     ↓
Project Requirements
     ↓
SSOT
     ↓
Architecture
     ↓
MVP Scope
     ↓
Milestone / Epic
     ↓
Tickets
     ↓
Implementation
```

즉, Ticket은 제거된 기능이 아니라 **프로젝트 규모가 필요로 할 때 추가하는 확장 기능**이다.

---

# 11. Implementation Strategy

첫 번째 목표는 **Minimum End-to-End Vertical Slice**다.

예를 들어 문제가 비동기 Job 처리 시스템이라면:

```text
Request
   ↓
API
   ↓
Job
   ↓
Queue
   ↓
Worker
   ↓
Processing
   ↓
Result
```

같은 구조가 나올 수 있다.

하지만 이것은 예시일 뿐이다.

실제 문제에 Queue가 필요하지 않으면 Queue를 만들지 않는다.

GPU가 필요하지 않으면 GPU 구조를 만들지 않는다.

Database가 필요하지 않으면 Database를 추가하지 않는다.

---

# 12. Claude Development Loop

Claude는 다음 Loop를 사용한다.

```text
Inspect
  ↓
Implement Small Change
  ↓
Run
  ↓
Observe
  ↓
Fix
  ↓
Run Again
```

큰 코드 덩어리를 한 번에 생성한 후 마지막에 실행하는 방식을 피한다.

가능하면 핵심 경로를 빠르게 실행 가능한 상태로 만든다.

---

# 13. Human Role During Implementation

Claude가 구현을 시작한 뒤에도 Human Engineer는 완전히 손을 떼지 않는다.

다음 사항을 계속 확인한다.

- 현재 구현이 MUST를 향하고 있는가
- Claude가 Scope를 확대하고 있지 않은가
- 불필요한 Dependency를 추가하지 않는가
- Architecture를 다시 크게 뜯으려 하지 않는가
- 실제 실행 결과를 확인하고 있는가
- 오류를 추측으로 고치고 있지 않은가

Human Engineer가 직접 모든 코드를 리뷰할 필요는 없다.

대신 **방향과 중요한 결정**을 통제한다.

---

# 14. Core E2E Checkpoint

가장 먼저 확보해야 할 것은 Core E2E다.

Core E2E가 동작하면 잠시 멈추고 확인한다.

```text
[ ] Application starts
[ ] Primary input enters
[ ] Required processing occurs
[ ] Result is generated
[ ] Result is observable
```

이 시점부터 Working Baseline을 보호한다.

이후 변경은 가능한 한 Incremental하게 수행한다.

---

# 15. Time Recovery Rule

전체 구현 시간의 약 2/3가 지났는데 Core E2E가 아직 동작하지 않는다면 Scope를 즉시 축소한다.

90분 구현이라면 대략 55~60분 부근을 하나의 경계로 볼 수 있다.

이 시점에서 Core E2E가 없다면:

```text
STOP

- Optional Features
- Refactoring
- Architecture Expansion
- Infrastructure Expansion
- Documentation Expansion
- Production Improvements
```

다음에만 집중한다.

```text
Make Core Scenario Work
        ↓
Verify MUST
        ↓
Fix Critical Problems
```

**작지만 동작하는 구현이 크지만 미완성인 구현보다 우선한다.**

---

# 16. Self-Review Strategy

Core E2E와 주요 MUST가 동작한 후 Claude에게 한 번의 집중된 Self-Review를 수행하게 한다.

Review 대상:

## Critical

- 실행 불가
- Core flow 실패
- 필수 기능 누락
- 잘못된 필수 결과

## Major

- 중요 요구사항 위반
- 상태 관리 오류
- 중요한 concurrency 문제
- 핵심 error handling 문제

다음은 우선순위에서 제외한다.

- Naming preference
- Cosmetic refactoring
- Optional abstraction
- Production architecture 개선
- Style-only changes

Review 자체가 새로운 대규모 개발 작업으로 변하지 않도록 한다.

---

# 17. Final Verification

마지막에는 반드시 실제 실행을 통해 확인한다.

최소 확인 대상:

```text
Application Starts
Core E2E Works
MUST Requirements Work
Acceptance Criteria Checked
Tests Executed
No Known Critical Issue
Demonstration Path Known
```

가능하다면 Primary Scenario를 처음부터 다시 실행한다.

Docker를 사용했다면 Docker build 성공만 확인하지 말고 실제 서비스에 요청을 보내 Core Scenario까지 검증한다.

---

# 18. Final Claude Prompt

구현 종료 직전 Claude에게 다음과 같이 요청할 수 있다.

```text
Perform the final coding interview review.

1. Verify the primary end-to-end scenario.
2. Verify all MUST requirements and acceptance criteria.
3. Run the relevant tests.
4. Review only Critical and Major issues.
5. Fix Critical issues if any.
6. Fix Major issues only if the change is low-risk and time permits.
7. Re-run affected verification.
8. Update docs/SSOT.md with actual verification results.
9. Update docs/ARCHITECTURE.md only where the actual implementation differs.
10. Give me a concise interview briefing covering:
    - what was implemented
    - implemented architecture
    - important technical decisions and trade-offs
    - verification results
    - known limitations
    - production evolution
    - likely interviewer questions

Do not perform cosmetic refactoring.
Do not add optional features.
Do not expand the architecture.
```

---

# 19. Interview Briefing

구현 종료 후 Claude의 최종 설명을 이용해 90분 Interview Discussion을 준비한다.

최소한 다음 질문에는 Human Engineer가 직접 답할 수 있어야 한다.

```text
1. 무엇을 구현했는가?
2. 왜 이 Architecture를 선택했는가?
3. 다른 대안은 무엇이었는가?
4. 왜 그 대안을 사용하지 않았는가?
5. 어떤 부분을 실제로 검증했는가?
6. 어떤 부분은 검증하지 못했는가?
7. 현재 구현의 가장 큰 한계는 무엇인가?
8. Production이라면 무엇을 바꿀 것인가?
9. Scale이 커지면 어디가 먼저 문제가 되는가?
10. 시간이 더 있었다면 무엇을 다음으로 구현할 것인가?
```

Claude의 설명을 그대로 암기하지 않는다.

본인이 설명할 수 없는 Architecture나 코드는 면접에서 위험 요소다.

---

# 20. Expected Interview Workflow

전체 실전 흐름:

```text
Interview Task Received
        ↓
Create Workspace
        ↓
Copy Harness
        ↓
Preserve ORIGINAL_TASK
        ↓
Start Claude
        ↓
Claude Reads AI_ENTRYPOINT
        ↓
Task + Repository Analysis
        ↓
SSOT Initial Update
        ↓
Minimum E2E Definition
        ↓
Architecture Decision
        ↓
===== HUMAN CHECKPOINT =====
        ↓
Implementation
        ↓
Early Execution
        ↓
Run → Observe → Fix
        ↓
Core E2E Working
        ↓
Protect Working Baseline
        ↓
Remaining MUST Requirements
        ↓
Relevant Tests
        ↓
Focused Self-Review
        ↓
Critical / Major Fix
        ↓
Final Verification
        ↓
SSOT Final Update
        ↓
Interview Briefing
        ↓
Technical Discussion
```

---

# 21. Approximate 90-Minute Operating Guide

시간은 문제 난이도에 따라 조정한다.

고정된 WBS가 아니라 **운영 가이드**로 사용한다.

```text
00 ~ 10 min
Task / Repository Analysis
Requirements
Scope
Minimum E2E
Architecture

10 ~ 55 min
Core Implementation
Early Execution
Run → Fix loop

55 ~ 70 min
Remaining MUST
Important Validation
Relevant Tests

70 ~ 80 min
Focused Self-Review
Critical / Major Fix

80 ~ 90 min
Final Verification
SSOT Update
Interview Briefing
```

### 가장 중요한 Checkpoint

```text
~10 min
방향이 맞는가?

~55-60 min
Core E2E가 실제로 동작하는가?

~80 min
더 개발할 것인가,
Working Solution을 보호하고 마무리할 것인가?
```

시간표보다 Working State를 우선한다.

---

# 22. Prompt Submission Consideration

면접에서 AI Prompt 또는 AI 사용 과정을 제출해야 하는 경우:

- 과제 원문과 Claude의 해석을 구분한다.
- 중요한 Human correction을 명확하게 남긴다.
- Claude가 생성한 코드를 실제 실행하고 검증한 흔적을 유지한다.
- 불필요하게 Prompt를 반복하거나 복잡한 Agent workflow를 만들지 않는다.
- 최종 결과를 AI가 만들었다는 사실보다 **어떤 판단과 검증을 Human Engineer가 수행했는지**가 드러나도록 한다.

가능하면 작업 과정은 다음 형태가 보이도록 한다.

```text
Requirement
    ↓
AI Analysis
    ↓
Human Review / Correction
    ↓
Implementation
    ↓
Execution Evidence
    ↓
AI Review
    ↓
Human Acceptance
```

---

# 23. Reusing Harness-Light for New Projects

`harness-light`는 Coding Interview뿐 아니라 새로운 프로젝트의 Bootstrap으로 사용할 수 있다.

새 프로젝트에서는 우선 경량 상태로 시작한다.

```text
Harness-Light
     ↓
Requirements
     ↓
SSOT
     ↓
Architecture
     ↓
MVP
```

프로젝트가 성장하면서 실제 필요가 발생하면 다음 요소를 추가한다.

```text
tickets/
ADR/
reports/
infra/
runbook/
CI/CD rules
PR workflow
deployment rules
project-specific agent rules
```

처음부터 모든 프로세스를 추가하지 않는다.

**Complexity should be introduced by actual project needs.**

원본 `harness-light`는 가능한 한 범용 Template 상태로 유지하고 프로젝트별 특화 내용은 복사된 프로젝트 쪽에서 관리한다.

---

# Final Principle

이 하네스는 Claude가 개발자를 대신하여 모든 판단을 하도록 만드는 시스템이 아니다.

목적은 Claude를 이용하면서도 다음 과정을 Human Engineer가 통제할 수 있도록 만드는 것이다.

```text
Understand
   ↓
Decide
   ↓
Implement
   ↓
Execute
   ↓
Verify
   ↓
Explain
```

면접에서 중요한 것은 많은 코드를 생성하는 것이 아니다.

- 요구사항을 제대로 이해했는가
- 합리적인 범위를 정했는가
- 실제로 동작하는가
- 검증했는가
- 기술적 선택을 설명할 수 있는가
- 무엇을 단순화했는지 알고 있는가
- Production에서는 어떻게 달라져야 하는지 설명할 수 있는가

가 더 중요하다.

**Build the smallest correct system that works, verify it, and be prepared to explain why it was built that way.**