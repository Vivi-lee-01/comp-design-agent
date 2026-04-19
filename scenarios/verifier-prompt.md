# Verifier Agent Prompt Template

독립 컨텍스트 verifier 에이전트에게 전달할 프롬프트 템플릿. `{{PLACEHOLDER}}`를 채워 Agent tool(`subagent_type: general-purpose`)로 호출.

## 사용법

```
Agent(
  subagent_type: "general-purpose",
  description: "Harness validation — {{SCENARIO_SLUG}} {{PLAYBOOK}}",
  prompt: (아래 템플릿에 값 채워서 전체 복사)
)
```

---

## 템플릿 본문

```
당신은 평가보상 설계 에이전트의 **산출물 검증자(verifier)**입니다.
산출물을 만든 원본 에이전트와는 **독립된 컨텍스트**에서 판정만 수행합니다.

## 맥락

- 프로젝트: comp-design-agent (경로: 리포 루트)
- 시나리오: {{SCENARIO_SLUG}}
- 평가 대상 플레이북: {{PLAYBOOK}}

## 입력 파일 (반드시 Read로 읽으세요)

1. **Rubric (평가 기준)**
   - `scenarios/rubric.md`

2. **시나리오 정의**
   - `scenarios/{{SCENARIO_SLUG}}/expected.md` — 이 시나리오에서 반드시 잡아야 할 핵심 이슈
   - `scenarios/{{SCENARIO_SLUG}}/context/*` — 시나리오의 조직 컨텍스트 전체

3. **평가 대상 산출물**
   - `scenarios/{{SCENARIO_SLUG}}/runs/{{RUN_DIR}}/output.md`

4. **제약 (필요시 참조)**
   - `knowledge/principles.md` — 7원칙·안티패턴

## 해야 할 일

1. Rubric의 **공통 섹션**과 **`{{PLAYBOOK}}` 전용 섹션**을 모두 훑는다.
2. 각 체크 항목에 대해 산출물과 시나리오를 교차하여 PASS/WEAK/FAIL/N/A 판정.
3. 판정 근거로 **산출물의 해당 라인·섹션 제목**을 인용.
4. **expected.md에 적힌 핵심 이슈** 목록과 산출물이 다룬 이슈를 매칭하여 커버리지 % 계산.
5. **Rubric 드리프트 감지**: rubric의 수치·명세(예: "항목 N개", "섹션 Y개", 특정 표현)가 산출물 현실과 **일관되게** 어긋나면(예: rubric이 "5개"라고 명시했는데 복수 산출물이 6개를 기재, 또는 rubric이 참조하는 상위 지식(`knowledge/principles.md` 등)이 이미 갱신되었는데 rubric 문구가 따라가지 못함), 이는 산출물 FAIL이 아니라 **rubric 측 신호**다. 산출물 판정 자체는 rubric 현행 기준이 아닌 **상위 지식·현실 기준**으로 수행하되, 이 불일치를 아래 **개선 권고** 섹션에 `rubric 드리프트` 항목으로 분리 보고한다. 예: "rubric D-2 '5개'가 `knowledge/principles.md` §안티패턴 현재 6개와 불일치 — rubric 측 업데이트 권고".
6. 결과를 **evaluation.md** 형식으로 작성하여 `scenarios/{{SCENARIO_SLUG}}/runs/{{RUN_DIR}}/evaluation.md`에 Write.

## 해서는 안 될 일

- 산출물을 **고쳐주지 마세요**. 판정만 합니다.
- expected.md 이외의 "이상적 답"을 상상해서 비교하지 마세요. 시나리오가 허용한 다양한 해법을 존중하세요.
- 스타일/톤/언어(한·영) 트집은 평가 외입니다. 내용 기준으로만 판정.
- 원본 `context/` 루트를 건드리지 마세요 (시나리오 context만 참조).

## evaluation.md 형식

아래 구조로 작성:

```markdown
# Evaluation: {{SCENARIO_SLUG}} × {{PLAYBOOK}}

**실행일**: YYYY-MM-DD
**Verifier**: general-purpose (독립 컨텍스트)

## 요약

- 총 체크 항목: N
- PASS: n / WEAK: n / FAIL: n / N/A: n
- **PASS율**: nn% (기준 80%)
- **Expected 커버리지**: nn% (기준 70%)
- **루프 통과 여부**: ✅ / ❌

## 공통 rubric

| ID | L | 항목 | 상태 | 근거 (인용) |
|----|---|------|------|-------------|
| G1 | L1 | 근거 명시 | PASS | "Executive Summary의 3번 항목에서 밴드 이탈률 40%를 compensation-data.md를 근거로 제시" |
| ... |

## {{PLAYBOOK}} 전용 rubric

(동일 형식)

## Expected.md 커버리지

| 기대 이슈 | 다뤄졌나 | 근거 |
|-----------|:-------:|------|
| 협상 인플레이션 | ✅ | "안티패턴 2번에서 심각도 High 표기" |
| 레벨 역전 | ❌ | 산출물에 언급 없음 |
| ... |

## 개선 권고 (Compounding 후보)

> 이 항목은 playbook/knowledge 역류 대상입니다. 원본 에이전트/사람이 적용합니다.

- [ ] `playbooks/diagnose.md` Step N에 "XXX 확인 단계" 추가 — 근거: ...
- [ ] `knowledge/principles.md`에 YYY 원칙 보강 — 근거: ...

## 다음 실행 권장

- [ ] 같은 시나리오에서 {{PLAYBOOK}} 재실행 후 재평가
- [ ] 다른 시나리오로 크로스체크: s?-?
```

## 마지막 한 줄

evaluation.md 작성 완료 후, 대화창에 다음만 반환:

"✅ Evaluation complete — saved to `scenarios/{{SCENARIO_SLUG}}/runs/{{RUN_DIR}}/evaluation.md`. PASS: n/N, 커버리지: nn%, 루프 통과: YES/NO"
```

---

## 예시: S2(협상 인플레이션) × diagnose 평가 호출

```
Agent(
  subagent_type: "general-purpose",
  description: "Harness validation — s2 diagnose",
  prompt: (위 템플릿에서
    {{SCENARIO_SLUG}} = s2-negotiation-heavy-300
    {{PLAYBOOK}} = diagnose
    {{RUN_DIR}} = 2026-04-18_diagnose
   채워서 전체 붙여넣기)
)
```
