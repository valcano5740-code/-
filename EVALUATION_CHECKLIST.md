# AI Starter Kit Evaluation Checklist (Results)

## 1. Usability (사용성)

- [x] **Accessibility**: `REGISTRY`가 있으니 파일 위치를 헤맬 필요가 없음. (매우 유용)
- [ ] **Overhead**: 간단한 파일 수정(`REGISTRY` 한 줄 추가)을 위해 문서 3개(`TASK`, `LOG`, `REGISTRY`)를 다 열어야 함. -> **부담스러움.**
- [x] **Clarity**: `TASK`는 미래, `LOG`는 과거. 역할 구분은 명확함.

## 2. Efficiency (효율성)

- [x] **Sync Cost**: `PLAN_TEMPLATE`은 복사해서 쓰니까 OK. 하지만 `DEV_LOG`를 매번 쓰는 건 효율이 떨어짐.
- [x] **Context Loading**: `AI_WORKFLOW_GUIDE`는 AI에게 "행동 강령"을 주입하는 데 필수적임.

## 3. Necessity (필요성) - "굳이?"

- [x] **REGISTRY**: **필수**. AI가 가장 싫어하는 게 "없는 파일 참조하기"인데, 이걸 막아줌.
- [ ] **DEV_LOG**: **조건부 필요**. "성공" 로그는 무의미함. "실패/에러" 로그만 의미 있음. 단순 구현 성공까지 적는 건 낭비.
- [x] **PLAN_TEMPLATE**: **필수**. 복잡한 구현 전 "생각 정리" 단계로 매우 유용.
- [x] **TASK**: **필수**.

## 4. Improvement Proposals (개선안)

### 1. 로그 작성 기준 완화

- **현재**: 모든 작업 후 기록.
- **변경**: "에러가 발생했거나, 계획이 변경되었을 때만" 기록. (Exception-based Logging)

### 2. Registry 자동화 가능성

- **제안**: AI가 파일을 생성(`create_file`)할 때, 툴 내부에서 자동으로 `REGISTRY` 업데이트를 수행하도록 프롬프트("System Prompt")에 박아넣으면 좋겠지만, 현재는 파일로 관리해야 하므로 "파일 생성 시 필수 업데이트" 규칙 유지.

### 3. Task Granularity

- `TASK`에 "문서 업데이트" 같은 잡무는 적지 말고, "기능 단위"만 적도록 가이드 수정.
