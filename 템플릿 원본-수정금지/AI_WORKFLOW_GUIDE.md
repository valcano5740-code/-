# AI Development Workflow Guide

## 1. The 4-Pillar System (문서 체계)

이 4가지 문서가 있으면 AI는 기억을 잃지 않고, 프로젝트는 파편화되지 않습니다.

### 🏛️ 1. The Registry (지도 & 법전)

- **파일**: `REGISTRY.md`
- **역할**: 프로젝트의 **"현재 구조"**와 **"규칙"**을 정의합니다.
- **원칙**:
  - **Index, Not Content**: 파일의 모든 코드를 적는 게 아니라, "무슨 파일이 어디에 있고 뭐 하는 녀석인지" 한 줄 요약만 적습니다.
  - **Register First**: 새 파일을 만들기 전에 반드시 여기에 먼저 등록(선언)해야 합니다.

### 📋 2. The Tracker (나침반)

- **파일**: `TASK.md`
- **역할**: 할 일을 아주 잘게(Atomic) 쪼개서 관리합니다.
- **원칙**: 작업 단위가 클수록 AI는 헤맵니다. "로그인 기능 구현" (X) -> "로그인 UI 생성", "API 연동", "에러 처리" (O).

### 📜 3. The Journal (항해일지)

- **파일**: `DEV_LOG.md`
- **역할**: **"시행착오와 결론"**을 기록합니다.
- **원칙**:
  - 모든 잡담을 적는 게 아닙니다. "뭘 시도했고, 왜 실패했나? 그래서 결론은 뭔가?"만 남깁니다.
  - 내용이 길어지면 `ARCHIVE` 파일로 옮기고 "핵심 요약"만 남깁니다.

### ⚙️ 4. The Manual (작업 지침서)

- **파일**: `AI_WORKFLOW_GUIDE.md` (본 문서)
- **역할**: 작업할 때마다 따르는 표준 절차(SOP)입니다.

---

## 2. The 5-Step Development Cycle (표준 절차)

AI에게 작업을 시킬 때 이 순서를 강제하세요.

1.  **Context Loading (상황 파악)**:
    - `REGISTRY.md`를 읽어 "어디를 건드려야 할지" 파악.
    - `DEV_LOG.md`를 읽어 "피해야 할 함정" 파악.
2.  **Planning (계획)**:
    - `implementation_plan.md` 등을 이용해 계획 수립.
    - **Safety Check**: 기존 구조를 해치지 않는지 점검.
3.  **Execution (실행)**:
    - **보수적 분리 (Conservative Separation)**: 일단 기존 파일에 기능을 추가하고, 덩어리가 커지면 그때 분리합니다.
    - 새 파일을 만들면 즉시 `REGISTRY`에 등록.
4.  **Verification (검증)**:
    - 기능 테스트 및 기존 기능(Regression) 점검.
5.  **Alignment (절차 종료 & 정리)**:
    - `DEV_LOG`에 "성공/실패/교훈" 기록.
    - `TASK` 완료 처리.
    - 불필요한 임시 코드 삭제 등 정리(Cleanup).
