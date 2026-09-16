# Data

개인 프로젝트 **Relationship Economy**의 데이터 관리 규칙을 기록합니다.

## 데이터 소스
- VTuber 1B Dataset
- 원본 저장소: https://github.com/sigvt/vtuber-livechat-dataset

## 운영 원칙
- 대용량 원본 데이터는 GitHub에 커밋하지 않습니다.
- 로컬에서는 `data/raw/`, `data/interim/`, `data/processed/` 구조 사용을 권장합니다.
- GitHub에는 스키마, 샘플 컬럼 설명, 추출 조건, 데이터 딕셔너리만 저장합니다.
- 분석 재현을 위해 사용한 VTuber, 기간, 필터 조건을 명시합니다.

## 예정 문서
- `data_dictionary.md`
- `subset_definition.md`
- `quality_checks.md`
