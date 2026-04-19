# Playbook: Design Pay Bands

페이밴드를 설계하는 절차.

## 실행 조건

- **필수**: `context/roles-and-levels.md` 가 정의되어 있어야 함 (없으면 `design-leveling.md` 먼저)
- **권장**: `context/compensation-data.md` 의 현 급여 분포
- **권장**: 보상 철학 관련 경영진 합의

## 산출물

- **Pay Band Table** (`templates/pay-band-template.md` 형식)
- 현직자 매핑 결과
- 이탈자 조정 계획
- 연간 갱신 프로세스

## 단계

### Step 1: 지식 / 컨텍스트 로드

1. `knowledge/compensation/pay-bands.md` — 이론
2. `knowledge/compensation/market-benchmark.md` — 벤치마크 방법
3. `knowledge/compensation/pay-philosophy.md` — 철학
4. `context/roles-and-levels.md` — 레벨 구조
5. `context/compensation-data.md` — 현 데이터
6. `context/constraints.md` — 예산 제약

### Step 2: 철학 확정

설계 전에 다음 항목에 대한 **명시적 합의** 확보:

- **시장 포지셔닝**: 어떤 percentile? (직군별 차등 가능)
- **Spread**: 레벨별 밴드 폭
- **Overlap**: 인접 레벨 간 중첩 비율
- **Location Factor**: 적용 여부 및 단계
- **Compa Group**: 밴드 내 위치 구분 체계

합의되지 않은 항목이 있으면 **사용자에게 결정 요청**. 에이전트가 임의 결정 금지.

#### 2-보강 (Scope 판정)

본 플레이북 진입 전 `.claude/rules/scope-discipline.md`의 §0 Scope 판정 5단계를 수행하라. Total Comp 층과 Cash 층 분리는 **축소/이관** 판정의 대표 예시다.

### Step 3: 시장 벤치마크 수집

`market-benchmark.md` 절차 따라:

#### 3-1: 데이터 소스 선정
- 국내 IT: 원티드 인사이트, Levels.fyi, 경쟁사 공개 자료
- 직군별로 소스 다를 수 있음

#### 3-2: 데이터 정규화
- Base vs TC 구분
- 지역 구분
- 레벨 매핑

#### 3-3: 직군 x 레벨 매트릭스 작성

| 직군 | 레벨 | 소스 | p50 | p75 | p90 | 표본 | 비고 |
|------|------|------|-----|-----|-----|------|------|

**표본 수 검증 규약** (필수):

- **n < 50 소스는 단독 사용 금지** — 반드시 2개 이상 소스 가중 평균 또는 **보수 퍼센타일**(예: 목표 p60 → 실제 p55 적용) 선택
- **표본 수 미확인 소스**는 산출물 §7.1 데이터 소스 표에 **"표본 미확인" 라벨 필수**
- **n이 작을수록 가중치 축소**: 예) 가중 평균 시 원티드 n=300, 교육 피어 n=40이면 원티드 0.7 / 교육 피어 0.3 수준으로 조정 근거 명시
- 이 규약은 **PB-2 rubric "벤치마크 근거 명시"의 숨은 취약점**(출처만 있고 n이 부재하거나 n<50) 차단 목적 (s1·s3·s5 교차 관찰 근거)

### Step 4: Midpoint 산정

Step 2에서 정한 포지셔닝에 따라 midpoint 결정.

**예시**: 포지셔닝 p65, p50=7,500 / p75=9,000
```
p65 = 7,500 + (9,000 - 7,500) × 0.6 = 8,400
Midpoint = 8,400
```

### Step 5: Min / Max 산출

Spread에 따라:
```
Min = Midpoint × (1 - spread/2)
Max = Midpoint × (1 + spread/2)
```

**레벨별 spread 적용**:
- IC1~IC2: 25~30%
- IC3~IC4: 30~40%
- IC5+: 40~50%
- Manager: 40~60%

### Step 6: Overlap 검증

인접 레벨 간 overlap 비율 계산:
```
Overlap % = (Lower Max - Upper Min) / Lower Max
```

목표: **20~30% overlap**.

너무 크거나 작으면 midpoint 간격 조정.

### Step 7: Location Factor 적용 (선택)

기본 지역(예: 서울) 1.0 기준으로 타 지역 계수 적용.

```
예:
- 서울 / 수도권: 1.0
- 비수도권: 0.93
- 해외 원격: 개별 협의
```

**주의**: 2~3단계 권장. 과도한 세분화는 운영 부담.

### Step 8: Compa Group 정의

밴드 내 위치 구분 (GitLab 방식):
- **Learning** (Min ~ Mid-5%): 레벨 역량 학습 중
- **Performing** (Mid-5% ~ Mid+5%): 레벨 역량 충족
- **Exceeding** (Mid+5% ~ Max): 레벨 역량 초과

또는 단순히 4분위로 구분도 가능.

### Step 9: 현직자 매핑

각 구성원의 현 급여를 밴드에 매핑.

**발생 가능한 케이스**:

1. **밴드 내 적정 위치**: 문제 없음
2. **밴드 하한 미달**: 인상 계획 수립
3. **밴드 상한 초과**: 동결 또는 특별 관리
4. **Compa Group 불일치**: 성과와 보상 연계 점검

### Step 10: 이탈자 조정 계획

밴드 이탈자를 어떻게 처리할지.

**하한 미달**:
- 즉시 인상 (예산 충분 시)
- 단계적 인상 (2~3 사이클에 걸쳐)

**상한 초과**:
- 동결 (밴드 갱신까지)
- Red Circle (레벨만 조정, 급여는 유지)
- 밴드 재검토 (밴드 자체가 낮게 설계됐을 수 있음)

### Step 11: 예산 검증

`constraints.md` 의 예산 제약과 대조:
- 전체 인건비 증가율
- 개인별 최대 인상률
- Special grant 가능 여부

제약 초과 시 **사용자에게 재조정 요청**.

### Step 12: 갱신 프로세스 설계

연간 갱신 방식:

- **시점**: (예: 매년 Q3에 갱신, Q4에 적용)
- **주체**: HR / People Team
- **프로세스**:
  1. 시장 데이터 재수집
  2. 밴드 수치 조정 제안
  3. 경영진 승인
  4. 전사 공유
  5. 개인별 적용

### Step 13: 투명성 수준 결정

밴드 공개 범위:
- 본인 밴드만 공개
- 본인 + 인접 레벨 공개
- 전사 공개

`pay-philosophy.md` 의 투명성 수준과 일치시킬 것.

### Step 14: 산출물 작성

`templates/pay-band-template.md` 형식.

**필수 노출 항목**:

- Step 2-보강의 **Total Comp 층 vs Cash 층 scope 판정 결과**를 §1.1 또는 서문 "설계 scope" 블록에 명시
- Step 3-3의 **벤치마크 표본 수 검증 결과**(n<50 소스 처리, 표본 미확인 라벨)를 §7.1 데이터 소스 표에 반영

## 체크포인트

- [ ] 철학이 먼저 합의되었는가?
- [ ] **Total Comp vs Cash 층 scope 판정이 산출물에 명시되었는가?** (Step 2-보강)
- [ ] 벤치마크 데이터가 **최근 6개월 이내**인가?
- [ ] **벤치마크 소스별 표본 수(n)가 명시되고 n<50 소스는 단독 사용하지 않았는가?** (Step 3-3)
- [ ] 모든 직군 x 레벨 조합이 커버되는가?
- [ ] Overlap이 설계 의도 범위 내인가?
- [ ] 현직자 매핑에 **이탈자 조정 계획**이 있는가?
- [ ] 예산 제약을 준수하는가?
- [ ] 성별/연령 페이 갭이 **악화되지 않는가**?
- [ ] 갱신 주기가 정의되었는가?

## 사용자 확인 지점

1. **Step 2 (철학) 완료 후**
2. **Step 3 (벤치마크) 완료 후**: 데이터 소스 승인
3. **Step 9 (매핑) 완료 후**: 매핑 결과 검토
4. **Step 10~11 (조정/예산)**: 예산 영향 확인
5. **최종 산출물**: 전체 검토

## 관련 파일

- `knowledge/compensation/pay-bands.md`
- `knowledge/compensation/market-benchmark.md`
- `knowledge/compensation/pay-philosophy.md`
- `templates/pay-band-template.md`
