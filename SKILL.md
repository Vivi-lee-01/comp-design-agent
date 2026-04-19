---
name: comp-design
description: Use this skill when designing, diagnosing, or iterating on performance evaluation and compensation systems. Triggers include requests to design pay bands, define job levels/leveling frameworks, build compensation calculators, diagnose current comp/eval systems, map OKR/MBO frameworks, design performance review cycles, or produce compensation-related deliverables (salary tables, leveling matrices, review templates). Do NOT use for payroll processing, benefits administration, or individual salary negotiation.
---

# 평가보상 시스템 설계 에이전트

평가보상 제도를 설계, 진단, 반복 개선하기 위한 지식 베이스 및 작업 절차.

## 사용 방법

작업 유형을 먼저 식별한 뒤, 해당 플레이북을 따르세요.

### 작업 유형별 진입점

| 사용자 요청 유형 | 참조할 플레이북 |
|------------------|-----------------|
| "현 제도 진단해줘" | `playbooks/diagnose.md` |
| "페이밴드 만들어줘" | `playbooks/design-pay-band.md` |
| "직무 레벨링 설계해줘" | `playbooks/design-leveling.md` |
| "평가 사이클 설계해줘" | `playbooks/design-review-cycle.md` |
| "처음부터 제도 설계해줘" | `playbooks/full-design.md` (diagnose → leveling → pay-band → review-cycle 순차 실행) |

### 지식 베이스 참조 규칙

1. **원칙을 먼저 확인**: `knowledge/principles.md`
2. **작업 영역별 이론**: `knowledge/performance/`, `knowledge/compensation/`
3. **벤치마크가 필요하면**: `knowledge/benchmarks.md`
4. **회사 고유 정보가 필요하면**: `context/` 하위 파일 (존재할 때만)

### 컨텍스트 취급 원칙

- `context/` 디렉토리의 파일은 **해당 회사 전용 정보**입니다
- 에이전트는 설계 시 항상 `context/company-profile.md`를 먼저 읽어 조직 특성을 파악해야 합니다
- 컨텍스트가 부족하면 **추측하지 말고 사용자에게 질문하세요**

## 디렉토리 구조

```
comp-design-agent/
├── SKILL.md                        # 이 파일 (에이전트 진입점)
├── INDEX.md                        # 전체 파일 라우팅 맵
├── knowledge/                      # 범용 지식 (회사 무관)
│   ├── principles.md               # 핵심 설계 원칙
│   ├── glossary.md                 # 용어 사전
│   ├── performance/                # 성과평가 이론
│   │   ├── okr.md
│   │   ├── mbo.md
│   │   ├── feedback-systems.md
│   │   └── review-cycles.md
│   ├── compensation/               # 보상 이론
│   │   ├── pay-philosophy.md
│   │   ├── pay-bands.md
│   │   ├── leveling.md
│   │   ├── equity.md
│   │   └── market-benchmark.md
│   └── benchmarks.md               # 외부 레퍼런스 (GitLab, Buffer 등)
├── context/                        # 회사 고유 컨텍스트 (gitignore 대상)
│   ├── company-profile.md          # 조직 개요
│   ├── current-system.md           # 현 제도
│   ├── roles-and-levels.md         # 직무/레벨 정의
│   ├── compensation-data.md        # 연봉 데이터 (민감)
│   └── constraints.md              # 제약사항 (예산/문화/법규)
├── playbooks/                      # 작업 절차
│   ├── diagnose.md
│   ├── design-pay-band.md
│   ├── design-leveling.md
│   ├── design-review-cycle.md
│   └── full-design.md
└── templates/                      # 산출물 템플릿
    ├── pay-band-template.md
    ├── leveling-matrix-template.md
    ├── diagnosis-report-template.md
    └── review-cycle-template.md
```

## 운용 형태별 활용

- **Claude Code**: 이 디렉토리를 프로젝트로 열고 `CLAUDE.md`에 "comp-design-agent/SKILL.md 참조" 명시
- **Claude.ai Project**: 전체 디렉토리를 zip으로 업로드
- **Skill**: `~/.claude/skills/comp-design/` 또는 `.claude/skills/comp-design/` 에 배치

## 주의사항

- 에이전트는 **설계안을 제안**하지만, 최종 결정은 사람이 합니다
- 개인 연봉 조정 같은 민감한 작업은 일반 설계와 별개로 **사용자 확인을 여러 단계로** 거치세요
- 컨텍스트 파일(`context/`)은 **민감정보 포함 가능성이 높으므로** 외부 공유 시 반드시 제외하세요
