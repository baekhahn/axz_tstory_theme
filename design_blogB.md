# Blog B — Re-Store 톤 (San Francisco Edition)

> 작성일: 2026-05-20 KST
> 디자인 레퍼런스: https://re-store.io/index.html
> 콘텐츠 주제: San Francisco 도시 소개 (영문)
> 이미지: Unsplash architecture / travel
> 폰트: **Pretendard** (Graphik Web 의 대체)

---

## 1. 톤 키워드

**캠페인 사이트 / 매시브 타이포 / 좌측-라벨 우측-텍스트 이단 / em-dash 시그니처 / 모노톤 + 단일 액센트**

Clarkson(Blog A) 가 "editorial · 카드 리스트 · 크림" 톤이라면, Re-Store(Blog B) 는 **"광고 캠페인 · 풀폭 hero · 화이트"** 톤.

---

## 2. 컬러 토큰

### Raw

| 토큰 | hex | 용도 |
|---|---|---|
| `--raw-bg-base` | `#FFFFFF` | 메인 배경 (흰) |
| `--raw-bg-inv` | `#1E1E1E` | 다크 반전 (CTA 버튼 배경) |
| `--raw-bg-tint` | `#F4F1ED` | 매우 옅은 톤 (섹션 alternation 용, 옵션) |
| `--raw-text-str` | `#1E1E1E` | 강조 / 헤딩 / 본문 |
| `--raw-text-mut` | `#6B6B6B` | 보조 |
| `--raw-text-sub` | `#A0A0A0` | 더 보조 / 캡션 |
| `--raw-text-inv` | `#FFFFFF` | 다크 위 텍스트 (헤더 hero, CTA) |
| `--raw-border-def` | `#E5E5E5` | 기본 보더 |
| `--raw-border-sub` | `#F0F0F0` | 약한 보더 |
| `--raw-accent` | `#D94B27` | **시그니처 액센트** (em-dash, 화살표, 호버) |

### Semantic (Blog B 전용)

```css
--color-bg: var(--raw-bg-base);
--color-bg-inv: var(--raw-bg-inv);
--color-text: var(--raw-text-str);
--color-text-mut: var(--raw-text-mut);
--color-text-inv: var(--raw-text-inv);
--color-border: var(--raw-border-def);
--color-accent: var(--raw-accent);
```

---

## 3. 타이포 (Pretendard 기반)

Re-Store 의 Graphik Web → **Pretendard** 로 대체. Pretendard 는 가변 weight 지원, 라틴/한글 모두 자연스러움.

```css
--font-sans: 'Pretendard Variable', 'Pretendard', -apple-system, ...;
```

### 스케일

| 토큰 | size | weight | letter-spacing | line-height | 용도 |
|---|---|---|---|---|---|
| `--type-massive` | clamp(72px, 11vw, 168px) | 400 | -0.04em | 0.95 | 좌측 거대 라벨 (`Re—shop`) |
| `--type-hero` | clamp(48px, 6vw, 92px) | 500 | -0.03em | 1.0 | hero 헤드라인 |
| `--type-h1` | clamp(36px, 4vw, 56px) | 500 | -0.025em | 1.05 | 페이지 H1 |
| `--type-h2` | clamp(24px, 2.4vw, 32px) | 500 | -0.02em | 1.2 | 섹션 헤드 |
| `--type-body-lg` | 20px | 500 | -0.6px (≈ -0.03em) | 1.4 | 본문 강조 (intro 단락) |
| `--type-body` | 18px | 400 | -0.5px | 1.5 | 본문 |
| `--type-body-sm` | 16px | 500 | -0.56px | 1.25 | 네비, 메타 |
| `--type-caption` | 13px | 400 | 0 | 1.35 | 캡션, 푸터 |

### em-dash 시그니처 처리

`Re—shop`, `San—Francisco` 같이 em-dash 가 들어가는 단어는 em-dash 만 액센트 컬러:

```html
<span class="brand-mark">San<span class="dash">—</span>Francisco</span>
```

```css
.brand-mark .dash { color: var(--color-accent); margin: 0 -.08em; }
```

---

## 4. 레이아웃 패턴

### 4.1 헤더 (Hero variant)

- **포지션**: absolute / fixed (이미지 위 오버레이)
- **로고**: 좌상단, hero 풀화면일 땐 화이트
- **메뉴**: 우측 가로 (예: `Districts · Stories · Food · Events`) + 우측 끝 언어 토글 (`EN`)
- **스크롤 시**: 검정 텍스트로 전환 (옵션 — 초안에선 단순화 가능)

### 4.2 Hero 섹션 (홈)

```
┌─────────────────────────────────────────────────┐
│ [LOGO]              [Menu items]           [EN] │  ← 헤더 (오버레이, 흰 텍스트)
│                                                 │
│ Find a city that lives                          │  ← Hero headline (massive)
│ between fog and ocean.                          │
│                                                 │
│ [● Explore San Francisco]                       │  ← 검정 pill CTA
│                                                 │
│                                                 │
│        [── 풀폭 메인 이미지 (Unsplash SF) ──]     │
│                                                 │
│ ─────────                                        │  ← 가로선
│ San—Francisco                                   │  ← 좌하단 캡션
│ A field guide by the bay                        │
└─────────────────────────────────────────────────┘
```

### 4.3 이단 섹션 (좌측 라벨 + 우측 본문)

Re-shop / Re-brand 패턴.

```
┌───────────────────┬──────────────────────────────┐
│                   │ The fog rolls in every       │
│ San—              │ afternoon, painting the      │
│ Francisco         │ Golden Gate in soft greys.   │
│ (massive)         │                              │
│                   │ How? By trapping cool        │
│                   │ Pacific air against the      │
│                   │ warm inland valley.          │
│                   │                              │
│                   │ ─────────                    │
│                   │ Read the geography  →        │  ← 오렌지 화살표
└───────────────────┴──────────────────────────────┘
```

좌측 라벨: `--type-massive`, 우측 본문: 첫 단락 `--type-body-lg` bold 인트로, 다음 단락 `--type-body`.

### 4.4 풀폭 이미지 + 좌하단 캡션

이미지 위에 absolute 로 캡션 박스 (얇은 가로선 + 작은 텍스트 2줄).

### 4.5 카드 (게시글 목록 — Blog B 의 "Districts" 같은 그리드)

Clarkson 의 카드와 다르게 **이미지가 정사각형**, **캡션 아래 좌정렬**, 보더 없음.

```
┌──────┐ ┌──────┐ ┌──────┐
│      │ │      │ │      │
│ IMG  │ │ IMG  │ │ IMG  │
│      │ │      │ │      │
└──────┘ └──────┘ └──────┘
Mission    Castro    Sunset
The Latin  Rainbow   Where the
heartbeat  crossing  city ends
```

### 4.6 푸터

```
─────────────────────────────────────────
San—Francisco                A field guide
                             © 2026
Districts   Stories   Food   Events   Contact
```

좌측 브랜드 마크 + 우측 짧은 카피, 한 줄 가로선 위에 메뉴 인라인.

---

## 5. 컴포넌트

### CTA 버튼 (Primary)

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 14px 24px;
  background: var(--color-bg-inv);
  color: var(--color-text-inv);
  border-radius: 999px;          /* pill */
  font-size: 16px;
  font-weight: 500;
  letter-spacing: -0.3px;
}
.btn-primary::before {
  content: '';
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--color-accent);  /* dot prefix */
}
```

### 화살표 링크

```html
<a class="arrow-link">Read more <svg>→</svg></a>
```

화살표는 원형 배경(`--color-accent`) + 흰 화살표 SVG.

### 가로선 캡션

```html
<div class="hairline-caption">
  <hr class="hairline">
  <p class="brand-mark">San<span class="dash">—</span>Francisco</p>
  <p class="caption">A field guide by the bay</p>
</div>
```

```css
.hairline { border: 0; border-top: 1px solid currentColor; width: 200px; margin: 0 0 12px; }
```

---

## 6. 간격 / 리듬

- 섹션 패딩: `clamp(80px, 12vh, 160px)` (위·아래)
- 좌우 거터: `clamp(24px, 4vw, 64px)`
- 이단 그리드 갭: `clamp(40px, 6vw, 120px)`
- 본문 단락 간: 16px ~ 24px

---

## 7. 컨텐츠 매핑 (San Francisco)

### 7.1 홈 (전체 테마 — 캠페인형)

- **Hero headline**: "Find a city that lives between fog and ocean."
- **Hero sub**: "A field guide to San Francisco — neighborhoods, light, food, and the people who keep it strange."
- **Hero CTA**: "Explore San Francisco"
- **Hero image**: Unsplash SF skyline / Golden Gate fog

### 7.2 이단 섹션 3개 (광고 캠페인형)

#### Section 1 — San—Francisco
> The fog rolls in every afternoon, painting the Golden Gate in soft greys. By trapping cool Pacific air against the warm inland valley, the city stays cool while California burns. Locals call it Karl.

#### Section 2 — Hill—Light
> Forty-two hills, each one its own weather. Walk Russian Hill at sunset and the bay turns into hammered copper. Walk it at dawn and it's a watercolor of pale blue and salmon.

#### Section 3 — People—First
> A city of immigrants and inventors. The fog doesn't care where you came from. Find your block, find your café, and the city will hold you the way it's held everyone else.

### 7.3 District 그리드 (홈 하단 또는 별도 페이지)

| 라벨 | 한 줄 카피 |
|---|---|
| Mission | The Latin heartbeat |
| Castro | Where the rainbow began |
| Sunset | Where the city ends and the ocean begins |
| North Beach | Italian, beat-poet, all-night |
| SoMa | Concrete and code |
| Richmond | Foggy, quiet, dim-sum |

### 7.4 게시글 상세 — "On Walking the Bridge"

> A long-form essay (Stanton 블로그형으로 재활용 가능). 헤더 hero 이미지 + 큰 H1 + 본문 단락 + 이미지 풀폭 사이사이 삽입. 본문은 글 본문 HTML 모드에서 작성될 부분.

---

## 8. Unsplash 이미지 후보

**카테고리**: travel / san francisco / golden gate
**가이드라인**: `images.unsplash.com/photo-{id}?w=...&fit=crop&q=75&auto=format`

후보 (검증 필요 — 실제 ID 는 사용 시 확정):
- Hero: 골든게이트 + 안개 와이드샷
- Section 1: 안개 낀 다리 클로즈업
- Section 2: 언덕 위 빅토리안 하우스
- Section 3: 케이블카 / 사람들 거리 풍경
- Districts: 각 동네별 거리 사진 (Mission 벽화, Castro 무지개, Sunset 해변, North Beach 카페 등)

> 실제 작업 단계에서 Unsplash 에서 ID 확보 후 적용.

---

## 9. LNB (셸) 구성 — Blog B 활성 시

현 LNB 가 Blog A 기준이므로 Blog B 로 전환되면 화면 리스트가 달라져야 함. 다음과 같이 매핑:

### Blog A — Clarkson · 공간노트

| 섹션 | 화면 | 라우트 |
|---|---|---|
| 화면 (조합 검수) | 전체 테마 (기본형) | `#theme?b=A&v=base` |
|  | 전체 테마 (캠페인형) | `#theme?b=A&v=campaign` |
|  | 게시글 (블로그형) | `#post?b=A` |
| 컴포넌트 (단독 검수) | 헤더 | `#header?b=A&v=...` |
|  | 푸터 | `#footer?b=A` |
|  | (TODO) 사이드바 / 홈 목록 / 페이지네이션 / 태그 · 방명록 | — |

### Blog B — Re-Store · San Francisco

| 섹션 | 화면 | 라우트 |
|---|---|---|
| 화면 (조합 검수) | 전체 테마 (Hero) | `#theme?b=B&v=hero` |
|  | 전체 테마 (Editorial) | `#theme?b=B&v=editorial` (옵션 — 추후) |
|  | 게시글 (Long-form) | `#post?b=B` |
| 컴포넌트 (단독 검수) | 헤더 (Hero overlay) | `#header?b=B&v=hero` |
|  | 푸터 | `#footer?b=B` |
|  | (TODO) ... | — |

### 드롭다운 UI

좌측 sidenav 상단 brand 영역에 Blog 선택 드롭다운:

```
티스토리 테마
[Blog B — Re-Store SF        ▼]
마이터랩 · 1차 통합 미리보기
```

드롭다운 변경 → URL `?b=` 갱신 + LNB 메뉴 리스트 재구성 + 우측 미리보기 재로딩.

---

## 10. 빌드 단계 제안 (이번 세션)

1. `index.html` 안 `:root` 에 Blog B 토큰 (별도 namespace, 예: `body[data-blog="B"] { ... }`) 추가
2. sidenav 상단에 `<select id="blog-switch">` 추가
3. `BLOG_MENUS` 상수에 Blog A / Blog B 의 LNB 메뉴 리스트 정의 → 선택 시 `.sidenav-section` / `.nav-item` 동적 생성
4. `TEMPLATES` 객체에 Blog B 화면 추가: `theme-B-hero`, `post-B`, `header-B-hero`, `footer-B`
5. URL 라우팅 파서 — 기존 `#theme-base` → `#theme?b=A&v=base` 호환 (또는 단순화)
6. SF 영문 컨텐츠 + Unsplash 이미지 채움 (Pretendard CDN 링크 추가)
7. 풀스크린 파일 재빌드 (`clarkson_base_theme.html` 같은 형태로 Blog B 파일도 따로)
8. 로컬 서버 띄우고 사용자 확인
