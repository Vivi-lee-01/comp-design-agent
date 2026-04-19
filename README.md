# Compensation Design Agent Knowledge Base

**자기 회사에 딱 맞는 평가보상 제도를 설계·보완**하기 위한 개인용 하네스.

## 한 줄 개요

> **범용 엔진**(지식·플레이북·템플릿) + **회사별 연료**(`context/`) = **우리 회사 맞춤 산출물**

SaaS 제품이 아닙니다. 사용자가 자기 회사 데이터를 `context/`에 채우면, AI 에이전트가 범용 자산(7원칙·안티패턴·플레이북·템플릿)을 적용하여 **그 회사 고유의 제도 설계안**을 생성하는 구조입니다.

## 하네스 3축 (재료 · 설계 · 교정)

파일이 많아 보이지만 모든 자산은 세 축 중 하나에 속합니다.

| 축 | 역할 | 핵심 자산 |
|----|------|----------|
| **재료축** | 제도 설계에 들어가는 지식·맥락을 정돈 | `knowledge/` (7원칙·벤치마크·용어집), `context/` (회사별 연료), `SKILL.md`·`INDEX.md` (라우팅) |
| **설계축** | 설계 행위를 일정한 절차·형식으로 강제 | `playbooks/` (진단·레벨링·페이밴드·평가사이클 절차), `templates/` (1차 마크다운 구조), `.claude/rules/output-delivery.md` (2차 포맷 선제 제안) |
| **교정축** | 하네스가 드리프트·오버핏 없이 스스로 개선되도록 유지 | `.claude/rules/compounding.md` (승격 판단), `scope-discipline.md` (§0 Scope 5단계), `knowledge-sync.md` (층간 전파), `scenarios/` (검증 루프) |

> **왜 축으로 나누는가**: 하네스를 **점검·확장**할 때 "이 변경이 어느 축을 건드리는가"로 분류하면 영향 범위가 바로 보입니다. 예: knowledge 수정은 재료축이지만 소비자 스캔 의무(`knowledge-sync.md`)를 건드리므로 교정축 동시 확인 필요.

## 목적

사용자 회사 맥락에서 다음을 수행:

1. **진단** — 현 평가보상 제도의 결함·안티패턴·우선순위 파악
2. **설계** — 페이밴드 / 직무 레벨링 / 평가 사이클의 초안 생성 및 반복 개선
3. **전환 설계** — 기존 제도가 있는 조직의 단계적 개편 로드맵

## 누구를 위한 것인가

**자기 회사 데이터를 가진 HR 실무자**. 회사 규모·업종·단계 무관.

- 시리즈 A~C 스타트업 HR Lead (1~3인 HR 조직)
- 중견기업 인사팀 제도 담당자
- 제도 개편을 처음 혼자 주도하는 담당자
- 컨설팅 없이 내부에서 설계·설득 자료까지 밀어야 하는 실무자

### 특히 잘 맞는 경우

- 제도 설계 경험이 부족해서 **"무엇을 놓치면 안 되는지" 체크리스트**가 필요한 상황
- 초안은 머릿속에 있는데 **경영진 설득 문서 작성 비용**이 병목
- 컨설팅 예산 없이 **회사 맞춤 제도를 내부에서 만들어야 함**
- 여러 방향성을 **빠르게 시뮬레이션**하며 감을 잡고 싶음

### 약간 주의할 점

- **데이터 품질 = 산출물 품질**: `context/` 파일을 부실하게 채우면 그럴듯한 추측만 나옵니다. GIGO 원칙은 여기서도 작동
- **벤치마크 수치는 외부 검증 필수**: 에이전트가 생성하는 시장 데이터(Levels.fyi p50 등)는 **가설치**. 실제 구독 데이터나 업계 네트워크로 반드시 보정
- **정치 맥락 섹션은 입력 정보 기반**: CEO 성향·이해관계자 구조를 `context/`에 명확히 기술해야 §6.5가 의미 있는 서술을 함. 모호한 입력에는 모호한 추측이 나옴
- **문화 특수성 기본값**: 현재 `knowledge/`와 예시 시나리오는 **한국·북미 테크 중심**. 제조업·공공·금융·글로벌 멀티리전은 추가 커스터마이징 필요

### 덜 적합한 경우

- **대규모 조직 전사 개편** (1,000명+): 템플릿이 전제하는 데이터·이해관계자 복잡도 초과 — 참고 자산으로는 유효하나 end-to-end 커버는 어려움
- **개별 연봉 협상 같은 미시 업무**: 이건 제도 설계가 아니라 운영 — SKILL.md 첫 줄에서 명시적으로 범위 밖
- **"Claude 셋업이 부담스러움"**: Claude Code / Claude.ai Project / Skill 배포가 진입장벽. 일반 템플릿 자료로만 활용 가능하나 검증 루프는 못 돌림

## 빠른 시작

### 1. Claude Code 프로젝트로 쓰기

```bash
# 이 디렉토리를 Claude Code 프로젝트 루트로 복사
cp -r comp-design-agent ~/projects/

# Claude Code에 CLAUDE.md 추가
cat > ~/projects/comp-design-agent/CLAUDE.md << 'EOF'
이 프로젝트는 평가보상 시스템 설계 에이전트입니다.
작업 시작 전 반드시 SKILL.md 와 INDEX.md 를 먼저 읽으세요.
EOF

cd ~/projects/comp-design-agent
claude
```

### 2. Claude.ai Project로 쓰기

1. 이 디렉토리를 zip으로 압축
2. Claude.ai에서 새 Project 생성
3. zip 파일의 모든 .md 파일을 Project Knowledge에 업로드
4. Project의 Custom Instruction에 다음 추가:
   ```
   당신은 평가보상 시스템 설계 에이전트입니다.
   작업 요청 시 SKILL.md 와 INDEX.md 를 먼저 참조하고,
   적합한 playbook을 따라 작업을 수행하세요.
   ```

### 3. Skill로 쓰기

```bash
# Skill 위치로 이동
mv comp-design-agent ~/.claude/skills/comp-design
# 또는 프로젝트별로
mv comp-design-agent /your-project/.claude/skills/comp-design
```

`SKILL.md` 의 frontmatter가 트리거 역할을 합니다.

## 이렇게 씁니다 (실제 흐름)

### 플레이북 4종 — 언제 어떤 걸?

| 플레이북 | 트리거 질문 | 산출물 | 분량 |
|---------|------------|--------|:----:|
| `diagnose.md` | "현 제도 뭐가 깨져있어?" | 안티패턴 스캔 + 7원칙 점수 + 우선순위 로드맵 | ~500줄 |
| `design-leveling.md` | "레벨 체계 다시 짜자" | Leveling Matrix (4축·직군별·승급기준·현직자 매핑) | ~400줄 |
| `design-pay-band.md` | "밴드 만들어줘" | Min/Mid/Max 페이밴드 + Compa Group + 재원 영향 | ~450줄 |
| `design-review-cycle.md` | "평가 사이클 설계" | Cadence·calibration·compensation link·career dialogue | ~500줄 |
| `full-design.md` | "처음부터 설계해줘" | 위 4개를 순차 실행 (diagnose → leveling → pay-band → review) | 대형 |

### end-to-end 예시 (레벨링)

```
Step 1. context/ 5개 파일을 자기 회사 데이터로 채우기
        - company-profile.md  (조직 개요)
        - current-system.md   (현 제도)
        - roles-and-levels.md (현 직무·레벨)
        - compensation-data.md (현 연봉 분포, 민감)
        - constraints.md      (예산·문화·법규·의사결정 구조)

Step 2. Claude에게: "design-leveling 돌려줘"

Step 3. Claude가 자동으로:
        - SKILL.md → INDEX.md → playbooks/design-leveling.md 순 로드
        - §0 Scope 판정 (scope-discipline.md 규율 적용)
        - context/ 데이터 교차 참조
        - templates/leveling-matrix-template.md 형식에 맞춰 생성

Step 4. outputs/2026-04-19_leveling.md 저장

Step 5. (신규) Claude가 후속 포맷 질문:
        "PPT / Notion / PDF / 슬랙 / 이메일 / 그대로 중 어느 형태로 드릴까요?"

Step 6. (선택) 시나리오 검증으로 품질 확인
        verifier-prompt.md 템플릿으로 독립 verifier 호출 → evaluation.md
```

### 첫 사용 추천 경로

| 상황 | 시작점 |
|------|--------|
| 기존 제도 있고 뭐가 문제인지 확인부터 | `diagnose.md` 먼저 → 결과 보고 다음 단계 결정 |
| 제도 자체를 새로 짜야 함 | `full-design.md` (diagnose → leveling → pay-band → review 순차) |
| 특정 영역만 급함 (예: 페이밴드만) | 해당 플레이북 단독 실행, 단 선행 조건(레벨 체계)은 확인 |
| 하네스 자체 감을 잡고 싶음 | `scenarios/` 5개 중 자기 회사와 규모/업종 유사한 시나리오 실행 |

## 디렉토리 구조

```
comp-design-agent/
├── SKILL.md              # 에이전트 진입점 (Skill frontmatter 포함)
├── INDEX.md              # 파일 라우팅 맵
├── README.md             # 이 파일
├── CLAUDE.md             # 작업 시작 규칙 (Claude Code용)
├── knowledge/            # 범용 지식 (회사 무관)
│   ├── principles.md
│   ├── glossary.md
│   ├── benchmarks.md
│   ├── performance/
│   │   ├── okr.md
│   │   ├── mbo.md
│   │   ├── review-cycles.md
│   │   └── feedback-systems.md
│   └── compensation/
│       ├── pay-philosophy.md
│       ├── pay-bands.md
│       ├── leveling.md
│       ├── market-benchmark.md
│       └── equity.md
├── context/              # 회사 고유 컨텍스트 (gitignore, 사용자가 채움)
│   ├── company-profile.md
│   ├── current-system.md
│   ├── roles-and-levels.md
│   ├── compensation-data.md
│   └── constraints.md
├── playbooks/            # 작업 절차
│   ├── diagnose.md
│   ├── design-leveling.md
│   ├── design-pay-band.md
│   ├── design-review-cycle.md
│   └── full-design.md
├── templates/            # 산출물 템플릿
│   ├── diagnosis-report-template.md
│   ├── pay-band-template.md
│   ├── leveling-matrix-template.md
│   └── review-cycle-template.md
├── scenarios/            # 가상 회사 5종 (검증 루프용)
│   ├── README.md         # 시나리오 실행 규약
│   ├── rubric.md         # 산출물 평가 기준
│   ├── verifier-prompt.md
│   ├── s1-early-stage-startup-40/
│   ├── s2-negotiation-heavy-300/
│   ├── s3-remote-global-120/
│   ├── s4-pre-ipo-tech-200/
│   └── s5-b2b-edtech-80/
└── .claude/rules/        # 세션 운영 가드 (Claude가 지킬 룰)
    ├── compounding.md
    ├── scope-discipline.md
    └── knowledge-sync.md
```

## 첫 사용 체크리스트

에이전트를 실전 투입하기 전:

- [ ] `context/company-profile.md` 채우기
- [ ] `context/current-system.md` 채우기
- [ ] `context/roles-and-levels.md` 채우기
- [ ] `context/constraints.md` 채우기
- [ ] `context/compensation-data.md` 채우기 (민감, 선택)

컨텍스트가 비어있으면 에이전트는 **사용자에게 질문**으로 정보를 수집합니다.

## 민감 정보 관리

### `.gitignore` 정책

이 리포는 다음을 git 추적에서 제외합니다:

- `context/*` — 회사 고유 정보 (연봉·현 제도·직무·제약)
- `outputs/` — 산출물 (개별 연봉·평가 포함 가능)
- `scenarios/*/runs/` — verifier 실행 결과 (내부 실험 로그)
- `experiments/` — 하네스 회차별 실험 로그 (세션 컨텍스트)
- `.claude-handoff.json` — 세션 상태
- `.harness/` — 진단 리포트 (로컬 전용)

표준 보안 블록(`.env`, `*.key`, `credentials/`, `secrets/`)은 기본 포함.

### 공유 시 주의
- 외부 공유 시 `context/` 디렉토리 반드시 제외
- `knowledge/`, `playbooks/`, `templates/`, `scenarios/` (가상 데이터)만 공유 가능

## 시나리오 기반 검증 루프

`scenarios/` 디렉토리는 **5개 가상 회사**(초기 스타트업 40명 ~ B2B edtech 80명 등)를 포함하여 플레이북·지식의 일반화 여부를 검증합니다. **사용자가 자기 회사에 쓸 때는 `context/` 를 사용**하므로 시나리오는 실제 사용과 분리된 **하네스 자체의 검증 베드**입니다.

- 사용자가 `scenarios/sX/`를 지정하면 루트 `context/` 대신 해당 시나리오의 `context/`를 사용
- 실행 후 `scenarios/verifier-prompt.md`로 독립 verifier 호출 → 자기확증 편향 방지
- 병렬 실행: 여러 시나리오 executor를 동일 메시지에서 dispatch → 하네스의 compounding 루프 가동
- 사용자는 시나리오로 **감 잡기**에 쓰거나 무시하고 자기 `context/`로 바로 가도 OK

## 산출물 형태와 후속 변환

### 1차 산출물 — 마크다운 고정

플레이북 실행 결과는 **언제나 마크다운 파일**로 생성됩니다:

- 실전: `outputs/YYYY-MM-DD_{playbook}.md`
- 시나리오: `scenarios/{slug}/runs/YYYY-MM-DD_{playbook}/output.md`

템플릿의 분량 가드·자가 체크리스트·구조 강제가 마크다운 기준으로 설계되어 있어, **1차는 마크다운이 고정값**입니다. (템플릿 세부: `templates/*.md`)

### 2차 변환 — 사용자 선택

산출물 저장 완료 후, Claude가 후속 포맷 선호를 선제 질문합니다 (자동):

| 포맷 | 용도 | 변환 방식 |
|------|------|-----------|
| **PPT 슬라이드** | 경영진 보고·외부 설득 | Exec Summary + 7원칙 + 우선순위 + 로드맵 각 1장 + 정치 맥락 2-3장 |
| **Notion 문서** | 사내 공유·협업 | 섹션별 toggle, 표 보존, 체크박스 유지 |
| **PDF 인쇄용** | 이사회 자료·법무 검토 | 요약 1p + 본문 + 부록 분리 |
| **슬랙 mrkdwn** | 팀·경영진 초안 알림 | 600자 내외 핵심 요약 |
| **이메일 보고서** | 의사결정자 공식 요청 | Exec Summary 본문 + 상세 첨부 |
| **그대로** | 1차 산출물만 필요 | 추가 변환 없음 |

### §6.5 정치 맥락 보호

진단 리포트에 포함되는 **§6.5 정치 맥락·공개 순서·리스크 로그**는 민감도가 높아 2차 포맷 변환 시 별도 규약 적용:

- 내부 Notion/PDF → 원본 유지
- 경영진 PPT → 포함 여부 재확인
- 공개 PDF/슬랙/이메일 → 기본 제외, 명시 요청 시에만 포함

상세 규율은 `.claude/rules/output-delivery.md`.

## 세션 운영 룰 (`.claude/rules/`)

이 리포는 **도메인 지식(`knowledge/`)**과 **Claude 세션 운영 가드(`.claude/rules/`)**를 책임 분리합니다:

- `compounding.md` — verifier 제안을 하네스에 역류할 때의 판단 원칙 (2회+ 재발만 승격)
- `scope-discipline.md` — 모든 플레이북 공통 "§0 Scope 판정" 5단계
- `knowledge-sync.md` — knowledge 편집 시 소비자 층(rubric·playbook·template) 전파 의무
- `output-delivery.md` — 산출물 마감 시 후속 포맷(PPT/Notion/PDF/슬랙/이메일) 선제 제안 의무

## 확장 방법

### 새 playbook 추가
1. `playbooks/` 에 새 파일 생성
2. `INDEX.md` 의 라우팅 맵에 추가
3. `SKILL.md` 의 작업 유형 테이블에 추가

### 새 지식 영역 추가
1. `knowledge/` 에 새 하위 디렉토리 생성
2. `SKILL.md` 의 디렉토리 구조 섹션 업데이트
3. 관련 playbook의 "지식 로드" 단계에 추가

### 회사별 커스터마이징
- `knowledge/` 수정 금지 (범용 자산)
- `context/` 만 수정
- 회사 특수 playbook이 필요하면 `playbooks/custom/` 하위에

## 버전

- v0.3 (2026-04-19): README 포지셔닝 재정립(범용 엔진 + 회사별 연료), 산출물 후속 포맷 선제 제안 룰 `output-delivery.md` 추가
- v0.2 (2026-04-19): `.claude/rules/` 3종 도입, scenarios 5종 확장, compounding 루프 확립
- v0.1 (2026-04-18): 초기 릴리즈

## 향후 확장 아이디어

- [ ] 산업별 특화 knowledge (핀테크/헬스케어 등)
- [ ] 국가별 특화 knowledge (미국/일본 등)
- [ ] 업무 자동화 스크립트 (벤치마크 수집 등)
- [ ] 검증 테스트 케이스 (에이전트 출력 품질 측정)

## 라이선스

별도 LICENSE 파일 미지정. 공개 시 조직 정책에 따라 추가.

---

*`knowledge/`, `playbooks/`, `templates/`는 회사 무관 범용 자산. `context/`는 회사 고유 정보로 별도 관리합니다.*
