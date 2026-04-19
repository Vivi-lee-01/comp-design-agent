# INDEX: 파일 라우팅 맵

에이전트가 어떤 상황에 어떤 파일을 읽어야 하는지 빠르게 찾기 위한 맵.

## 상황별 참조 가이드

### "제도가 없는 조직에 새로 설계해야 한다"
1. `context/company-profile.md` — 조직 이해
2. `context/constraints.md` — 제약 파악
3. `knowledge/principles.md` — 설계 원칙
4. `playbooks/full-design.md` — 절차 진행

### "현 제도를 진단하고 개선점 찾아야 한다"
1. `context/current-system.md` — 현 상태
2. `knowledge/principles.md` — 기준점
3. `knowledge/benchmarks.md` — 외부 비교
4. `playbooks/diagnose.md` — 진단 절차
5. `templates/diagnosis-report-template.md` — 산출 형식

### "페이밴드만 만들면 된다"
1. `context/roles-and-levels.md` — 레벨 체계 (없으면 먼저 leveling부터)
2. `context/compensation-data.md` — 현 데이터
3. `knowledge/compensation/pay-bands.md` — 이론
4. `knowledge/compensation/market-benchmark.md` — 시장 데이터 활용법
5. `playbooks/design-pay-band.md` — 절차
6. `templates/pay-band-template.md` — 형식

### "직무/레벨 정의가 먼저 필요하다"
1. `context/company-profile.md` + `context/roles-and-levels.md`
2. `knowledge/compensation/leveling.md`
3. `playbooks/design-leveling.md`
4. `templates/leveling-matrix-template.md`

### "평가 사이클 (OKR/MBO/피드백) 설계"
1. `context/company-profile.md` — 조직 규모/문화
2. `knowledge/performance/` 전체
3. `playbooks/design-review-cycle.md`
4. `templates/review-cycle-template.md`

### "가상 시나리오로 검증 루프를 돌려야 한다"
1. `scenarios/README.md` — 전체 실행 절차
2. `scenarios/{slug}/expected.md` — 해당 시나리오에서 반드시 잡아야 할 이슈
3. `scenarios/{slug}/context/*` — 시나리오의 조직 컨텍스트 (루트 `context/` 대체)
4. 실행할 플레이북 (`playbooks/diagnose.md` 등)
5. `scenarios/rubric.md` — 평가 체크리스트 (공통 + 플레이북별)
6. `scenarios/verifier-prompt.md` — **독립 verifier 에이전트** 호출 프롬프트 템플릿
7. 결과 저장: `scenarios/{slug}/runs/{date}_{playbook}/output.md`
8. 평가 저장: `scenarios/{slug}/runs/{date}_{playbook}/evaluation.md`

## 파일 간 참조 관계

```
principles.md
  ├─→ 모든 playbook이 참조
  └─→ diagnose.md의 평가 기준이 됨

pay-bands.md ←→ leveling.md ←→ market-benchmark.md
  └─→ 세 파일은 상호 참조, 함께 읽어야 의미 있음

current-system.md → diagnose.md의 입력
compensation-data.md → design-pay-band.md의 입력
```

## 파일이 없을 때 대응

에이전트가 참조하려는 파일이 존재하지 않으면:

1. **`context/` 파일 부재**: 사용자에게 해당 정보를 질문으로 요청
2. **`knowledge/` 파일 부재**: 에이전트의 일반 지식으로 대체 가능하나, 사용자에게 고지
3. **`templates/` 파일 부재**: 플레이북 지침에 따라 자체 생성
