# DESIGN.md — 골든타임 갭 브리핑

> google-labs-code/design.md 포맷을 따르는 비주얼 아이덴티티 명세.
> 이 저장소의 모든 페이지 수정 시 이 문서를 우선 적용한다.

## Identity

- **주제**: 소방 골든타임 vs 요양시설 대피 시간 — 생명 데이터를 다루는 진지한 브리핑
- **톤**: 신뢰·절제. 화려함보다 가독성. 위험은 단 하나의 색으로만 말한다
- **테마**: 라이트 단일 (dark 변형 없음 — 공유·인쇄·발표 환경 일관성을 위해 의도적 선택)

## Color Tokens

| 토큰 | 값 | 용도 |
|---|---|---|
| `--bg` | `#faf9f6` | 페이지 바탕 (따뜻한 오프화이트) |
| `--ink` | `#1c2430` | 본문 텍스트 (잉크 네이비) |
| `--sub` | `#5a6472` | 보조 텍스트·캡션 |
| `--line` | `#e3e0d8` | 경계선 |
| `--card` | `#ffffff` | 카드 표면 |
| `--accent` | `#e5484d` | **위험·미대피·갭 전용** — 다른 용도 금지 |
| `--steel` | `#3d6a8f` | 소방 축 (도착시간·안전센터·섹션 번호) |
| `--ok` | `#2f7d5a` | 개선·구조 가능 |
| `--chip` | `#eef1ee` | 배지·게이지 바탕 |

**규칙**: accent(빨강)는 "사람이 위험한 숫자"에만. 소방 관련은 steel, 개선은 ok. 장식 목적의 색 사용 금지.

## Typography

- 스택: `Pretendard, "Noto Sans KR", "Malgun Gothic", sans-serif` (웹폰트 미사용 — CSP·오프라인 안전)
- 본문 16px / 행간 1.65 / 본문 폭 max 760px
- 숫자는 `font-variant-numeric: tabular-nums` (카운터·표)
- 섹션 헤딩: `01`~`07` steel 색 번호 + 굵은 제목 — 번호는 실제 읽기 순서를 의미

## Layout (StyleGallery 패턴)

- **containment**: 모든 위젯(지도·표·통계)은 `--card` 배경 + `--line` 테두리 + radius 10~12px 카드로 감싼다
- **stacking**: 단일 컬럼, 섹션 간 여백은 h2 `margin-top: 52px`로만 제어 (개별 마진 금지)
- 표·코드 등 넓은 콘텐츠는 자체 `overflow-x: auto` 컨테이너

## Motion

- **절제 원칙**: 정보 변화를 따라가게 돕는 목적만. 과시성 애니메이션 금지
- 시나리오 전환: 점 크기 0.7초 ease-out, 카운터 1.2초, 델타 배지 0.35초 페이드업
- `prefers-reduced-motion` 항상 존중

## Map

- 타일: CARTO `light_all` (키 불필요, 항상 밝은 배경 — 어두운 타일 금지)
- 시설 점: accent 채움 55% 투명, 반지름 `max(3, √미대피 × 1.7)px`
- 미대피 0 시설: steel 윤곽선만 / 119안전센터: steel 소형 원
