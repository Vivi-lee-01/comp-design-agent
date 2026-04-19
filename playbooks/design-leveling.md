# Playbook: Design Job Leveling

직무/레벨 체계를 설계하는 절차.

## 실행 조건

- `context/company-profile.md` 의 조직 규모/구성 파악
- `context/roles-and-levels.md` 의 현재 상태 파악

## 산출물

- **Leveling Matrix** (`templates/leveling-matrix-template.md` 형식)
- 레벨별 기대치 문서
- 승급 기준
- 현직자 매핑 (있다면)

## 단계

### Step 1: 지식 로드

에이전트는 순서대로 읽는다:

1. `knowledge/compensation/leveling.md` — 이론
2. `knowledge/principles.md` — 원칙
3. `context/company-profile.md` — 맥락
4. `context/roles-and-levels.md` — 현 상태

### Step 1-보강 (Scope 판정)

본 플레이북 진입 전 `.claude/rules/scope-discipline.md`의 §0 Scope 판정 5단계를 수행하라. "레벨 구조는 유지하되 재보정"형 시나리오에서는 **축소** 판정이 기본값이다.

### Step 2: Job Family 정의

#### 2-1: 직군 목록 확정

현재 실제 업무를 기준으로 **5~10개** 직군으로 grouping.

**판단 기준**:
- 필요 역량의 유사성
- 평가 축의 공통성
- 성장 경로의 유사성

**안티패턴**:
- 지나친 세분화 (예: Frontend/Backend 별도 분리, 30명 조직에서)
- 지나친 통합 (예: "Tech"로 엔지니어/데이터/디자인 묶기)

#### 2-2: 직군 간 경계 정의

모호한 케이스 처리:
- Engineering Manager는 Engineering인가 Management인가?
- 풀스택 개발자는?
- Product Designer는 Design인가 Product인가?

**원칙**: 대부분의 업무 시간이 투입되는 영역으로 분류.

### Step 3: Level 수 결정

`leveling.md` 가이드:
- < 30명: 3~4 레벨
- 30~100명: 4~5 레벨
- 100~500명: 5~7 레벨
- 500명+: 7~10 레벨

**우리 조직 규모에 맞춰 결정**.

### Step 4: Dual Track 설계

IC / Manager 트랙 분리.

**매핑 원칙**:
- 같은 숫자 레벨 = 동등한 가치/보상
- M1은 IC3와 동급 (첫 매니저 레벨)
- 일반적으로 M 트랙이 IC 트랙보다 **짧다** (더 높은 레벨에만 존재)

**예시**:
```
IC1  
IC2  
IC3  ↔  M1 (Team Lead)
IC4  ↔  M2 (Manager)
IC5  ↔  M3 (Senior Manager)
IC6  ↔  M4 (Director)
```

### Step 5: 4대 축 기대치 정의

각 (직군 x 레벨) 조합에 대해 4대 축으로 기대치 기술:

1. **Scope of Impact**: 영향 범위
2. **Autonomy**: 자율성 수준
3. **Complexity**: 다루는 문제 복잡도
4. **Influence**: 타인/조직에 대한 영향력

**작성 가이드**:
- **관찰 가능한 행동**으로 기술
- 구체적 예시 포함
- 모호한 표현("리더십", "오너십") 최소화

**예시 (Engineering IC3)**:
> **Scope**: 한 팀의 기능을 end-to-end로 소유 (설계~배포~모니터링)
> **Autonomy**: 요구사항을 받으면 기술 설계부터 자율 수행. 막히면 도움 요청.
> **Complexity**: 기존 시스템과의 통합, 레거시 마이그레이션 수준
> **Influence**: 팀 내 코드 리뷰 주도, 신입 온보딩 지원
> **구체적 예시**: "결제 모듈 리팩토링을 2주 내 혼자 설계하고 배포"

### Step 6: 승급 기준 정의

각 레벨 → 다음 레벨 조건:

- **최소 재직 기간**: 현 레벨에서 최소 N개월
- **지속적 성과**: 최근 N회 평가에서 기대치 이상
- **다음 레벨 역량 입증**: 이미 그 레벨처럼 일하고 있다는 증거
- **승급 심사**: 매니저 추천 + 패널 리뷰 or calibration

### Step 7: 현직자 매핑

현 구성원을 새 레벨 체계로 매핑.

**프로세스**:
1. 각 매니저가 팀원 초안 매핑
2. 직군 내 calibration
3. 전사 calibration
4. 이견 조정 (특히 다운레벨링 케이스)

**주의**:
- 다운레벨링은 매우 조심스럽게
- 기존 급여는 유지하되 레벨만 조정 ("red circle" 방식)
- 본인에게 납득 가능하게 설명

### Step 8: 타사 매핑 (참고)

구성원이 외부와 비교할 수 있도록 타사 레벨 참고 매핑.

| 우리 조직 | Google | Meta | 국내 대기업 |
|-----------|--------|------|-------------|
| IC3 | L4 | E4 | 대리/과장 |

**주의**: 이 매핑은 참고용. 실제 역할이 100% 일치하지 않을 수 있음.

### Step 9: 산출물 작성

`templates/leveling-matrix-template.md` 형식으로 작성.

## 체크포인트

- [ ] 산출물 §0에 Scope 판정 섹션이 명시되었는가 (다룸/축소/생략/강화 분류 + 근거 인용)
- [ ] scope 외로 선언된 항목은 이관 대상이 명시되었는가
- [ ] 모든 직군에 동일 레벨 구조가 적용되는가?
- [ ] Dual track이 대칭적인가? (IC 우대/홀대 없음)
- [ ] 각 레벨 기대치가 **관찰 가능한 행동**인가?
- [ ] 승급 기준이 **모호하지 않은가**?
- [ ] 현직자 매핑에 **정당화 근거**가 있는가?

## 사용자 확인 지점

1. **Step 2 (Job Family) 완료 후**: 직군 분류에 동의하는지
2. **Step 3 (Level 수) 완료 후**: 레벨 수가 적정한지
3. **Step 5 (기대치) 초안 작성 후**: 직군별 전문가 검토 요청
4. **Step 7 (매핑) 전**: 매핑 방식 합의
5. **최종 산출물 전**: 전체 검토

## 관련 파일

- `knowledge/compensation/leveling.md`
- `knowledge/principles.md`
- `templates/leveling-matrix-template.md`
- `playbooks/design-pay-band.md` (레벨링 완료 후 페이밴드)
