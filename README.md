# 개인 프로젝트 | Relationship Economy

## 버튜버 팬덤의 지불은 ‘즉흥적 끌림’인가, ‘장기적으로 축적된 관계’인가?

버튜버(VTuber)의 실제 Live Chat 및 Super Chat 로그를 활용해, 팬과 특정 크리에이터 사이의 관계 형성 과정과 지불 행동을 분석하는 **개인 데이터 분석 프로젝트**입니다.

핵심 목표는 단순히 “활동량이 많은 팬이 더 많이 지불하는가?”를 확인하는 것이 아니라, **Relationship(관계의 깊이)** 을 행동 데이터로 정의하고, 단순 Engagement보다 미래의 지불과 반복 지불을 더 잘 설명하는지 검증하는 것입니다.

### 핵심 Research Questions
- 팬의 최초 지불은 **즉흥적 끌림(Impulse Attraction)** 과 **장기적으로 축적된 관계(Accumulated Relationship)** 중 어떤 경로에서 더 자주 발생하는가?
- 단순 Engagement Volume보다 **Relationship Depth** 가 향후 첫 Super Chat과 반복 지불을 더 잘 설명하는가?
- 첫 Super Chat은 관계 축적의 결과인가, 아니면 이후 관계를 강화하는 전환점과 함께 나타나는가?
- 빠르게 결제한 팬과 오래 관계를 쌓고 결제한 팬은 이후 Retention과 반복 지불에서 어떻게 다른가?

### 분석 설계
1. `user × VTuber × date` 단위 행동마트 생성
2. Duration / Frequency / Consistency / Recency / Concentration 기반 **Relationship Depth Score** 설계
3. **Survival Analysis** 로 첫 interaction 이후 첫 Super Chat까지의 time-to-event 분석
4. **Payment Event Study** 로 첫 결제 전후 행동 변화 비교
5. Impulse Payer / Gradual Payer / Loyal Non-payer / Casual Viewer / Loyal Paying Fan 세그먼트 비교
6. 시간 여유 시 Journey Clustering 확장

### 주요 지표
- Active Days
- Streams Joined
- Chat Count / Chat Days
- Relationship Duration
- Recency
- Interaction Consistency
- VTuber Concentration
- Days to First Super Chat
- Repeat Payment Rate
- Paying Active Days
- 30/60/90-day Retention
- Observed Revenue

### 데이터
- **VTuber 1B Dataset**
- 공개 저장소: https://github.com/sigvt/vtuber-livechat-dataset
- YouTube Live 기반 대규모 VTuber 채팅/후원 로그
- 전체 데이터 대신 특정 VTuber와 3~6개월 구간을 추출해 분석 예정

### 분석 스택
- SQL: CTE, Window Function, Cohort, user×creator mart, event alignment
- Python: EDA, Survival Analysis, statistical comparison, event-time analysis
- Tableau: Cohort / Relationship Journey / Segment / Payment Funnel 시각화

### 20일 Core Scope
- Day 1–3: 데이터 subset 선정 및 정제
- Day 4–7: SQL 행동마트와 relationship feature 생성
- Day 8–10: EDA + Relationship Depth Score 설계
- Day 11–13: Survival Analysis
- Day 14–15: First Payment Event Study
- Day 16: Fan Segmentation 및 robustness check
- Day 17: Tableau Dashboard
- Day 18: Product Hypothesis / Monetization Insight
- Day 19–20: 포트폴리오 문서화 및 QA

### 프로젝트 해석 원칙
- ‘신뢰’, ‘애착’을 로그로 직접 측정했다고 주장하지 않고 행동 기반 proxy로 해석합니다.
- 관찰 데이터이므로 correlation과 causality를 구분합니다.
- Super Chat은 전체 팬 수익화 중 일부이므로 VTuber 전체 LTV로 확대 해석하지 않습니다.

### 확장 방향
이 프로젝트는 버튜버 팬덤을 통해 **관계 기반 수익화(Relationship Economy)** 를 먼저 관찰하고, 이후 AI Character / AI Companion에서의 `대화 → 기억 → 개인화 → 관계 형성 → 구독` 구조로 확장하는 것을 목표로 합니다.

> **Relationship Economy — 인간은 디지털 존재와 어떤 관계를 맺고, 관계의 무엇에 돈을 지불하는가?**
