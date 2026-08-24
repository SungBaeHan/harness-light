# Coding Interview AI Harness

이 디렉터리는 **시간 제한이 있는 Coding Interview에서 Claude와 함께 개발하기 위한 경량 AI Development Harness**이다.

기존 장기 프로젝트용 개발 하네스에서 다음 요소들을 제거하고 Coding Interview에 필요한 최소 실행 구조만 남겼다.

* Ticket-driven workflow
* GitHub Issue / Branch / PR workflow
* 프로젝트 고유 Architecture 강제
* 특정 Database / Framework 강제
* 별도 Analysis Report 생성
* CI/CD 및 Production 배포 검증
* 장기 프로젝트용 Documentation workflow

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

# 1. Directory Structure

하네스는 다음 7개 문서로 구성한다.

```text
docs/
├── README.md
├── AI_ENTRYPOINT.md
├── AI_AGENT_RULES.md
├── AI_DEV_PROMPT.md
├── DEVELOPMENT_GUIDE.md
├── SSOT.md
├── ARCHITECTURE.md
└── QA_AND_DONE.md
```

`README.md`는 사람을 위한 사용 설명서다.

실제 AI 실행 시작점은:

```text
docs/AI_ENTRYPOINT.md
```

이다.

---

# 2. Document Roles

## README.md

### 역할

하네스 자체의 사용 설명서.

다음을 설명한다.

* 하네스 목적
* 각 문서 역할
* Claude 시작 방법
* Coding Interview 진행 방법
* 시간 제한 상황에서의 운영 원칙

### 대상

Human Engineer.

Claude의 직접적인 실행 규칙은 이 파일이 아니라 `AI_ENTRYPOINT.md`부터 시작한다.

---

## AI_ENTRYPOINT.md

### 역할

Claude의 **Bootstrap / Entry Point**.

Claude가 repository에 처음 들어왔을 때:

* 어떤 문서를 읽어야 하는지
* 어떤 순서로 읽어야 하는지
* 과제를 어떻게 받아들여야 하는지
* repository를 어떻게 조사해야 하는지
* 언제 구현을 시작해야 하는지

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

* 요구사항 임의 확대 금지
* 불필요한 Architecture 금지
* 최소 E2E 우선
* 불필요한 dependency 금지
* 생성한 코드의 실제 실행 의무
* Critical / Major 중심 Self-Review
* 시간 부족 시 Scope 축소
* Secret 및 Credential 보호
* Human control 유지

### 핵심 원칙

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

* Interview Task 분석
* MUST / SHOULD / PRODUCTION 분리
* Minimum E2E 정의
* 간단한 Architecture 결정
* 구현 계획
* Core implementation
* 실행 검증
* Self-review
* Critical / Major 수정
* 최종 검증
* 결과 요약

일상적인 단계마다 Human approval을 기다리지 않는다.

Blocking decision이 있을 때만 Human에게 질문한다.

---

## DEVELOPMENT_GUIDE.md

### 역할

시간 제한 상황에서 **어떤 개발 전략을 사용할 것인지** 정의한다.

AI_DEV_PROMPT가 실행 순서를 정의한다면, DEVELOPMENT_GUIDE는 개발 전략을 정의한다.

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

### 중요한 원칙

처음부터 Production Architecture를 구현하지 않는다.

예를 들어:

```text
Interview
In-memory Queue

Production
RabbitMQ / Kafka / SQS
```

처럼 Interview Implementation과 Production Architecture를 분리한다.

---

## SSOT.md

### 역할

현재 Coding Interview 과제의 **Single Source of Truth**.

면접 시작 전에는 Template 상태로 존재한다.

과제를 받은 후 Claude가 실제 문제를 기준으로 내용을 채운다.

### 기록 대상

* Original Interview Task
* Objective
* Required Functionality
* Constraints
* Acceptance Criteria
* MUST / SHOULD / PRODUCTION
* Ambiguities
* Assumptions
* Repository State
* Minimum E2E
* Technical Decisions
* Implementation Status
* Verification Status
* Known Limitations
* Production Considerations

### 중요한 원칙

SSOT에는 **현재 실제 상태**만 기록한다.

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

* FastAPI
* Node.js
* REST
* Database
* Message Queue
* Microservices
* Docker
* Kubernetes
* Worker
* GPU
* Frontend

Architecture는 반드시 실제 문제에서 도출한다.

### 기록 대상

* Architecture Drivers
* Constraints
* Components
* Responsibilities
* Control Flow
* Data Flow
* State Model
* Interfaces
* Persistence
* Concurrency
* Worker Model
* ML / GPU Processing
* Technical Decisions
* Interview Simplifications
* Production Evolution

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

면접 전에 빈 작업 repository 또는 제공된 repository의 루트에:

```text
docs/
```

디렉터리를 복사한다.

하네스 자체는 특정 언어, Framework 또는 Architecture를 전제하지 않는다.

Claude를 실행한 후 다음 정도의 초기 지시만 제공한다.

```text
Read docs/AI_ENTRYPOINT.md and follow the coding interview harness.

Do not implement anything until the interview task is provided.
```

이 시점에서는:

* Architecture를 만들지 않는다.
* Application code를 만들지 않는다.
* Framework를 선택하지 않는다.
* SSOT를 임의로 채우지 않는다.

Interview Task를 기다린다.

---

# 5. When the Interview Task Is Given

면접 문제 원문을 Claude에게 그대로 제공한다.

가능하면 문제를 과도하게 재해석하지 않고 원문을 유지한다.

예:

```text
This is the coding interview task.

[PASTE ORIGINAL TASK HERE]

Use docs/AI_ENTRYPOINT.md and the interview harness.

First analyze the requirements and establish the minimum implementation scope.

Then proceed with implementation unless a genuinely blocking ambiguity requires my decision.
```

Claude는 먼저 다음을 수행한다.

```text
Task
 ↓
Requirements
 ↓
Constraints
 ↓
Acceptance Criteria
 ↓
MUST / SHOULD / PRODUCTION
 ↓
Minimum E2E
 ↓
Architecture
 ↓
Implementation Plan
```

이 결과를 기반으로 `SSOT.md`와 필요한 경우 `ARCHITECTURE.md`를 갱신한다.

---

# 6. Do Not Fully Populate Documentation First

면접 시작 직후 모든 문서를 완성하려고 하지 않는다.

문서는 구현을 지원해야 하며 구현 시간을 소비하는 별도 업무가 되어서는 안 된다.

초기에는 `SSOT.md`에서 다음 정도만 확보하면 충분하다.

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

Architecture 역시 필요한 부분만 기록한다.

나머지는 구현 과정에서 중요한 결정이 발생했을 때 업데이트한다.

---

# 7. Implementation Strategy

첫 번째 목표는 **Minimum End-to-End Vertical Slice**다.

예를 들어 문제가 비동기 Job 처리 시스템이라면 실제 구조가 다음과 같을 수 있다.

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

하지만 이것은 예시일 뿐이다.

실제 문제에 Queue가 필요하지 않으면 Queue를 만들지 않는다.

GPU가 필요하지 않으면 GPU 구조를 만들지 않는다.

Database가 필요하지 않으면 Database를 추가하지 않는다.

---

# 8. Claude Development Loop

Claude는 다음 loop를 사용한다.

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

# 9. Human Role

Claude가 코드를 작성하더라도 Human Engineer는 다음을 담당한다.

* 문제 이해
* Claude의 Requirement Interpretation 확인
* 주요 Architecture 판단
* Scope 결정
* 중요한 Trade-off 판단
* 실행 결과 확인
* 최종 설명

Claude가 선택한 Architecture를 자동으로 승인하지 않는다.

중요한 결정이 잘못되었다고 판단되면 즉시 방향을 수정한다.

---

# 10. Self-Review Strategy

Core E2E가 동작한 후 Claude에게 한 번의 집중된 Self-Review를 수행하게 한다.

Review 대상은:

## Critical

* 실행 불가
* Core flow 실패
* 필수 기능 누락
* 잘못된 결과

## Major

* 중요 요구사항 위반
* 상태 관리 오류
* 중요한 concurrency 문제
* 핵심 error handling 문제

다음은 우선순위에서 제외한다.

* Naming preference
* Cosmetic refactoring
* Optional abstraction
* Production architecture 개선
* Style-only changes

Review 자체가 새로운 대규모 개발 작업으로 변하지 않도록 한다.

---

# 11. Time Recovery Rule

시간이 부족해질 경우:

```text
STOP
- Optional Features
- Refactoring
- Architecture Expansion
- Infrastructure Expansion
- Documentation Expansion
```

그리고 다음에 집중한다.

```text
Core Scenario
      ↓
MUST Requirements
      ↓
Executable Verification
      ↓
Critical Fix
```

특히 전체 구현 시간의 약 2/3가 지났는데 Core E2E가 아직 동작하지 않는다면 Scope를 즉시 축소한다.

---

# 12. Final Verification

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

가능하다면 마지막에 처음부터 Primary Scenario를 다시 실행한다.

---

# 13. Final Interview Preparation

구현 시간이 끝나기 전에 Claude에게 최종 상태를 짧게 정리하게 한다.

필요한 내용:

```text
1. What was implemented
2. Architecture
3. Important technical decisions
4. Verification performed
5. Known limitations
6. Production evolution
```

이 내용은 이후 Interview Discussion의 참고 자료로 사용할 수 있다.

---

# 14. Example Final Prompt

구현 종료 직전 Claude에게 다음과 같이 요청할 수 있다.

```text
Perform the final coding interview review.

1. Verify the primary end-to-end scenario.
2. Run the relevant tests.
3. Review only Critical and Major issues.
4. Fix Critical issues if any.
5. Re-run affected verification.
6. Update SSOT with actual verification results.
7. Give me a concise interview briefing covering:
   - implemented architecture
   - important decisions and trade-offs
   - verification results
   - known limitations
   - production evolution

Do not perform cosmetic refactoring or add optional features.
```

---

# 15. Expected Interview Workflow

전체적인 면접 실행 흐름은 다음과 같다.

```text
Interview Task Received
        ↓
Claude Reads Harness
        ↓
Requirement Analysis
        ↓
SSOT Initial Update
        ↓
Minimum E2E Definition
        ↓
Architecture Decision
        ↓
Implementation
        ↓
Early Execution
        ↓
Core E2E Working
        ↓
Important Requirements
        ↓
Tests
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

# Final Principle

이 하네스는 Claude가 개발자를 대신하여 모든 판단을 하도록 만드는 시스템이 아니다.

목적은 Claude를 이용하면서도 다음 과정을 명시적으로 통제하는 것이다.

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

면접에서 중요한 것은 많은 코드를 생성하는 것이 아니라:

* 요구사항을 제대로 이해했는가
* 합리적인 범위를 정했는가
* 실제로 동작하는가
* 검증했는가
* 기술적 선택을 설명할 수 있는가

이다.

**Build the smallest correct system that works, verify it, and be prepared to explain why it was built that way.**
