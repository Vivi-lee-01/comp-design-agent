# Playbook: Full System Design

평가보상 시스템을 **처음부터 전체 재설계**하는 대규모 프로젝트 절차.

## 실행 조건

- 경영진 합의 확보
- HR 리소스 배정
- 3~6개월 프로젝트 기간 확보

## 전체 흐름

```
Phase 0: 준비
   ↓
Phase 1: 진단 (diagnose.md)
   ↓
Phase 2: 철학 정립
   ↓
Phase 3: 레벨링 설계 (design-leveling.md)
   ↓
Phase 4: 페이밴드 설계 (design-pay-band.md)
   ↓
Phase 5: 평가 사이클 설계 (design-review-cycle.md)
   ↓
Phase 6: 통합 검증
   ↓
Phase 7: Rollout
```

## Phase 0: 준비 (2~4주)

### 이해관계자 확보
- 경영진 스폰서
- HR 리더 (프로젝트 오너)
- 각 부서 리더 (자문)
- 구성원 대표 (피드백)

### 프로젝트 스코프 정의
- 전 영역인가 일부인가?
- 기존 제도 전면 폐기인가 단계적 개선인가?
- 목표 완료 시점

### 리소스 확보
- 예산 (컨설팅 / 데이터 구매 / 도구)
- HR 팀 공수
- 외부 파트너 (필요 시)

### 기존 컨텍스트 수집
- `context/` 디렉토리 전체 채우기
- 구성원 서베이 (현 제도 만족도)
- 최근 이탈자 exit interview 데이터

## Phase 1: 진단 (3~4주)

`playbooks/diagnose.md` 실행.

**산출물**: Diagnosis Report

**Decision Point**: 전면 재설계가 정말 필요한지 재확인. 부분 개선으로 충분하면 개별 플레이북으로 분기.

## Phase 2: 철학 정립 (2~3주)

### 경영진 워크숍
`knowledge/compensation/pay-philosophy.md` 의 7개 구성요소에 대해 합의.

1. Market Positioning
2. Pay Mix
3. Pay for Performance 정도
4. Internal Equity vs Market Responsiveness
5. Transparency Level
6. Geographic Differentiation
7. Review Cadence

### 산출물
**Pay Philosophy Statement** (1~2페이지)

이 문서는 이후 모든 설계의 **헌법** 역할. 합의 없으면 진행 금지.

## Phase 3: 레벨링 설계 (4~6주)

`playbooks/design-leveling.md` 실행.

**산출물**:
- Job Family 정의
- Level Matrix (직군 x 레벨 x 4대 축)
- 승급 기준
- 현직자 매핑

**주의**: 레벨링은 **정치적으로 가장 민감**한 단계. 현직자 매핑 시 저항 예상.

## Phase 4: 페이밴드 설계 (4~6주)

`playbooks/design-pay-band.md` 실행.

**선행 조건**: Phase 3 레벨링 완료.

**산출물**:
- Pay Band Table (직군 x 레벨 x 지역)
- Compa Group 체계
- 현직자 보상 매핑
- 이탈자 조정 계획
- 연간 갱신 프로세스

**주의**: 예산 영향이 가장 크게 드러나는 단계. 경영진 지속 조율 필요.

## Phase 5: 평가 사이클 설계 (4~6주)

`playbooks/design-review-cycle.md` 실행.

**병행 가능**: Phase 4와 일부 병행 가능하나, 평가-보상 연결 부분은 Phase 4 완료 후 확정.

**산출물**:
- Review Cycle Design
- 평가 양식
- Calibration 프로세스
- 매니저 가이드
- 도구 선정

## Phase 6: 통합 검증 (2~3주)

### 전체 일관성 점검

- [ ] 철학 ↔ 레벨링 ↔ 페이밴드 ↔ 평가 사이클이 **일관된 논리**인가?
- [ ] 한 요소 변경 시 다른 요소에 미칠 영향 예측 가능한가?
- [ ] 구성원에게 **설명 가능한 스토리**가 되는가?

### End-to-End 시뮬레이션

가상 구성원 5~10명 케이스로:
1. 입사 시 offer
2. 첫 평가
3. 승급 또는 유지
4. 이탈 시 retention offer

각 시나리오가 설계대로 작동하는지 검증.

### 법무 검토
- 노동법 준수
- 차별 금지
- 프라이버시

### 재무 검토
- 연간 예산 영향
- 3~5년 시뮬레이션

## Phase 7: Rollout (3~6개월)

### 커뮤니케이션

#### 전사 발표
- 배경: 왜 바꾸는가
- 철학: 어떤 원칙으로 설계했는가
- 주요 변화: 무엇이 달라지는가
- 개인 영향: 본인에게 미치는 영향
- FAQ

#### 1:1 매핑 통보
- 개인별 레벨
- 개인별 밴드
- 보상 조정 (있다면)

### 매니저 교육

- 1on1 효과적 운영
- 피드백 전달법
- Calibration 참여
- 어려운 대화 (등급 통보, 밴드 외 케이스)

### 첫 사이클 운영

- 신중하게 운영
- 매주 진행 상황 점검
- 이슈 실시간 대응

### 피드백 수집 및 개선

- 첫 사이클 후 서베이
- 매니저 회고
- 프로세스 개선 제안

## 리스크 관리

### 예상되는 저항

1. **기존 상위 레벨자**: 새 체계에서 다운레벨링 가능성 → Red Circle 방식 활용
2. **협상력 있던 구성원**: 밴드 상한 초과 케이스 → 동결 설명
3. **매니저**: 운영 부담 증가 → 교육 및 도구 지원
4. **구성원 전반**: 불확실성 → 투명한 커뮤니케이션

### 중단 판단 기준

다음 상황에서는 **프로젝트 일시 중단** 검토:

- 핵심 인재의 집단 이탈 조짐
- 경영진 합의 붕괴
- 예산 제약 극심
- 외부 환경 급변 (예: 펀딩 위기)

## 성공 지표

6개월 후 측정:
- 이탈률 변화
- 구성원 eNPS
- 평가 만족도 서베이
- Offer accept rate
- 페이 갭 개선 정도

## 관련 파일

모든 플레이북 참조:
- `playbooks/diagnose.md`
- `playbooks/design-leveling.md`
- `playbooks/design-pay-band.md`
- `playbooks/design-review-cycle.md`

모든 knowledge 디렉토리 참조.
