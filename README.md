# Compensation Design Agent Knowledge Base

평가보상 시스템을 **설계할 AI 에이전트**가 참조할 지식 베이스 및 작업 절차 모음.

## 목적

에이전트가 다음 작업을 수행할 수 있도록 지원:

1. 현 평가보상 제도 **진단** 및 개선안 제시
2. **페이밴드 / 직무 레벨링** 같은 특정 산출물 설계
3. **범용 설계**: 다양한 시나리오에 대응

## 누구를 위한 것인가

- HR 전문가가 **설계 에이전트**를 구성할 때
- Claude Code / Claude Project / Skill 어떤 형태로도 활용 가능

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

`scenarios/` 디렉토리는 **5개 가상 회사**(초기 스타트업 40명 ~ B2B edtech 80명 등)를 포함하여 플레이북·지식의 일반화 여부를 검증합니다.

- 사용자가 `scenarios/sX/`를 지정하면 루트 `context/` 대신 해당 시나리오의 `context/`를 사용
- 실행 후 `scenarios/verifier-prompt.md`로 독립 verifier 호출 → 자기확증 편향 방지
- 병렬 실행: 여러 시나리오 executor를 동일 메시지에서 dispatch → 하네스의 compounding 루프 가동

## 세션 운영 룰 (`.claude/rules/`)

이 리포는 **도메인 지식(`knowledge/`)**과 **Claude 세션 운영 가드(`.claude/rules/`)**를 책임 분리합니다:

- `compounding.md` — verifier 제안을 하네스에 역류할 때의 판단 원칙 (2회+ 재발만 승격)
- `scope-discipline.md` — 모든 플레이북 공통 "§0 Scope 판정" 5단계
- `knowledge-sync.md` — knowledge 편집 시 소비자 층(rubric·playbook·template) 전파 의무

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
