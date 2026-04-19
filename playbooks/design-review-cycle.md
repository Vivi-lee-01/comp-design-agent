# Playbook: Design Performance Review Cycle

평가 사이클을 설계하는 절차.

## 실행 조건

- `context/company-profile.md` 의 조직 규모/문화 파악
- (권장) `context/roles-and-levels.md` 의 레벨 정의

## 산출물

- **Review Cycle Design** (`templates/review-cycle-template.md` 형식)
- 평가 양식
- 일정 캘린더
- 매니저/구성원 가이드

## 단계

### Step 1: 지식 / 컨텍스트 로드

1. `knowledge/performance/review-cycles.md`
2. `knowledge/performance/okr.md` (목표 설정 방식 결정 시)
3. `knowledge/performance/feedback-systems.md`
4. `context/company-profile.md`

### Step 1-보강 (Scope 판정)

본 플레이북 진입 전 `.claude/rules/scope-discipline.md`의 §0 Scope 판정 5단계를 수행하라. Review cycle은 peer feedback·calibration·compensation link·career dialogue 레이어가 공존하므로 특히 **이관 인터페이스(→ pay-band, → leveling)** 명시가 필수다.

### Step 2: 주기 결정

조직 규모와 문화에 맞는 주기 선택:

- **초기 스타트업 (~30명)**: 반기 공식 + 상시 1on1
- **성장기 (~100명)**: 반기 공식, 분기 체크인
- **중견 (~500명)**: 연간 + 중간 체크인
- **대기업**: 연간

### Step 3: 평가 축 정의

3축 구조 권장:

#### Axis 1: What (성과)
- OKR 달성도 / KPI / 프로젝트 성과
- 정량 + 정성 혼합

#### Axis 2: How (역량/행동)
- 조직 가치 실천
- 레벨별 기대 역량 충족 (로딩한 `roles-and-levels.md` 참조)

#### Axis 3: Potential (잠재력) — 선택
- 차기 레벨 가능성
- 승급 후보 판단용

### Step 4: 등급 체계 설계

등급 수 결정:
- 3단계: 단순, 차등 약함
- 5단계: 표준, 균형
- 7단계: 세밀, 관리 부담

**권장**: 5단계 (Far Exceeds / Exceeds / Meets / Below / Far Below)

**분포 가이드** (강제 아님):
- Far Exceeds: ~5%
- Exceeds: ~20%
- Meets: ~60%
- Below: ~10%
- Far Below: ~5%

### Step 5: 사이클 구성 요소 선정

**필수**:
- [ ] Goal Setting
- [ ] Self Review
- [ ] Manager Review
- [ ] Calibration
- [ ] 평가 면담
- [ ] 보상 결정

**선택**:
- [ ] Peer Review
- [ ] 360 Review
- [ ] Mid-cycle Check-in
- [ ] Potential Assessment

### Step 6: 세부 일정 설계

연간 사이클 예시 (반기 기준):

```
[H1 사이클]
1월 1주: H1 목표 설정 개시
1월 4주: 목표 설정 완료
4월 1주: 중간 체크인
5월 4주: Self Review 개시
6월 2주: Manager Review 완료
6월 3주: Calibration
6월 4주: 평가 면담
7월 1주: 보상 결정 통보
7월 2주: H2 목표 설정 개시
...
```

### Step 7: 평가 양식 설계

#### Self Review 양식 구성
- 지난 기간 주요 성과 (3~5개)
- 목표 달성도 (정량)
- 잘한 점 / 개선점 자기 분석
- 다음 기간 포부

#### Manager Review 양식 구성
- 성과 종합 평가 (근거 필수)
- 역량/행동 평가 (루브릭 기반)
- 강점 / 개발 필요 영역
- 종합 등급
- 다음 기간 개발 계획

### Step 8: Calibration 프로세스 설계

#### 참여자
- 매니저급 이상
- HR Business Partner 퍼실리테이터

#### 프로세스
1. 각 매니저가 팀원 잠정 등급 제출
2. 그룹 모임에서 검토
3. 이상 케이스 토론
4. 합의 등급 확정

#### 주의사항
- 순위 매기기 아님
- 조정 시 **근거 필수**
- 결과 기록

### Step 9: 평가 ↔ 보상 연결 방식 결정

세 가지 옵션:

**A. 직접 연동**
- 등급 → 인상률 매트릭스
- 투명, 예측 가능

**B. 느슨한 연동**
- 등급은 참고, 보상은 별도 결정
- 유연함

**C. 분리 (권장)**
- 평가 면담 = 성장 대화 (시점 A)
- 보상 면담 = 결정 통보 (시점 B)
- 사이에 HR/경영진 조정

### Step 10: 매니저 교육 설계

매니저 역량이 제도 성패 결정.

**필수 교육**:
- 1on1 효과적 운영법
- SBI 피드백 모델
- Radical Candor
- Calibration 참여법
- 어려운 대화 (PIP, 등급 통보)

### Step 11: 도구 선택

옵션:
- **Notion + 템플릿**: 저비용, 커스텀
- **Lattice**: 통합 플랫폼, 1on1 강점
- **15Five**: 주간 체크인 강점
- **Culture Amp**: 서베이 강점

조직 규모/예산/기존 도구 고려.

### Step 12: Rollout 계획

단계적 도입:

**Phase 1 (0~3개월)**: 기반 마련
- 제도 확정
- 도구 세팅
- 매니저 교육 1차

**Phase 2 (3~6개월)**: 첫 사이클 운영
- 첫 평가 사이클 실행
- 실시간 피드백 수집

**Phase 3 (6~12개월)**: 정착
- 2회차 사이클 운영
- 프로세스 개선
- 데이터 축적

### Step 13: 측정 지표 정의

제도 성공을 측정:
- Manager 1on1 실시율
- 평가 제출 on-time 비율
- 평가 관련 eNPS
- 성과-보상 상관관계
- 이탈자의 평가 이력 패턴

## 체크포인트

- [ ] 주기가 조직 규모에 적정한가?
- [ ] What/How 축이 분리되어 있는가?
- [ ] Calibration 프로세스가 명확한가?
- [ ] 평가와 보상의 **시간 간격**이 있는가?
- [ ] 매니저 교육 계획이 포함되었는가?
- [ ] 측정 지표가 정의되었는가?

## 사용자 확인 지점

1. **Step 2 (주기) 완료 후**
2. **Step 4 (등급) 완료 후**
3. **Step 9 (평가-보상 연결) 완료 후**: 철학적 결정
4. **Step 12 (Rollout) 전**: 자원 확보 확인
5. **최종 산출물**: 전체 검토

## 관련 파일

- `knowledge/performance/review-cycles.md`
- `knowledge/performance/okr.md`
- `knowledge/performance/feedback-systems.md`
- `templates/review-cycle-template.md`
