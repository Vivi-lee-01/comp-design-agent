# 검증 루프 (Validation Loop)

가상의 회사 조건으로 플레이북을 돌려 **이 에이전트가 실제로 유의미한 설계를 내는지** 반복 검증하기 위한 시나리오 모음.

## 왜 만들었나

이 프로젝트는 "설계는 있지만 아직 돌려본 적 없는" 하네스에서 출발했다. 자동화 훅/테스트 프레임워크 대신, **가상 회사 시나리오 + 독립 에이전트 verifier**로 검증을 문서·절차로 풀어낸다.

- 하네스 축 5 (검증) — 플레이북이 실제 조건에서 작동하는지 확인
- 하네스 축 6 (개선) — 실패한 시나리오에서 발견한 결함을 `playbooks/`, `knowledge/`에 역류 → Compounding 루프

## 디렉토리 구조

```
scenarios/
├── README.md                     # 이 파일
├── rubric.md                     # 평가 체크리스트 (공통 + 플레이북별)
├── verifier-prompt.md            # 독립 verifier 에이전트 호출 프롬프트 템플릿
└── {scenario-slug}/
    ├── context/                  # 이 시나리오의 context/ 스냅샷
    │   ├── company-profile.md
    │   ├── current-system.md
    │   ├── roles-and-levels.md
    │   ├── constraints.md
    │   └── compensation-data.md  (선택)
    ├── expected.md               # 이 시나리오에서 반드시 잡아야 할 "핵심 이슈"
    └── runs/                     # 실행 기록 (flexible, 생성될 때 자동 생성)
        └── {date}_{playbook}/
            ├── output.md         # 플레이북 실행 결과물
            └── evaluation.md     # verifier 평가 결과
```

## 시나리오 카탈로그 (v0.1)

| Slug | 조직 프로필 | 난이도 | 기대 이슈 |
|------|------------|:-----:|-----------|
| `s1-early-stage-startup-40` | 시드~시리즈A, 40인, 테크 | Easy | 구조 전면 부재 (철학·레벨·밴드 모두 없음) |
| `s2-negotiation-heavy-300` | 시리즈D, 300인, 엔터프라이즈 | Hard | 협상 인플레이션, 동일 직급 격차 35%+ |
| `s3-remote-global-120` | 리모트 글로벌, 120인, 10개국 | Hard | 지역별 페이 정책 부재, 로컬 vs 표준 혼재 |
| `s4-pre-ipo-tech-200` | Pre-IPO, 200인 | Medium | Equity 집중, 현금 저평가, 코호트 격차 |
| `s5-b2b-edtech-80` | B2B SaaS, 80인 | Medium | 평가 인플레이션, 레벨 역전, 개정 정체 |

## 실행 절차 (Run Loop)

### 1. 시나리오 선택 & context 로드

루트 `context/`를 시나리오 context로 교체한다. 실제 작업에는 민감정보가 들어 있을 수 있으므로, 검증용은 **심볼릭 링크**나 **임시 스와핑**으로 처리한다.

```bash
# 예: S1을 루트로 로드
SCENARIO=s1-early-stage-startup-40
mv context context.real.bak
ln -s scenarios/$SCENARIO/context context
```

※ 실제 작업으로 돌아갈 땐 `rm context && mv context.real.bak context`.

### 2. 플레이북 실행

Claude Code에서 평소처럼 요청한다:

```
이 회사의 현 평가보상 제도를 진단해줘.
```

에이전트는 `SKILL.md → INDEX.md → playbooks/diagnose.md` 순서로 따라가며 `outputs/{date}_diagnosis.md`에 결과물을 낸다.

#### 2-병렬: 다중 시나리오 동시 실행 (3개 이상)

단일 시나리오 반복보다 **여러 시나리오를 병렬 실행**하면 compounding 승격 효율이 높다. **2회+ 반복 승격** 기준(`.claude/rules/compounding.md` §1)을 단일 세션 내에서 충족하려면 **실행 3 + verifier 3 = 6개 독립 관찰 각도**가 필요하다.

- Claude Code Agent tool로 시나리오별 executor를 **한 메시지에 병렬 dispatch**
- 각 실행 완료 직후 독립 verifier를 별도 dispatch (실행 세션과 분리)
- 3개 compounding-applied.md 교차 분석 → **마지막 시나리오 파일 말미**에 누적 교차표 집중 작성, 나머지는 참조 링크
- 2회+ 반복 패턴만 playbooks/templates/knowledge에 역류. 단건은 보류하고 다음 회차 재관찰

**경고**: 병렬 실행이 "더 빠른 과적합"으로 작동하지 않도록 교차 분석 시 **보류 건도 반드시 기록**하고, 다음 회차 산출물 분량 분포 같은 오버핏 지표를 모니터링한다.

### 3. 산출물을 runs/로 이동

```bash
mkdir -p scenarios/$SCENARIO/runs/$(date +%F)_diagnose
mv outputs/$(date +%F)_diagnosis.md scenarios/$SCENARIO/runs/$(date +%F)_diagnose/output.md
```

### 4. 독립 verifier 에이전트로 평가

`verifier-prompt.md`의 템플릿을 채워 Claude Code의 Agent tool로 실행:

```
subagent_type: general-purpose
prompt: (verifier-prompt.md 템플릿을 이 시나리오·rubric·output으로 채운 내용)
```

verifier는 `evaluation.md`를 반환한다. `runs/{date}_{playbook}/evaluation.md`에 저장.

### 5. 실패 항목을 플레이북/지식으로 역류 (Compounding)

`evaluation.md`에서 FAIL로 찍힌 항목이 있으면:

- 플레이북 절차가 부족 → `playbooks/*.md` 개선
- 지식/원칙이 모호 → `knowledge/*.md` 보강
- 템플릿이 유도하지 않음 → `templates/*.md` 보강

수정 후 같은 시나리오를 다시 돌려서 **재평가 시 FAIL이 PASS로 바뀌는지** 확인한다. 이것이 Compounding 루프.

## 루프 성공 기준

- 하나의 시나리오에서 **3회 이내 반복으로 모든 rubric PASS** 도달
- 같은 결함이 2개 이상 시나리오에서 발견되면 → **공통 지식 결함** → `knowledge/principles.md`에 반영
- 시나리오 하나만 통과해서는 안 된다 — 최소 3개 시나리오 통과 시 "플레이북 검증 완료"로 간주

## 주의

- 시나리오 context는 **모두 가상 데이터**다. 실제 회사와 이름·수치 유사성은 우연.
- 시나리오는 `compensation-data.md`에 숫자가 있지만 **전부 가상**. 외부 공유 제약 없음.
- 실전 실행 전 `context.real.bak` 복원을 반드시 확인한다.

## 확장

- 새 시나리오 추가: `s6-*` 디렉토리 + `expected.md` 작성
- 새 플레이북에 대응하는 rubric 추가: `rubric.md` 하단에 섹션 신설
- 자동화 훅 추가 시 (향후): `.claude/hooks/` 도입 후 `run.sh` 래퍼 스크립트 작성
