# Project Registry

## Critical Components (삭제/수정 금지)

> ⚠️ 이 항목들은 **사용자 승인 없이 절대 삭제/수정 금지**.
> 수정이 필요하면 반드시 사용자에게 먼저 확인을 받으세요.

- (예시) `src/core/` - 핵심 비즈니스 로직
- (예시) `config/` - 설정 파일

## Existing Features (기존 기능 목록)

> 새 기능 추가 전 **반드시** 여기서 중복 여부를 확인하세요.
> 유사 기능이 있으면 새로 만들지 말고 기존 것을 확장하세요.

| 기능        | 위치        | 설명                 |
| ----------- | ----------- | -------------------- |
| (예시) 인증 | `src/auth/` | 로그인/로그아웃 처리 |

---

## Directories

- `src/`: 소스 코드 디렉토리.
- `docs/`: 문서 디렉토리.

## Files

- `REGISTRY.md`: (현재 파일) 프로젝트 구조 정의.
- `AI_WORKFLOW_GUIDE.md`: 개발 워크플로우 가이드.
- `DEV_LOG.md`: 개발 및 이슈 로그.
- `TASK.md`: 작업 목록.
- `PLAN_TEMPLATE.md`: 구현 계획서 템플릿.

## Global Rules

1.  **Search First**: 새 파일/기능을 만들기 전에 "Existing Features"에서 유사한 것이 있는지 먼저 확인.
2.  **Register First**: 확인 후 없으면, 이 파일에 먼저 등록한 뒤 생성.
3.  **No Silent Delete**: 함수/파일 삭제 전 사용처 검색 필수. Critical Components는 절대 삭제 금지.
4.  **Conservative Separation**: 파일 분리는 신중하게. 관련 기능은 먼저 모듈화 후 필요 시 분리.
5.  **Language**: 문서는 한국어/영어 혼용 가능, 코드는 영어 권장.
