# Website A — 도담도담 (Dodam)

> 작성일: 2026-05-20 KST (v2 — 레퍼런스 정밀 재추출)
> 디자인 레퍼런스: Aboard (https://www.aboard.com) — 첨부 캡처 기준
> 서비스: 아이를 위한 동네 병원 추천·리뷰·프로모션 공유 앱
> 폰트: **타이틀 = ELandNice** (jsdelivr CDN) / **본문 = Pretendard**

---

## 1. 톤 키워드

**캠페인 SaaS · 노란빛이 주인공 · 둥글둥글 마스코트 · 비대칭 카드 그리드 · 손글씨 헤딩**

레퍼런스의 핵심은 **(1) 옐로우가 메인 컬러 — 다른 컬러는 옐로우를 받쳐주는 보조 / (2) 한 컬러 안에서도 라이트/메인 두 단계가 같이 사용됨 / (3) 마스코트는 단순 도형이 아니라 "표정과 볼터치까지 있는 캐릭터" / (4) 종이 메모 3장 묶음과 해바라기는 시그니처 일러스트**.

---

## 2. 컬러 팔레트 (재정의)

### 2.1 베이스

| 토큰 | hex | 비고 |
|---|---|---|
| `--wa-bg`      | `#FFFFFF` | 메인 흰 배경 |
| `--wa-text`    | `#1A1A1A` | 본문/헤딩 (거의 검정) |
| `--wa-text-mut`| `#6B6B6B` | 보조 |
| `--wa-text-sub`| `#9B9B9B` | 더 보조 |
| `--wa-border`  | `#E8E5DE` | 카드/UI 보더 (일러스트엔 사용 X) |

**일러스트 — 완전 플랫 + 볼드.** 레퍼런스 (Aboard 마스코트 시트) 의 진짜 핵심:

1. **그라데이션 0** — fill 은 한 단색
2. **drop-shadow 0** — 그림자 일체 없음
3. **opacity 0** — 표정도 풀 검정
4. **외곽선 0** — 마스코트 보더 안 씀
5. **표정 stroke = 순수 검정 `#000` 3~4px**, `stroke-linecap: round`
6. **눈 두 가지 변형**:
   - **닫힌 호** `^^` (살짝 위로 휘는 작은 두 호) — 기본
   - **googly** (흰 동그라미 + 검정 동공 4-6px) — 변화감
7. **윙크** — 한쪽은 동그라미, 다른 쪽은 닫힌 호
8. **볼터치 X** — 레퍼런스에 없음
9. **크기 1.3~1.5×** 키움 — 통통하고 존재감 있게
10. **흰 sparkle ✦ (4-point star)** — 큰 마스코트 옆 코너 데코로 시그니처

### 2.1.5 vivid 시그니처 4종 (배경 카드용)

레퍼런스 image 1·2·3 의 박스 배경 톤. **파스텔이 아닌 진한 단색**.

| 토큰 | hex | 매칭 |
|---|---|---|
| `--wa-blue-vivid`  | `#1E4DEB` | image 1 royal blue 배경 — 흰 텍스트 |
| `--wa-yellow`      | `#FFC83D` | image 2 sunshine 배경 — 검정 텍스트 |
| `--wa-green`       | `#2F9C56` | image 3 vivid green 배경 — 흰 텍스트 |
| `--wa-orange`      | `#FF5C2E` | image 1·2 의 큰 원 마스코트 / 강한 배경 |

### 2.2 카드 컬러 (옐로우 중심 9종)

레퍼런스의 색을 6종에서 **9종으로 확장** + **light / main 두 단계** 명확히 분리.

| 토큰 | hex | 매칭 |
|---|---|---|
| **YELLOW (메인)** | | |
| `--wa-yellow`        | `#FFD66E` | Aboard 의 "Profiles / Events / Photos / 1-2-1" 카드 (메인 옐로우, 가장 많이 등장) |
| `--wa-yellow-soft`   | `#FFEAA8` | Yellow light (캘린더 mockup 안 배경 등) |
| `--wa-yellow-deep`   | `#F2B826` | Yellow deep (액센트, 호버) |
| **ORANGE (시그니처)** | | |
| `--wa-orange`        | `#FF8E47` | **"Holiday planning" 의 큰 오렌지 구름 마스코트 컬러 — 시그니처** |
| `--wa-orange-deep`   | `#E66A1F` | 외곽선 강조 또는 보더 |
| **PINK** | | |
| `--wa-pink`          | `#F8C6D7` | "Pre-boarding" 카드 (꽃 마스코트 배경) — 차분한 코랄핑크 |
| `--wa-pink-deep`     | `#F4A8C7` | 볼터치, 액센트 |
| **GREEN (라임)** | | |
| `--wa-green`         | `#DBE57F` | "People data" 카드 — 라임 그린 |
| `--wa-green-deep`    | `#B6C246` | "Bulk action" 다크그린 카드 |
| `--wa-green-soft`    | `#E7EE9D` | "Analytics" 옅은 라이트그린 |
| **LAVENDER** | | |
| `--wa-lavender`      | `#DDD4F2` | "Whistleblowing / Templates" 카드 |
| `--wa-lavender-deep` | `#B6A4E0` | 액센트 |
| **CREAM / NEUTRAL** | | |
| `--wa-cream`         | `#F4EFE2` | "Anna Mooney / Collaborate together / Everything sorted" 카드 — 회색빛 베이지 |
| **BLUE** | | |
| `--wa-blue`          | `#C7E2F5` | "Your documents in one secure place" 큰 카드 (자물쇠 일러스트 배경) |
| **MINT** (옵션) | | |
| `--wa-mint`          | `#C9EBD9` | 추가 보조 |

### 2.3 무지개 그라데이션 (Hero 백드롭)

레퍼런스의 헤더 무지개는 **5색 → 흰 배경으로 자연스럽게 페이드 아웃**.

```css
background:
  radial-gradient(70% 90% at 50% 0%,
    rgba(248, 198, 215, 0.92) 0%,    /* 핑크 */
    rgba(255, 214, 110, 0.88) 22%,   /* 옐로우 */
    rgba(255, 142, 71, 0.65) 38%,    /* 오렌지 (약간) */
    rgba(219, 229, 127, 0.65) 55%,   /* 라임 */
    rgba(221, 212, 242, 0.55) 75%,   /* 라벤더 */
    rgba(255, 255, 255, 0)  100%);
filter: blur(8px);
```

오렌지를 추가 stop 으로 넣은 게 핵심 — 레퍼런스에서 핑크와 옐로우 사이가 따뜻한 색감으로 채워짐.

---

## 3. 타이포

### 3.1 폰트 패밀리

```css
@font-face {
  font-family: 'ELandNice';
  src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts-20-12@1.0/ELAND_Nice_M.woff') format('woff');
  font-weight: normal;
  font-display: swap;
}
:root {
  --wa-font:       "Pretendard", -apple-system, sans-serif;
  --wa-font-title: 'ELandNice', "Pretendard", sans-serif;
}
```

### 3.2 스케일

| 토큰 | 폰트 | size | weight | letter-spacing | 용도 |
|---|---|---|---|---|---|
| `.wa-hero-display` | ELandNice | clamp(48px, 7vw, 96px) | 400 | -.005em | Hero 헤드라인 |
| `.wa-display`      | ELandNice | clamp(44px, 6.4vw, 86px) | 400 | -.01em | placeholder 큰 |
| `.wa-h1`           | ELandNice | clamp(34px, 3.8vw, 52px) | 400 | -.005em | 섹션 헤드 |
| `.wa-h2`           | ELandNice | clamp(24px, 2.4vw, 32px) | 400 | 0 | 카드 헤드 |
| `.wa-brand`        | ELandNice | 22px | 400 | 0 | 도담도담 로고 |
| `.wa-body`         | Pretendard| 16px | 400 | -.015em | 본문 |
| `.wa-body-mut`     | Pretendard| 15px | 400 | -.01em | 본문 보조 |
| `.wa-tag`          | Pretendard| 11px | 600 (upper, .1em) | — | 카드 상단 라벨 |

**규칙**: ELandNice 는 무게가 이미 충분히 두꺼움 → weight 400 으로 그대로 사용. Pretendard 본문은 -.015em 정도 살짝 좁히기 (한글 시각 보정).

---

## 3.9 카드 ↔ 마스코트 크롭 시스템 (v3)

레퍼런스의 결정적 감성: **마스코트가 박스 면적의 50%+ 차지하고 모서리에서 잘림**. 박스 가운데 작게 들어가는 게 아님.

- `.wa-card { overflow: hidden; position: relative; }` 유지
- `.wa-card-crop` — 마스코트 wrapper. `position: absolute` + 음수 offset
- variant: `is-tl-lg / is-br / is-br-lg / is-tr / is-c` — 어디로 잘릴지
- 마스코트 SVG width 도 함께 1.5~2× 키움 (현 카드 안에서 작게 들어가던 사이즈에서 280-320px 까지)
- 한 카드 안에 마스코트 2-3개 — `is-tl-lg` + `is-br` 조합 (image 3 의 큰 노란 원 + 작은 클로버 톤)

## 4. 일러스트레이션 라이브러리 (재정의)

레퍼런스의 모든 마스코트·아이콘은 **outline 없는 평면 컬러 + 부드러운 표정 stroke + soft drop-shadow** 패턴을 공유합니다. 모두 인라인 SVG.

### 4.1 구름 마스코트 (Cloud)

**5봉우리 구름** (지금 4봉우리에서 한 단계 더 정밀화):

- 전체 폭 120 × 높이 90
- 윗선이 5개 봉우리로 구성 (작은-큰-작은-큰-작은)
- 외곽선: `--wa-stroke` 2px (없으면 단순해 보임 — 반드시 있어야 함)
- 채우기: **그라데이션** (라이트 → 메인) — 입체감 살짝
- **얼굴 요소**:
  - 두 눈 — 호 모양 닫힌 눈 (`Q` 곡선, 검정 2.5px stroke) — 살짝 미소 짓는 느낌
  - 핑크 볼터치 2개 — 옆구리에 작은 분홍 타원 (opacity .7)
  - 입 — 작은 호 (`M..Q..` 검정 2.5px)
- 컬러 variant 4종:
  - **노란 구름** (`--wa-yellow`) — 가장 많이 사용, Hero 마스코트 중 하나
  - **핑크 구름** (`--wa-pink-deep`) — Hero 옆 마스코트
  - **오렌지 구름** (`--wa-orange`) — **"Holiday planning" 의 시그니처 큰 마스코트, 크기 1.5×**
  - **흰 구름** (`#FFFFFF` 보더만) — 옵션

### 4.2 해바라기 마스코트 (Flower)

**"Pre-boarding" 카드의 핑크 배경 위 시그니처 일러스트**:

- 폭 140 × 높이 170 (큼)
- **꽃잎 8장** — 모두 둥근 타원 (`rx 14 ry 22`), 45도씩 회전 배치
- 꽃잎 색: `--wa-yellow-deep` (강한 노랑)
- 꽃잎 외곽선: **`--wa-stroke` 2px** (꼭 검정 보더)
- 꽃잎 끝이 살짝 둥글게 → `ellipse` 가 자연스러움
- **가운데 얼굴** — 큰 동그라미 (r 24), `--wa-yellow-soft` 채움 + 검정 보더
  - 두 눈 — 닫힌 호 (살짝 위쪽 휘어짐, 즐거운 표정)
  - 입 — 큰 호 (V 자 미소 X, 둥근 U 자 O — 부드러움)
  - 볼 — 핑크 작은 타원 양옆
- **줄기** — 한쪽으로 짧게 (옆구리에 한 잎 추가) — 옵션
- 자세는 **약간 기울어짐** (3° ~ 5°) — 너무 정직하지 않게

### 4.3 종이 메모 3장 묶음 (Memo Stack)

**"Photos" / "Gather work-related photos" 시그니처**:

- 3장 겹쳐 배치, 각각 다른 각도와 컬러
- 사이즈: 각 100 × 120 정도, 살짝 겹쳐서 전체 230 × 160
- 각도:
  - **장 1 (뒤)** — 옐로우 (`--wa-yellow`), 회전 -8°
  - **장 2 (가운데)** — 핑크 (`--wa-pink`), 회전 4°
  - **장 3 (앞, 작음)** — 그린 (`--wa-green`), 회전 -2°, 60 × 80
- 각 종이:
  - 둥근 모서리 8px
  - 외곽선 `--wa-stroke` 2px
  - 가운데 작은 동그라미 (r 14) — 각자 약간 다른 채움색 (deep 톤) + 그 안에 작은 face (눈 2개 + 미소)
- **시각 효과**: 폴라로이드 사진처럼 보이게. 메모/사진 두 가지 의미 동시 표현.

### 4.4 별 마스코트 (Star)

- 5각 별 (각 30°씩 회전, 둥글지 않은 표준 star path)
- 채움: `--wa-yellow-deep`
- 외곽선: `--wa-stroke` 2.5px
- 가운데 작은 얼굴 (face — 점 두 개 눈 + 미소 호)

### 4.5 위치 핀 (Pin)

- 폭 60 × 높이 76
- 핑크 핀 (`--wa-pink-deep`) + 둥근 위쪽 + 뾰족한 아래쪽
- 외곽선 `--wa-stroke` 2.5px
- 가운데 흰 동그라미 (r 10) + 검정 보더

### 4.6 아이콘 (작은 SVG, 외곽선 only)

레퍼런스 카드 모서리에 작게 들어가는 단순 아이콘들. **stroke only, 채움 없음, 1.8px stroke, 둥근 끝**.

- 종 (bell) — "알림" 카드
- 방패 (shield + 체크) — "안전" 카드
- 화살표 우측 (arrow-right) — "더보기"
- 캘린더 (calendar grid)
- 카메라 (camera body + 렌즈)
- 청진기 (stethoscope) — 의료
- 별 외곽선 (rating)
- 하트 (favorite)
- 자물쇠 (lock)

---

## 5. 컴포넌트 (간략)

### 5.1 카드

```css
.wa-card {
  border-radius: 28px;          /* 레퍼런스의 둥근 모서리 */
  padding: clamp(24px, 3vw, 36px);
  position: relative;
  overflow: hidden;
  min-height: 260px;
  display: flex; flex-direction: column; gap: 14px;
}
/* 큰 마스코트 카드는 36px, 작은 텍스트 카드는 28px */
.wa-card.is-large { border-radius: 36px; min-height: 320px; }
```

**카드 안 일러스트 배치**: 우측 하단 또는 가운데 하단. 본문 텍스트 우측을 살짝 비워두고 그곳에 일러스트.

### 5.2 CTA 버튼 (pill)

레퍼런스 "Get a demo" 톤:
```css
.wa-btn {
  background: var(--wa-text);     /* 검정 */
  color: #FFFFFF;
  border-radius: 999px;
  padding: 14px 24px;
  font-size: 15px;
  font-weight: 600;
  font-family: var(--wa-font);    /* Pretendard — 가독성 */
}
.wa-btn-ghost {
  background: transparent;
  color: var(--wa-text);
  border: 1.5px solid var(--wa-text);
}
```

### 5.3 카드 그리드 (비대칭 12-칸)

레퍼런스 배치 패턴:
- **A형 (5+7)** — 좌측 작은 카드 + 우측 큰 마스코트 카드
- **B형 (7+5)** — 좌측 큰 마스코트 카드 + 우측 작은 텍스트 카드
- **C형 (4+4+4)** — 3개 동일 크기 카드
- **D형 (5+4+3)** — 비대칭 3개
- 한 섹션 안에서 **두 줄 이상** 으로 묶어 마치 마손리(masonry) 처럼 보임

```css
.wa-grid { display: grid; grid-template-columns: repeat(12, 1fr); gap: 20px; }
.wa-card.span-3  { grid-column: span 3; }
.wa-card.span-4  { grid-column: span 4; }
.wa-card.span-5  { grid-column: span 5; }
.wa-card.span-7  { grid-column: span 7; }
.wa-card.span-8  { grid-column: span 8; }
.wa-card.span-12 { grid-column: span 12; }
```

---

## 6. 섹션 매핑 (도담도담 컨텐츠)

| Aboard 섹션 | 도담도담 매핑 | 핵심 일러스트 |
|---|---|---|
| Hero "Bring joy..." | "아이의 작은 신호에 빠르게 답하는 가족." | 핑크·노랑 구름 2개 + 디바이스 mockup |
| Employees — A dedicated space | **For parents — 부모를 위한 공간** | 5 카드 (증상기록 + 핑크구름 / 근처병원 + 핀 / 리뷰 + 별 / 사진보관 + **메모 3장** / 알림 + 종) |
| Manage absences | **늦은 밤에도, 휴일에도 — 야간 + 휴진** | 캘린더 mockup + **큰 오렌지 구름 마스코트** |
| HR essentials | **진료의 핵심을, 단순하게** | 의사 프로필 카드 + 라임그린 People data + 다크그린 Bulk + 라벤더 Whistle + 라이트그린 Analytics (구름 3개) |
| Onboarding / Pre-boarding | **새 부모를 자연스럽게 안내** | 단계별 mockup + **꽃 마스코트 (Pre-boarding 핑크 카드)** |
| Documents / E-signing | **모든 진료 기록을 한 곳에** | 베이지 정렬 카드 + 큰 블루 보안 카드 + 인증 pill |

---

## 7. 현재 코드 vs 레퍼런스 — 개선 우선순위

(현재 `index.html` 의 `BASE_STYLE_WA` / `HOME_BODY_WA` / `WA_SVG` 와 비교한 차이)

| 우선순위 | 항목 | 현재 | 개선안 |
|---|---|---|---|
| 🔴 높음 | **오렌지 컬러 누락** | 없음 | `--wa-orange #FF8E47` 추가 → "늦은 밤에도, 휴일에도" 의 두 번째 카드 배경으로 큰 오렌지 구름 마스코트 |
| 🔴 높음 | **메모 3장 마스코트** | 단순한 SVG 1개 (작음) | 옐로우/핑크/그린 3장 각도 다르게 겹친 풀크기 SVG, 카드 우측 하단에 크게 |
| 🔴 높음 | **꽃 마스코트 — 가운데 얼굴** | 줄기는 있는데 가운데가 옅음 | 큰 옐로우-soft 얼굴 + 표정 강조 |
| ✅ 정정 | **마스코트 외곽선** | 검정 2px 적용 시도 → 톤 무거워짐 | **제거**. outline-less 평면 컬러 + drop-shadow 가 레퍼런스 감성 |
| 🟠 중간 | **카드 색 분포** | 옐로우 1, 라벤더 2, 그린 1 | 옐로우 비중 늘리기 (4-5개) + 오렌지 1개 추가 |
| 🟠 중간 | **무지개 그라데이션** | 4 색 stop | 오렌지를 stop 으로 추가 (핑크→옐로우→**오렌지**→라임→라벤더) |
| 🟡 낮음 | **카드 라운드** | 28px 균일 | 큰 마스코트 카드는 36px 로 더 둥글게 |
| 🟡 낮음 | **별 마스코트 face** | 작은 face | face 좀 더 크게 + 표정 강조 |

---

## 8. 다음 단계

1. 본 design.md 의 컬러/일러스트 새 정의를 **`index.html` 의 `BASE_STYLE_WA` 와 `WA_SVG` 에 반영** — 코드 작업 단계.
2. 반영 후 `dodam_home.html` 재빌드 + 브라우저에서 레퍼런스와 옆에 두고 비교.
3. 디테일 보정 (마스코트 크기·위치·표정 라운드).
