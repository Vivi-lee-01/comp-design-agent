# Knowledge → 소비자 전파 규율

본 문서는 `knowledge/*.md`(principles.md, benchmarks.md, glossary.md 등) **지식 문서가 변경될 때**, 그 변경이 **소비자 레이어**(rubric, playbooks, templates)로 **편집 시점에** 함께 전파되도록 강제하는 **세션 운영 가드**다.

지식 층(canonical source)과 소비자 층(체크리스트·판정 기준) 간 드리프트는 **조용히 쌓인다**. 지식은 갱신됐는데 체크리스트는 옛날 수치/목록을 쓰고 있는 상태. 이 드리프트는 verifier가 자발 감지(`.claude/rules/compounding.md` §1)하기 전까지 산출물 커버리지 누락을 만든다.

## 1. 근거 (승격 히스토리)

- **8회차** (design-diagnose × 4): s3 verifier가 `scenarios/rubric.md` D-2 "5개" vs `knowledge/principles.md` §안티패턴 **6개** 불일치를 자발 감지 → rubric D-2 동적 참조("등재 전체(현 6개)")로 수정. cross-layer 드리프트 **1회차 관찰**.
- **9회차** (조치 B 사전 조사): `playbooks/diagnose.md` Step 3 안티패턴 체크리스트가 **5개**만 있고 `principles.md` §안티패턴 **6개**를 못 따라감(`analysis-without-action` 누락) 발견. 동일 본질 드리프트 **2회차 재현** (소비자 층만 playbook 으로 다름).

`.claude/rules/compounding.md` §1("2회+ 반복 패턴 승격") 조건 충족 → rules 층으로 승격. 9회차 조치 B-split의 C 단계 공식 도입.

## 2. 핵심 원칙

### 2.1 Knowledge 변경 = 소비자 스캔 의무

`knowledge/*.md`를 편집했다면, 그 편집이 영향을 주는 **소비자 파일 전체**를 스캔한 뒤 편집을 마감한다. 소비자 영역과 조회 경로:

| 소비자 층 | 대표 파일 | 전파 대상 |
|----------|-----------|----------|
| 형식 | `scenarios/rubric.md` | 체크 항목 문구·수치(특히 D-1·D-2·D-3) |
| 절차 | `playbooks/*.md` | 체크리스트·스캔 대상 목록(diagnose.md Step 3·4 등) |
| 산출 | `templates/*.md` | 기재 항목 수·섹션 구성 |

스캔 없이 지식만 편집 → **조용한 드리프트 발생**.

### 2.2 소비자 측 참조 문구는 **동적 참조**로 유지

하드코딩 수치("5개", "6개") 대신 **동적 참조 패턴**을 사용한다.

- 표준 형태: `` `knowledge/{file}.md` §{section} **등재 전체(현 N개)** ``
- "(현 N개)" 괄호는 읽는 사람을 위한 현재 상태 안내. 본질은 **"등재 전체"** 선언이 verifier·executor로 하여금 원천 문서를 조회하도록 만드는 데 있음.
- 이미 적용된 예: `scenarios/rubric.md` D-1·D-2·D-3 (9회차 B 단계에서 일관화 완료).

### 2.3 Rubric.md 상단의 "Knowledge 의존성 박스"가 Single Source of Truth

소비자 파일이 여럿이어도 **의존 매핑은 한 곳**(`scenarios/rubric.md` 상단 박스)에만 기술한다.

- knowledge 편집 시 **이 박스부터** 갱신 → 이후 rubric 본문 / playbook / template 본문 동기화.
- 박스가 최신이 아니면 이 rule 위반의 **1차 신호**.
- 새로운 knowledge ↔ 소비자 매핑이 추가되면 박스에 **행(row) 추가**로만 확장 (별도 문서 신설 금지 — SSOT 파괴).

## 3. 자가 체크 4문항 (knowledge/*.md 편집 마감 시 수행)

- [ ] `scenarios/rubric.md` 상단 "Knowledge 의존성 박스"의 해당 수치·참조가 이번 편집 이후 상태와 일치하는가?
- [ ] 영향 받는 `playbooks/*.md` 체크리스트(예: `diagnose.md` Step 3·4 체크박스 목록)를 스캔했고 일관되게 갱신했는가?
- [ ] 영향 받는 `templates/*.md` 기재 항목이 있는가? 있다면 갱신했는가?
- [ ] 소비자 측 참조 문구가 하드코딩 수치가 아닌 **동적 참조**("등재 전체", "최신 기준")로 작성되어 있는가?

4문항 중 하나라도 No면 편집을 마감하지 말고 해당 소비자 파일을 먼저 보완한다.

## 4. 안티패턴 (금지)

1. **Knowledge-only 편집**: `knowledge/principles.md`만 고치고 소비자 스캔 건너뛰기. → 드리프트의 대표 발생 경로.
2. **하드코딩 고집**: 소비자 측 참조를 "N개" 명시 수치로 유지. → knowledge 확장 때마다 수동 동기화 필요하며 결국 드리프트.
3. **박스 우회**: `rubric.md` 상단 의존성 박스를 갱신하지 않고 rubric 본문 항목만 개별 수정. → SSOT 구조 파괴.
4. **Verifier 의존**: "verifier가 자발 감지하면 그때 고치자" 태도. → compounding §1 "2회+ 재발" 원칙 상 감지까지 최소 2회차 낭비.
5. **부분 전파**: rubric만 갱신하고 playbook 체크리스트 같은 다른 소비자 방치. → 8회차 이후 실제 발생(`analysis-without-action` 누락).

## 5. 플레이북·Rubric 본문과의 관계

각 소비자 파일 본문에는 "Knowledge 의존성" 절차를 **중복 서술하지 않는다**. 의존 매핑은 `scenarios/rubric.md` 상단 박스에만, 전파 절차는 본 rules 파일에만 둔다 (compounding §3 "한 권고 복수 층 중복 반영 금지").

## 6. 롤백 조건 (리스크 신호 감지 시)

rules 층 승격은 되돌리기 어려우므로, 다음 신호가 **2회차+ 연속** 관찰되면 재검토한다.

- **형식적 완주**: knowledge 편집 시 자가 체크 4문항이 모두 ✅ 체크됐으나 실제로 드리프트 발견·수정 사례 **0건** (체크리스트가 "선언만 하고 작동 안 함").
- **박스 방치**: `rubric.md` 상단 의존성 박스가 knowledge 편집과 무관하게 **수정 안 됨**으로 지나간 패턴.
- **자발 감지율 역전**: 본 rule 도입 후에도 verifier 쪽 rubric 드리프트 자발 제기 건수가 감소하지 않거나 오히려 증가 → 사전 절차가 실효 없다는 신호.

이 중 2건 이상 2회차 연속 관찰 시 본 규율을 부분 개정 또는 조건부 작동으로 재설계.

---

*본 룰은 `.claude/rules/compounding.md` §1(2회+ 재발 승격)·§3(층위 구분)에 의거한 rules 층 신규 승격. 9회차 조치 B-split의 C 단계로 공식 도입.*
*관련: `scenarios/rubric.md` 상단 "Knowledge 의존성 박스"(자가 문서화 스냅샷), `.claude/rules/scope-discipline.md`(동류 rules 선례).*
