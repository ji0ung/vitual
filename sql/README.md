# SQL

개인 프로젝트 **Relationship Economy**의 데이터 마트 및 분석 쿼리를 관리합니다.

## 예정 파일
- `01_user_creator_daily.sql` — user × VTuber × date 행동마트
- `02_relationship_features.sql` — Duration / Frequency / Consistency / Recency / Concentration
- `03_first_payment_event.sql` — 최초 Super Chat 및 결제 전후 이벤트 정렬
- `04_retention_cohort.sql` — 30/60/90-day Retention 및 cohort

## 원칙
- 원본 데이터는 저장소에 직접 업로드하지 않습니다.
- 재현 가능한 변환 로직을 SQL로 남깁니다.
- 파생 지표 정의는 기획 문서와 일치시키고 변경 시 함께 업데이트합니다.
