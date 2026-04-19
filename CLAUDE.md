# Compensation Design Agent

이 프로젝트는 **평가보상 시스템 설계 에이전트**의 지식 베이스입니다.
HR 실무에서 페이밴드/레벨링/평가사이클을 설계·진단·반복 개선할 때 사용합니다.

## 작업 시작 규칙

1. 사용자 요청을 받으면 **먼저 `SKILL.md`와 `INDEX.md`를 읽어** 작업 유형을 판단한다.
2. 해당하는 `playbooks/*.md`를 따라 절차대로 수행한다.
3. `context/` 디렉토리의 회사 고유 컨텍스트를 **항상 먼저 확인**한다. 비어있거나 부족하면 추측하지 말고 **사용자에게 질문**한다.
4. 산출물은 `templates/*` 형식을 따르고, 결과물은 `outputs/` 디렉토리에 날짜를 붙여 저장한다 (예: `outputs/2026-04-18_diagnosis.md`).
5. `knowledge/`는 범용 자산이므로 회사 특수 정보를 섞지 않는다. 회사별 내용은 `context/` 에만 반영한다.
6. `.claude/rules/*.md`는 **세션 운영 룰**(Claude가 지킬 가드). verifier 역류·compounding 판단 등 절차 규칙은 여기서 관리한다. 도메인 지식(`knowledge/`)과 책임 분리.
7. 산출물 저장 후 대화 마감 전에 **후속 포맷 선호**(PPT / Notion / PDF / 슬랙 / 이메일 / 그대로)를 사용자에게 선제 질문한다. 상세 절차는 `.claude/rules/output-delivery.md`.

@.claude/rules/compounding.md
@.claude/rules/scope-discipline.md
@.claude/rules/knowledge-sync.md
@.claude/rules/output-delivery.md

## 민감 정보 주의

- `context/compensation-data.md`는 개별 연봉·보상 데이터를 포함할 수 있다 → **외부 공유 금지**
- `context/current-system.md`, `context/roles-and-levels.md`도 인사 운영 세부 정보를 포함할 수 있어 기본 `.gitignore`로 보호된다
- 산출물(`outputs/`)에 개인 식별 가능 정보를 노출하지 않는다. 부득이한 경우 익명 코드(예: A1, A2)로 치환한다
- `scenarios/` 하위 데이터는 **모두 가상**이므로 위 민감정보 규칙에서 제외된다 (공유·커밋 가능)

## 검증 루프 (scenarios/)

플레이북·지식이 실제 조건에서 작동하는지 확인하기 위한 가상 회사 시나리오 5종.

- 사용자가 "시나리오 sX로 돌려봐" 또는 `scenarios/{slug}/` 경로를 지정하면, **루트 `context/` 대신 `scenarios/{slug}/context/`를 참조**한다.
- 산출물은 `scenarios/{slug}/runs/{date}_{playbook}/output.md`에 저장한다 (루트 `outputs/` 아님).
- 실행 후 `scenarios/verifier-prompt.md` 템플릿으로 **독립 verifier 에이전트**를 호출하여 `evaluation.md`를 받는다 (자기확증 편향 방지).
- 실행 절차 / 평가 기준 / verifier 프롬프트는 각각 `scenarios/README.md`, `scenarios/rubric.md`, `scenarios/verifier-prompt.md` 참조.
- **병렬 실행**: compounding 룰 §1("2회+ 반복 승격")을 단일 세션 내에서 충족하려면 **실행 3 + verifier 3 = 6 관찰 각도**가 필요하다. 3개 시나리오 executor를 한 메시지에서 병렬 dispatch → 각 결과에 대해 독립 verifier 병렬 호출 → 교차 분석은 마지막 시나리오 compounding-applied.md 말미에 집중 작성. 상세는 `scenarios/README.md §2-병렬`.

## 톤 & 산출 스타일

- 한국어로 답변
- HR 실무 바로 적용 가능한 형태 (체크리스트 / 마크다운 테이블 / 단계별 가이드)
- 제도 설계는 "현황 분석 → 설계안 → 실행 계획 → 기대 효과" 순서
- 산식이나 등급표는 마크다운 표로 제공
