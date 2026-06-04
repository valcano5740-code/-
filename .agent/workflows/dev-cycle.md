---
description: AI 개발 5단계 표준 절차 - Context Loading → Planning → Execution → Verification → Alignment
---

# AI Development Cycle Workflow

이 워크플로우는 모든 개발 작업에서 반드시 따라야 하는 **5단계 표준 절차**입니다.

> 📁 모든 파일 참조는 **프로젝트 루트 기준 상대 경로**입니다.
> 예: `REGISTRY.md`, `src/auth/login.js`

---

## Step 0: Git 초기화 (프로젝트 시작 시 1회)

// turbo

1. Git 저장소가 없으면 `git init` 실행
2. `.gitignore` 파일 확인/생성

---

## Step 1: Context Loading (상황 파악)

작업 시작 전 필수 문서를 읽어 현재 상황을 파악합니다.

// turbo

1. `git status`로 현재 작업 상태 확인
2. `REGISTRY.md` 읽기:
   - **Critical Components** 섹션에서 수정 금지 항목 확인
   - **Existing Features** 섹션에서 기존 구현 파악
   - **Directories/Files** 섹션에서 프로젝트 구조 파악
3. `DEV_LOG.md` 읽기:
   - 과거 **실패 사례**와 **피해야 할 함정** 확인
4. `TASK.md` 읽기:
   - 현재 **진행 중인 작업** 확인 (세션 재시작 시 복원점)
   - **백로그** 확인

---

## Step 2: Planning (계획 수립)

구현 전에 반드시 계획을 세웁니다.

### 2-1. 중복 검사 (필수)

1. `REGISTRY.md`의 **Existing Features** 섹션 확인
2. 코드베이스에서 유사한 기능/함수 검색
3. **있으면**: 기존 것 확장 → 새로 만들지 마세요
4. **없으면**: 새로 생성 가능

### 2-2. 영향 범위 분석 (필수)

1. 수정할 파일을 **사용하는 다른 파일** 목록 작성
2. `REGISTRY.md`의 **Critical Components** 확인
3. Critical에 해당하면 특별히 주의

### 2-3. 계획서 작성

1. `PLAN_TEMPLATE.md`를 참조하여 `implementation_plan.md` 작성
2. **Safety Check**:
   - 기존 코드 구조를 해치지 않는가?
   - 기존 기능에 영향을 주는가?

---

## Step 3: Execution (실행)

계획에 따라 구현합니다. 다음 원칙을 반드시 준수하세요.

### 3-1. 파일 생성/분리 기준

// turbo

1. **Conservative Separation (기본 원칙)**:
   - 새 기능은 **기존 파일에 추가**
   - 처음부터 파일을 분리하지 마세요

2. **파일 분리 조건** (다음 두 조건 모두 충족 시):
   - 파일이 **300줄 초과** AND
   - 명확히 **독립된 기능 단위**가 있을 때

3. 새 파일 생성 시 **즉시** `REGISTRY.md`에 등록:
   - Files 섹션에 파일 추가
   - Existing Features 섹션에 기능 추가

### 3-2. 삭제 시 (필수 확인)

1. 함수/파일 삭제 전 **사용처 검색** 실행 (grep 등)
2. 검색 결과가 0건일 때만 삭제
3. **Critical Components는 절대 삭제 금지**

### 3-3. Git 커밋 정책

// turbo

1. **기능 단위 커밋**: 하나의 기능이 완성되면 커밋
   ```bash
   git add .
   git commit -m "[TASK-ID] 기능설명"
   ```
2. **위험 작업 전**: 현재 상태 먼저 커밋 (롤백 지점 확보)

### 3-4. 진행 상태 업데이트 (컨텍스트 유지)

1. `TASK.md`에서 해당 작업을 `[/]` (진행 중)으로 표시
2. 긴 작업 시 중간 진행 상황 기록:
   ```markdown
   - [/] **로그인 기능 구현**
     - [x] UI 생성 (완료)
     - [x] API 연동 (완료)
     - [ ] 에러 처리 ← 다음
   ```

### 3-5. 에러 처리 정책

1. 동일 에러 **3회 연속 실패** 시:
   - 작업 중단
   - `DEV_LOG.md`에 문제 기록
   - 다른 접근 방식 검토

---

## Step 4: Verification (검증)

구현이 완료되면 반드시 검증합니다.

### 4-1. 테스트 방법 (언어별)

// turbo

| 프로젝트 타입 | 명령어        | 성공 기준     |
| ------------- | ------------- | ------------- |
| Node.js       | `npm test`    | 에러 0건      |
| Python        | `pytest`      | PASSED 100%   |
| Godot         | 프로젝트 실행 | 에러/경고 0건 |
| 정적 HTML/JS  | 브라우저 실행 | 콘솔 에러 0건 |

### 4-2. Regression Test (필수)

1. `REGISTRY.md`의 Existing Features에서 **관련 기능 목록** 작성
2. 각 기능별 핵심 동작 1개씩 테스트
3. 결과 기록:
   - ✅ `로그인: 정상`
   - ❌ `회원가입: 에러 - [내용]`

### 4-3. 빌드/컴파일 확인

1. 프로젝트 빌드 명령 실행
2. 에러 0건 확인

---

## Step 5: Alignment (정리 및 문서화)

작업 종료 후 프로젝트 상태를 업데이트합니다.

// turbo

### 5-1. Git 최종 커밋

```bash
git add .
git commit -m "[TASK-ID] 완료: 기능설명"
```

### 5-2. TASK.md 업데이트

- 완료된 작업을 `[x]`로 표시

### 5-3. DEV_LOG.md 기록 (실패/교훈이 있는 경우만)

- **Issue**: 무엇이 문제였는가?
- **Attempt**: 무엇을 시도했는가?
- **Solution**: 어떻게 해결했는가?
- **Lesson**: 다음에 주의할 점은?

### 5-4. DEV_LOG 정리 (항목이 10개 이상일 때)

- 오래된 항목을 `ARCHIVE/DEV_LOG_YYYY-MM.md`로 이동
- 최근 5개만 유지

### 5-5. REGISTRY.md 동기화 검증

// turbo

1. **Files 섹션**: 실제 파일과 일치하는지 확인
   - 없는 파일이 등록되어 있으면 삭제
   - 있는 파일이 누락되어 있으면 추가
2. **Existing Features 섹션**: 실제 기능과 설명이 일치하는지 확인

### 5-6. 정리 (Cleanup)

- 불필요한 임시 코드, 디버그 로그 삭제

---

## 실험적 문제 해결 가이드 (Experimental Fix)

> ⚠️ **적용 조건**: 원인이 불분명하여 여러 시도가 필요한 복잡한 문제

실패한 시도가 코드에 그대로 남으면 프로젝트가 지저분해집니다.
**반드시 아래 절차를 따라 깔끔하게 유지하세요.**

### 시작 전 (필수)

// turbo

```bash
# 1. 현재 상태 저장 (안전장치)
git add .
git commit -m "[SAVE] 문제 해결 시도 전 상태"

# 2. 실험 브랜치 생성
git checkout -b fix/[문제설명-간단히]
```

### 각 시도마다 (반복)

// turbo

```bash
# 시도 N 시작
# 1. 변경 수행
# 2. 테스트

# 실패 시: 즉시 되돌리기 (흔적 남기지 않음)
git checkout -- .
# 또는 이미 커밋했다면
git reset --hard HEAD~1

# 성공 시: 커밋
git add .
git commit -m "[FIX] 문제설명: 해결 방법"
```

### 해결 완료 후 (필수)

// turbo

```bash
# 1. main 브랜치로 복귀
git checkout main

# 2. 성공한 수정사항만 병합
git merge fix/[문제설명-간단히]

# 3. 실험 브랜치 삭제 (깔끔하게)
git branch -d fix/[문제설명-간단히]
```

### 핵심 원칙

| 상황                   | 행동                               |
| ---------------------- | ---------------------------------- |
| 시도 실패              | **즉시 되돌리기** → 흔적 없음      |
| 시도 성공              | 커밋 → main에 병합                 |
| 여러 시도 중 일부 성공 | 성공한 것만 남기고 나머지 되돌리기 |

---

## 롤백 가이드 (문제 발생 시)

문제가 발생하면 다음 절차로 복구:

// turbo

1. `git log -5`로 최근 커밋 확인
2. 롤백할 커밋 선택
3. `git revert <commit-hash>` 실행
4. `DEV_LOG.md`에 롤백 사유 기록

---

## 세션 재시작 가이드

이전 세션이 중단된 경우:

// turbo

1. `TASK.md` → `[/]` 표시된 작업 확인 (마지막 진행 상태)
2. `DEV_LOG.md` → 최근 3개 항목 확인
3. `git status` → 커밋되지 않은 변경사항 확인
4. `git branch` → 실험 브랜치가 있으면 해당 브랜치로 이동
5. 이전 상태 복원 후 계속 진행
