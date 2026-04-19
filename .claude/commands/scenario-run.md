---
description: 시나리오 × 플레이북 조합을 executor + verifier 병렬 dispatch로 자동 실행
argument-hint: {scenario-slug(s)} {playbook}
---

# /scenario-run

지정한 시나리오 × 플레이북 조합을 실행하고 독립 verifier 평가까지 원샷으로 처리한다. 복수 시나리오를 쉼표로 받으면 병렬 dispatch.

## 입력

- `$1` (SCENARIO_SLUGS): 단일 슬러그(`s1-early-stage-startup-40`) 또는 쉼표 구분(`s3-remote-global-120,s4-pre-ipo-tech-200,s5-b2b-edtech-80`). 짧은 표기(`s1`,`s3`) 수용 — `scenarios/` 하위에서 전방 일치로 resolve.
- `$2` (PLAYBOOK): 플레이북 이름 (`diagnose` / `design-pay-band` / `design-leveling` / `design-review-cycle`). `playbooks/{playbook}.md` 존재 확인.

## 실행 절차

### Step 1. 입력 정규화

1. `$1`을 쉼표로 split → slug 리스트
2. 각 slug가 짧은 형태면 `Glob: scenarios/{slug}*/` 로 전체 이름 확정. 매칭 0개·2개+면 사용자에게 질문
3. `$2`에 해당하는 `playbooks/{PLAYBOOK}.md` 존재 확인. 없으면 중단
4. RUN_DIR 계산: `$(오늘날짜 YYYY-MM-DD)_{PLAYBOOK}`

### Step 2. 경로 충돌 체크

각 시나리오에 대해 `scenarios/{slug}/runs/{RUN_DIR}/` 이미 존재하면 **덮어쓸지 확인**. 없으면 바로 진행.

### Step 3. Executor Agent 병렬 dispatch

슬러그 개수만큼 Agent tool을 **한 메시지에서 병렬 호출**한다. 각 Agent에는:

- 읽을 파일: `scenarios/{slug}/context/*`, `playbooks/{PLAYBOOK}.md`, `templates/{관련}.md`, `knowledge/principles.md`, `SKILL.md`, `INDEX.md`
- 저장 경로: `scenarios/{slug}/runs/{RUN_DIR}/output.md`
- 독립 컨텍스트 강조: 시나리오별 context만 참조, 루트 `context/` 참조 금지
- 산출물 구조는 플레이북이 지정하는 템플릿 엄수

### Step 4. Verifier Agent 병렬 dispatch

Step 3 완료 후 각 output.md에 대해 **별도 Agent**를 병렬로 호출. 프롬프트는 `scenarios/verifier-prompt.md` 템플릿의 `{{SCENARIO_SLUG}}`, `{{PLAYBOOK}}`, `{{RUN_DIR}}` 채워서 사용.

- 독립 컨텍스트 (executor와 분리)
- 산출물 수정 금지, 판정만
- 저장 경로: `scenarios/{slug}/runs/{RUN_DIR}/evaluation.md`

### Step 5. 요약 반환

모든 verifier 완료 후 시나리오별:
- PASS율 (N/16), Expected 커버리지 (N/M)
- 루프 통과 여부 (PASS/WEAK/FAIL)
- compounding 후보 건수 (executor 제안 + verifier 제안)

3개 이상 실행이면 말미에 "compounding 교차 분석이 필요하다면 `compounding-analyzer` agent를 호출하세요" 안내.

## 주의

- **병렬 dispatch 필수**: 한 메시지에 Agent tool을 슬러그 수만큼 호출 (직렬 금지)
- **verifier는 별도 Agent 호출**: executor와 같은 Agent에 합치지 말 것 (자기확증 편향)
- **RUN_DIR 오타 방지**: executor/verifier가 같은 경로를 참조하도록 컴파일 시 한 번만 계산
- `scenarios/` 하위 데이터는 가상이므로 민감정보 룰 제외

## 예시

```
/scenario-run s1 diagnose
/scenario-run s3,s4,s5 diagnose
/scenario-run s1-early-stage-startup-40 design-pay-band
```
