# Expected Issues — s3

## 반드시 다뤄져야 할 이슈 (P1)

1. **Geographic Pay Policy 문서화 부재 + "Location-agnostic" 원칙과 실 운영 괴리**
   - 근거: `current-system.md`, `compensation-data.md` 2.3x 격차
   - 기대 권고: 명시적 정책 3가지 중 선택 — (a) 완전 균일 (b) 티어별(Tier A/B/C) (c) 순수 로컬 마켓. 각 트레이드오프 분석

2. **Market Benchmark 국가별 소스 관리 부재**
   - 근거: `current-system.md` "어떤 소스 쓰는지 비공개"
   - 기대 권고: 국가별 벤치마크 소스 등록·분기 업데이트 절차

3. **Equity 국가별 세금 형평성 (실수령 2배+ 차)**
   - 근거: `constraints.md`, `compensation-data.md`
   - 기대 권고: Tax-equalization 접근 검토 또는 세후 형평성을 고려한 grant 조정

4. **평가·승진 결정에서 서구권 집중 (제도적 불이익)**
   - 근거: `roles-and-levels.md` 시차/언어 장벽 내부 설문
   - 기대 권고: 비동기 Calibration 설계, 각 지역 대표자 포함

5. **환율 변동 리스크 대응 부재**
   - 근거: `current-system.md`, `compensation-data.md`
   - 기대 권고: FX buffer 또는 정기 재조정 메커니즘

## 놓치지 말아야 할 이슈 (P2)

6. **EOR 비용이 지역 조정 계산에 반영되어 있나**
7. **법규 업데이트 프로세스 부재** (지역별 HRBP 없음)
8. **Exit survey에서 "지역 간 형평성 불만" 1위 → 긴급도 표시**
9. **신입 입사자 vs 기존 입사자 정책 차등 — 향후 정합 로드맵**

## 다뤄질 필요 없는 사항

- 단일 로케이션 가정 권고
- 대규모 레벨 매트릭스 재설계 (레벨 자체는 Global 단일, 이 부분은 유지)

## 난이도 태그

**Hard** — 지역성·환율·세법·문화 다변수. 이 시나리오는 "한 쪽 답을 고르기"보다 **트레이드오프를 솔직히 드러내고 옵션 제시**하는 것이 유능함의 표지. 플레이북이 단일 해답을 밀어붙이지 않는지가 평가 포인트.
