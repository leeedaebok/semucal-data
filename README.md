# semucal-data

**사장님 세무캘린더** 앱이 소비하는 원격 세무 일정 데이터.

## 구조
- `data/tax_calendar.json` — 국세·지방세 신고/납부 일정(연도 비종속 rule + 연도별 공휴일)

## 갱신 워크플로
1. 로컬에서 `data/tax_calendar.json` 수정 (국세청 세무일정·위택스 1차 대조, 모델 지식 금지)
2. 커밋 후 `master`에 push
3. 앱이 다음 실행 시 아래 raw URL로 받아 캐시 → 무심사 반영

```
https://raw.githubusercontent.com/leeedaebok/semucal-data/master/data/tax_calendar.json
```

## 스키마 메모
- 일정은 `rule`(`fixed` = month/day 고정, `monthly` = 매월 day)만 가지며 연도를 담지 않는다. 앱이 오늘 기준 다음 도래일로 해석한다.
- 순연은 `holidays`(연도별 공휴일 맵)로 앱이 자동 계산(토·일·공휴일 → 다음 영업일).
- 제도 개정(시행시기 등)은 매년 12월 정기 갱신, 임시공휴일·직권연장은 수시 핫픽스.
