# design.md — Softer Volumes 디자인 시스템 추출

> 레퍼런스: https://shop.softervolumes.com/
> 추출일: 2026-05-28 KST (Claude Code, 브라우저 computed-style 직접 측정)
> 용도: 프렌치 스타일 카페 웹사이트 테마의 디자인 토큰 베이스

---

## 한 줄 요약

**미니멀 에디토리얼 + 타이트 그리드.** 화이트 배경에 거의 검정(#222) 텍스트, Inter 산세리프, 거대한 라이트웨이트 헤딩.
제품(메뉴) 셀은 **1px 헤어라인 gap 으로만 분리된 full-bleed 그리드** — 여백 없이 빽빽하게 붙는다.
사진은 웜 뉴트럴 톤의 인테리어/제품 컷이 화면을 가득 채운다.

이 톤은 기존 프로젝트의 Clarkson(크림 베이스) 과 다르다 → **새 테마 토큰 세트**로 다룬다 (덮어쓰기 아님).

---

## 1. 컬러 토큰

브라우저에서 실측한 사용 빈도 상위 색상 기준.

| 역할 | hex | rgb | 비고 |
|---|---|---|---|
| 배경 (메인) | `#FFFFFF` | 255,255,255 | 순백 |
| 텍스트 (강조/본문) | `#222222` | 34,34,34 | 거의 검정, 최다 사용 (1316회) |
| 헤어라인 보더/구분선 | `#E5E7EB` | 229,231,235 | 그리드 셀 사이 1px 라인 (880회) |
| 웜 베이지 (섹션 밴드) | `#D9D1C5` | 217,209,197 | "Cafes Book" 타이틀 밴드 배경 |
| 딥 베이지 (악센트) | `#C8BEB4` | 200,190,180 | 셀 배경 등 보조 |
| 보조 텍스트 | `#6B6B6B` 근사 | — | 캡션/메타 (회색조) |
| Shop 버튼 보라 | `#5A31F4` | — | Shopify 결제 전용 (우리 테마에선 미사용) |

### 의미색 매핑 제안 (`:root` 토큰)

```css
--sv-bg-base:    #FFFFFF;   /* 페이지 배경 */
--sv-bg-band:    #D9D1C5;   /* 섹션 타이틀 밴드 (웜 베이지) */
--sv-bg-cell:    #C8BEB4;   /* 이미지 없는 셀 폴백 */
--sv-text-str:   #222222;   /* 헤딩 / 강조 */
--sv-text-pri:   #222222;   /* 본문 */
--sv-text-mut:   #6B6B6B;   /* 캡션 / 메타 / 가격 보조 */
--sv-line:       #E5E7EB;   /* 1px 헤어라인 (그리드 gap, 구분선) */
--sv-line-str:   #222222;   /* 강조 보더 (버튼 외곽선) */
```

> Clarkson 토큰(`--raw-bg-base: #F5F1EA` 등)과 **병행**한다. 새 테마는 `sv-` 프리픽스로 격리.

---

## 2. 타이포그래피

| 항목 | 값 | 비고 |
|---|---|---|
| 폰트 패밀리 | `Inter, sans-serif` | 라틴. 한글은 **Pretendard** 페어링 (프로젝트 표준, 유사 지오메트릭 산세) |
| 본문 크기 | `17px` | weight 400 |
| 본문 line-height | `1.2` (20.4/17) | 타이트한 행간 |
| 본문 색 | `#222222` | |
| letter-spacing | `normal`~`-0.01em` | 헤딩에서 살짝 음수 |
| text-transform | `none` | **대문자 변환 없음** (내비/캡션 모두 sentence case) |

### 헤딩 스케일 (관찰)

- 섹션/제품 타이틀이 **매우 큼** (데스크탑 ~56–72px) 인데 **weight 400 (regular)** — bold 가 아니라 큰 사이즈로 존재감을 낸다. 가볍고 우아한 느낌.
- 내비게이션/캡션은 본문과 동일한 17px 안팎, weight 400.

```css
--sv-font: 'Inter', 'Pretendard', sans-serif;
--sv-fs-body:   17px;
--sv-fs-cap:    15px;
--sv-fs-h-sm:   28px;
--sv-fs-h-md:   44px;
--sv-fs-h-lg:   64px;   /* 섹션 밴드 타이틀 */
--sv-lh-tight:  1.05;   /* 큰 헤딩 */
--sv-lh-body:   1.2;
--sv-fw-reg:    400;
--sv-fw-med:    500;
```

> 프로젝트 규칙: **한글 italic 절대 금지.** 강조는 weight/자간/컬러로만.

---

## 3. 레이아웃 — 타이트 그리드 (시그니처)

이 사이트의 정체성. **12컬럼 그리드 + 1px gap.**

| 항목 | 값 |
|---|---|
| 그리드 컬럼 | `grid-template-columns: repeat(12, 1fr)` (데스크탑) |
| gap | **`1px`** (= 헤어라인). `gap-gridline` / `gap-gutter` 유틸로 명명됨 |
| gap 색 | 그리드 컨테이너 배경을 `#E5E7EB` 로 깔고 셀을 `#FFF`/이미지로 채워 1px 라인처럼 보이게 함 |
| 모바일 | `grid-cols-1` 또는 `grid-cols-2` 로 축소 |
| 셀 내부 | **패딩 0, 라운드 0** — 이미지가 셀을 꽉 채움 (object-fit: cover) |
| 셀 비율 | 정사각형~세로형 (제품은 4:5 근사) |

### 메뉴 그리드에 적용할 패턴

사용자 요구 = "여백 없는 타이트한 그리드에 메뉴들". 정확히 이 패턴:

```css
.sv-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);      /* 모바일 2열 */
  gap: 1px;
  background: var(--sv-line);                  /* gap 이 헤어라인으로 보임 */
}
@media (min-width: 768px) {
  .sv-grid { grid-template-columns: repeat(4, 1fr); }  /* 카페 메뉴는 4열 권장 */
}
.sv-cell {
  background: var(--sv-bg-base);
  /* 패딩 없음, 라운드 없음 */
}
.sv-cell img { width: 100%; aspect-ratio: 4/5; object-fit: cover; display: block; }
```

### 섹션 타이틀 밴드

- 그리드 위에 **웜 베이지(`--sv-bg-band`) 풀폭 밴드** + 좌측 정렬 거대 헤딩.
- 위아래로 hero 이미지(full-bleed) → 밴드 → 그리드 순서가 반복되는 리듬.

---

## 4. 컴포넌트 스타일

### 헤더 / 내비게이션
- 상단 **마퀴 티커**(좌→우 흐르는 공지 텍스트, "Just Launched…" 반복) — 옵션 요소.
- 그 아래 **3분할 내비바**: 좌측 메뉴 링크 그룹 / 중앙 로고(워드마크, 대문자 자간 넓게 `SOFTER VOLUMES`) / 우측 유틸(지역·계정·카트).
- 배경 화이트, 하단 1px 헤어라인.
- 카페 버전: 좌측 = 메뉴/공간/오시는길, 중앙 = 카페 워드마크, 우측 = 예약/인스타 등.

### 제품(메뉴) 셀
- full-bleed 이미지 + 하단 **캡션 바 한 줄**: 이름(좌) · 가격(우), 15px, `#222`.
- 캡션 바는 셀 하단에 얇게, 위로 1px 헤어라인.
- hover 시 두 번째 이미지로 크로스페이드(라이프스타일 컷) — 옵션.

### 버튼 / CTA
- **pill(완전 라운드) 외곽선 버튼**: `border: 1px solid #222; border-radius: 9999px;` 배경 투명, 텍스트 `#222`.
- 라벨 끝에 **화살표** `→` ("Add to cart →" 패턴). 카페에선 "메뉴 보기 →", "예약하기 →".

```css
.sv-btn {
  display: inline-flex; align-items: center; gap: .5em;
  padding: 14px 28px;
  border: 1px solid var(--sv-line-str);
  border-radius: 9999px;
  background: transparent; color: var(--sv-text-str);
  font: 400 17px var(--sv-font);
}
.sv-btn:hover { background: var(--sv-text-str); color: #fff; }
```

### 푸터
- 다단 링크 + 소셜 + 지역 선택 (Shopify 표준). 카페 버전은 간결하게: 주소/영업시간/인스타 + 카피라이트.

---

## 5. 사진 디렉션

- **웜 뉴트럴 톤** — 따뜻한 베이지·브라운·자연광. 채도 낮고 그림자 풍부.
- 인테리어/오브제/라이프스타일 컷이 **화면을 가득** 채움 (full-bleed, 여백 최소).
- 카페 버전: 같은 톤의 **카페 내부 인테리어 사진 다량** (자연광 창가, 우드/라탄 가구, 원목 카운터, 라떼·디저트 클로즈업).
- 프로젝트 규칙: **Unsplash 에서 직접 다운로드 → 육안 확인 → 톤 일관 컷만 큐레이션.** ID만 박지 않음.

---

## 6. 톤 키워드

`미니멀` · `에디토리얼` · `웜 뉴트럴` · `타이트 그리드` · `라이트웨이트 대형 헤딩` · `풀블리드 사진` · `헤어라인 디테일` · `차분한 부티크`

---

## 7. 카페 사이트 적용 매핑 (요약)

| 레퍼런스 요소 | 카페 사이트 대응 |
|---|---|
| 상단 마퀴 티커 | 공지(영업시간/신메뉴) 또는 생략 |
| 3분할 내비 + 워드마크 | 카페 로고 + GNB (메뉴/공간/오시는길) |
| hero full-bleed 사진 | 카페 외관/시그니처 컷 hero |
| 웜 베이지 섹션 밴드 + 대형 헤딩 | "Menu", "Our Space", "Visit" 섹션 타이틀 |
| 1px gap 12→4컬럼 그리드 | **카페 메뉴 그리드** (요구사항 핵심) |
| 제품 캡션(이름·가격) | 메뉴명 · 가격 |
| full-bleed 사진 반복 리듬 | **인테리어 감성 사진 다량** (방문 유도) |
| 푸터 | 주소/영업시간/지도/인스타 |
| (신규) | **찾아오는 곳 — 다음(카카오)지도 임베드** |

> 다음 단계: 이 design.md + `tistory_structure.md` 를 합쳐 페이지 매핑표를 만들고,
> 테마 코드(skin.html/style.css) 와 본문 HTML 스니펫으로 분할한다.
