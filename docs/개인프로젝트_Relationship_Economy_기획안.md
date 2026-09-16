# 개인 프로젝트 | Relationship Economy 분석 기획안

## 프로젝트 제목
**첫눈에 반한 팬 vs 오래 함께한 팬**  
버튜버 팬덤의 지불을 만드는 것은 즉흥적 끌림인가, 장기적으로 축적된 관계인가?

## 1. 프로젝트 목적
버튜버(VTuber)의 실제 Live Chat 및 Super Chat 로그를 활용해 팬과 특정 크리에이터 사이의 관계 형성 과정과 지불 행동을 분석한다.

핵심 목적은 단순히 “활동량이 많은 팬이 더 많이 지불하는가?”를 확인하는 것이 아니라, **Relationship(관계의 깊이)** 을 행동 데이터로 정의하고 단순 Engagement보다 미래의 지불 및 반복 지불을 더 잘 설명하는지 검증하는 것이다.

## 2. 핵심 Research Questions
1. 팬의 최초 지불은 **즉흥적 끌림(Impulse Attraction)** 과 **장기적으로 축적된 관계(Accumulated Relationship)** 중 어떤 경로에서 발생하는가?
2. 단순 Engagement Volume보다 **Relationship Depth** 가 향후 첫 Super Chat과 반복 지불을 더 잘 설명하는가?
3. 첫 Super Chat은 관계 축적의 결과인가, 혹은 이후 관계를 강화하는 전환점과 함께 나타나는가?
4. 빠르게 결제한 팬과 오래 관계를 쌓고 결제한 팬은 이후 Retention, 반복 지불, 장기 Revenue에서 어떻게 다른가?

## 3. 분석 난이도 설계
### Relationship Depth Score
관계의 깊이를 다음 행동 기반 proxy로 정의한다.
- Duration: 최초 interaction 이후 관계 지속기간
- Frequency: 활동일수 및 참여 방송 수
- Consistency: 방문 주기와 활동의 규칙성
- Recency: 최근 상호작용 시점
- Concentration: 특정 VTuber에 대한 상호작용 집중도

단순 활동량 기반 모델과 관계 깊이 기반 모델을 비교한다.

- **Model A — Engagement Volume**: Chat Count, Stream Count, Total Events
- **Model B — Relationship Depth**: Duration, Frequency, Consistency, Recency, Concentration

## 4. Survival Analysis
첫 interaction을 Day 0으로 두고 첫 Super Chat까지 걸리는 시간을 `time-to-event`로 정의한다.

- Kaplan–Meier curve로 팬 유형별 최초 지불 시점 비교
- 결제하지 않은 유저도 censored observation으로 포함
- Relationship Depth와 최초 지불 hazard의 연관성 분석

핵심 질문은 **“누가 결제했는가?”가 아니라 “관계가 형성된 뒤 언제 결제하는가?”** 이다.

## 5. Payment Event Study
첫 Super Chat 시점을 `t=0`으로 정렬해 결제 전후 행동 변화를 분석한다.

`D-30 → D-7 → First Super Chat → D+7 → D+30 → D+90`

확인할 항목:
- 결제 직전 특정 VTuber 집중도 상승 여부
- 방문 빈도 및 활동 지속성 변화
- 결제 이후 상호작용 강화/약화 여부

관찰 데이터이므로 인과관계가 아니라 **결제 전후에 동반되는 행동 패턴**으로 해석한다.

## 6. Fan Journey Segmentation
- **Impulse Payer**: 짧은 관계기간 + 빠른 첫 결제
- **Gradual Payer**: 긴 관계 축적 후 첫 결제
- **Loyal Non-payer**: 높은 지속성·집중도 + 결제 없음
- **Casual Viewer**: 낮은 지속성·낮은 집중도
- **Loyal Paying Fan**: 지속 관계 + 반복 결제

특히 Loyal Non-payer를 통해 **관계 깊이와 지불 의향이 반드시 동일한가**를 검증한다.

## 7. 데이터 마트
### user_creator_daily
`fan_id, vtuber_id, date, chat_count, stream_count, superchat_count, superchat_amount`

### user_creator_relationship
`first_seen, last_seen, duration, active_days, frequency, consistency, concentration`

### first_payment_event
`first_superchat_at, days_to_first_payment, pre/post behavior metrics`

### fan_outcome
`repeat_payment, paying_active_days, 30/60/90-day activity, observed revenue`

## 8. 데이터
- **VTuber 1B Dataset**
- Source: https://github.com/sigvt/vtuber-livechat-dataset
- YouTube Live 기반 대규모 VTuber 채팅 및 Super Chat 로그
- 전체 데이터 대신 특정 VTuber 및 3~6개월 구간을 subset으로 추출해 분석

## 9. 분석 스택
- **SQL**: CTE, Window Function, Cohort, user×creator mart, event alignment
- **Python**: EDA, Survival Analysis, statistical comparison, event-time analysis
- **Tableau**: Relationship Journey, Cohort, Segment, Payment Funnel 시각화

## 10. 20일 실행 계획
- Day 1–3: 데이터 subset 선정·정제·분석 단위 확정
- Day 4–7: SQL user×creator mart 및 relationship feature 생성
- Day 8–10: EDA + Relationship Depth Score 설계
- Day 11–13: Survival Analysis
- Day 14–15: First Payment Event Study
- Day 16: Fan Segmentation 및 robustness check
- Day 17: Tableau Dashboard
- Day 18: Product Hypothesis / Monetization Insight
- Day 19–20: 포트폴리오 문서화 및 QA

## 11. 프로젝트 해석 원칙
- ‘신뢰’, ‘애착’을 로그로 직접 측정했다고 주장하지 않는다.
- Relationship Depth는 행동 기반 proxy로 해석한다.
- 관찰 데이터이므로 correlation과 causality를 구분한다.
- Super Chat은 전체 팬 수익화 중 일부이므로 VTuber 전체 LTV로 확대 해석하지 않는다.

## 12. 확장 방향
버튜버 팬덤에서 관찰되는 `콘텐츠 → 반복 상호작용 → 관계 형성 → 지불` 구조를 기반으로 향후 AI Character / AI Companion의 `대화 → 기억 → 개인화 → 관계 형성 → 구독` 구조로 연구를 확장한다.

> **Relationship Economy — 인간은 디지털 존재와 어떤 관계를 맺고, 관계의 무엇에 돈을 지불하는가?**

## 13. 데이터 선택 고민 및 의사결정 기준

현재 프로젝트에서 가장 큰 고민은 **분석 자유도가 높은 오래된 user-level 로그를 사용할 것인지, 최신성이 높은 대신 개인 행동 분석이 어려운 데이터를 사용할 것인지**이다.

### 13-1. VTuber 1B를 그대로 사용할 경우
**장점**
- 익명화된 user ID, VTuber channel ID, video ID, timestamp, Super Chat 이벤트 등 user-level 행동 분석에 필요한 구조가 비교적 잘 갖춰져 있다.
- `user × creator × time` 단위로 행동마트를 직접 만들 수 있어 Relationship Depth, Survival Analysis, First Payment Event Study를 자유롭게 설계할 수 있다.
- 공개 데이터이므로 실제 분석 재현성이 높다.

**한계**
- 원천 데이터가 주로 2021~2022 시점에 집중되어 있어 현재 시장의 최신 행동을 직접 대표한다고 보기 어렵다.
- 따라서 결과를 “2026년 버튜버 팬 행동”으로 일반화하지 않고, **historical behavioral dataset을 활용한 관계·지불 구조 분석**으로 명확히 한정해야 한다.

### 13-2. CHI 2025 연구 공개 데이터를 사용할 경우
해당 연구는 더 최근 시점까지의 대규모 VTuber 데이터를 다루지만, 공개 GitHub에는 전체 user-level raw log가 아니라 일부 집계·전처리 데이터만 공개되어 있다.

확인 결과:
- `payment_timestamps_of_sampled_vtubers.jsonl`: 방송 단위 `session_name`, `vtuber`, `payment_timestamps[]` 구조로 결제 시점은 확인 가능하지만 개별 user journey를 재구성하기 어렵다.
- `grouped_membership_status_stats_v5.jsonl`: `<1개월`, `1-2개월`, `2-6개월`, `1-2년` 등 membership tenure별 집계값만 존재한다.
- `num_of_vtubers_subscribed_to.jsonl`: 사용자가 몇 명의 VTuber를 구독했는지에 대한 분포는 있으나 user-level 식별자와 개별 행동 연결은 없다.
- `loyal_users_per_vtuber.jsonl`: 현재 공개 파일은 비어 있다.

따라서 이 데이터만으로는 `첫 노출 → 관계 축적 → 최초 지불 → 반복 지불`의 개인 단위 journey를 직접 분석하기 어렵다.

### 13-3. 2024~2026 최신 데이터 후보
2026년까지 업데이트되는 VTuber tracking archive 등 최신 자료도 존재하지만, 대부분 채널·방송·시장 추적용 메타데이터에 가깝고 다음 구조를 동시에 만족하지 못하는 경우가 많다.

`user_id + creator_id/IP + timestamp + 반복 interaction + payment/monetization`

최신성은 높지만 Relationship Economy를 user-level Product Analytics 관점에서 분석하기에는 제한적일 수 있다.

### 13-4. 현재 의사결정 기준
데이터 선택 시 다음 우선순위를 적용한다.

1. **User-level linkage** — 동일 사용자의 행동을 시간축으로 연결할 수 있는가?
2. **Creator/IP linkage** — 특정 VTuber/creator와의 관계를 구분할 수 있는가?
3. **Timestamp** — 관계 형성 과정을 순서와 기간으로 재구성할 수 있는가?
4. **Monetization** — 실제 결제 또는 지불 이벤트가 존재하는가?
5. **Recency** — 위 조건을 만족하면서 가능한 한 최신 데이터인가?
6. **20일 실행 가능성** — 접근·정제·가공 비용이 프로젝트 기간 내 감당 가능한가?

### 13-5. 잠정 방향
현재까지 확인한 범위에서는 **VTuber 1B가 최신성은 약하지만 분석 목적과 가장 잘 맞는 공개 user-level 데이터**다.

따라서 바로 확정하지 않고 다음 순서로 결정한다.

- **1순위:** 2024~2026 구간의 creator/fandom 데이터 중 user-level interaction + payment 구조를 갖춘 공개 데이터가 있는지 추가 탐색
- **2순위:** 적합한 최신 데이터가 없으면 VTuber 1B를 메인 데이터로 사용
- **보조 자료:** CHI 2025 및 최신 시장 자료는 membership, fandom structure, 최근 시장 맥락을 보완하는 secondary evidence로 활용

이 경우 프로젝트의 주장은 다음처럼 제한한다.

> **“최신 시장의 규모와 트렌드는 최근 자료로 설명하되, 팬의 관계 형성과 지불 메커니즘은 재현 가능한 historical user-level behavioral data로 검증한다.”**

즉, **최신성만을 위해 분석 가능성을 희생하지 않고, 분석 가능한 데이터와 최신 시장 맥락을 분리해서 사용한다.**
