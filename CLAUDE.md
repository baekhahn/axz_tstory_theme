# 티스토리 테마 프로젝트 — Miterlab

> Claude Code 세션 인계 문서. 새 세션 시작 시 자동 로드됩니다.
> 마지막 갱신: 2026-05-19 KST

---

## 한 줄 요약

마이터랩(Miterlab) 의 **티스토리 멀티 테마 프로젝트**.
티스토리의 표준 포스팅 구조(카테고리/제목/사진/글/댓글 등)를 기반으로,
**디자인 톤(Clarkson 베이스)** 은 통일하면서 **포스팅·홈 화면을 모듈 단위 variant** 로 분기해서
"블로그" 와 "웹사이트(캠페인 페이지)" 양쪽으로 변형 가능한 모듈 시스템을 만든다.

**프로토타입 단계**. 현재는 디자인·구조 검증 중이고, 이후 티스토리 변수 치환(`[##_article_rep_title_##]` 등)으로 실제 스킨 패키징 예정.

---

## 작업 디렉토리

- 로컬: `/Users/baekhahnwork/Documents/Baek_Codex/tstory_theme`
- 원격: https://github.com/baekhahn/axz_tstory_theme (Public, `main` 브랜치)
- 라이브 미리보기: https://baekhahn.github.io/axz_tstory_theme/ (GitHub Pages)

---

## 파일 구조

```
tstory_theme/
├── index.html                       # 통합 미리보기 셸 (좌측 sidenav + 우측 패널)
├── clarkson_base_theme.html         # 새 창 - 전체 테마 기본형 (카드 리스트)
├── clarkson_campaign_theme.html     # 새 창 - 전체 테마 캠페인형 (풀폭 알터네이트)
├── post_detail.html                 # 새 창 - 게시글 상세 (Stanton 블로그형)
├── CLAUDE.md                        # (이 문서)
├── .gitignore                       # .DS_Store, old/ 제외
├── old/                             # 구버전 백업 (push 제외)
└── .claude/                         # Claude Code 설정
```

3개 풀스크린 HTML 파일은 `index.html` 안 TEMPLATES 객체에서 추출하여 빌드된 것.
즉 **index.html 의 TEMPLATES 가 단일 source of truth** 이고, 3개 파일은 빌드 산출물.

---

## 빌드 방법 (3개 풀스크린 파일 재생성)

`index.html` 안의 TEMPLATES 객체를 수정한 뒤, 변경 내용을 풀스크린 파일에도 반영해야 함.

```bash
node -e "
const fs = require('fs');
const html = fs.readFileSync('index.html', 'utf8');
const m = html.match(/const TEMPLATES = ({[\s\S]*?});/);
const T = eval('(' + m[1] + ')');
const wrap = (key, title) => \`<!DOCTYPE html><html lang=ko><head><meta charset=UTF-8><title>\${title}</title></head><body>\${T[key]}</body></html>\`;
fs.writeFileSync('clarkson_base_theme.html', wrap('theme-base', '전체 테마 — 기본형'));
fs.writeFileSync('clarkson_campaign_theme.html', wrap('theme-campaign', '전체 테마 — 캠페인형'));
fs.writeFileSync('post_detail.html', wrap('post', '게시글 상세'));
"
```

(실제 빌드 시에는 wrapDoc 함수와 동일한 형태로 토큰/컴포넌트 CSS 전체 주입 필요. 위는 단순화 예시 — index.html 의 `wrapDoc()` 함수 참고.)

---

## 디자인 시스템 (Clarkson 톤)

`:root` 에 정의된 디자인 토큰. 두 단계 추상화:
1. `--raw-*` (원색)
2. `--color-*` (의미색) — 컴포넌트에서 사용

### 컬러 토큰

| 토큰 | hex | 용도 |
|---|---|---|
| `--raw-bg-base` | `#F5F1EA` | 크림 배경 (메인) |
| `--raw-bg-elev` | `#FFFFFF` | 카드/엘리베이션 |
| `--raw-bg-muted` | `#EDE7DC` | muted 영역 |
| `--raw-bg-inv` | `#1F1D18` | 다크 반전 (sidenav, dark 섹션) |
| `--raw-text-str` | `#1F1D18` | 강조 / 헤딩 |
| `--raw-text-pri` | `#2A2722` | 본문 |
| `--raw-text-mut` | `#6B6760` | 보조 |
| `--raw-text-sub` | `#A09B91` | 더 보조 |
| `--raw-text-inv` | `#F5F1EA` | 다크 위 텍스트 |
| `--raw-border-def` | `#DBD4C7` | 기본 보더 |
| `--raw-border-str` | `#C5BCAB` | 강한 보더 |
| `--raw-border-sub` | `#E8E2D6` | 약한 보더 |

### 타이포

- 폰트: **Pretendard** (마이터랩 표준, jsdelivr CDN)
- weight 600–700 큰 디스플레이 헤딩, weight 400–500 본문
- letter-spacing 적극 사용 (헤딩 음수, 라벨 양수)

### 셸 UI (index.html)

- 좌측 sidenav: 다크 (`--raw-bg-inv`) + 라이트 텍스트
- 우측 패널: 라이트 (`--raw-bg-base`) + 다크 텍스트
- 패널 헤더에 `panel-title` + `panel-file` (현재 화면의 파일명 표시) + "새 창에서 열기 ↗"

---

## 라우팅과 새 창 동작

**해시 라우팅** (file:// 호환). query string (`?preview=1`) 은 file:// 에서 누락되므로 사용 금지.

| 패널 / variant | 해시 라우트 | 새 창 링크 (정적 파일) |
|---|---|---|
| 전체 테마 / 기본형 | `#theme-base` (또는 `#theme` alias) | `clarkson_base_theme.html` |
| 전체 테마 / 캠페인형 | `#theme-campaign` | `clarkson_campaign_theme.html` |
| 게시글 상세 | `#post` | `post_detail.html` |

- 셸 내 미리보기는 iframe srcdoc 으로 TEMPLATES 콘텐츠 주입
- "새 창에서 열기 ↗" 는 `<a target="_blank" rel="noopener" href="정적파일.html">` — 브라우저 기본 동작 사용
- 라우트 전환 시 `activateRoute()` 가 a 태그의 href 도 함께 동기화

---

## 콘텐츠 톤

- 블로그 이름: **공간노트** (Notes on Architecture & Spaces)
- 작성자: **백희**
- 주제: 건축 / 공간 / 인테리어 에세이 ("건축에 대한 깊은 사고")
- 사진: **Unsplash architecture-interior 카테고리만 사용** (`images.unsplash.com/photo-{id}?...&fit=crop&q=75&auto=format`)
- picsum.photos, lorem ipsum 등 일반 더미 사용 금지

### 홈 카드 5개 (`clarkson_base_theme.html`)

1. 건축에 대한 깊은 사고 — 짓는 일이 아니라 묻는 일이다
2. 빛은 가장 비싼 재료입니다 — 그러나 가장 공짜입니다
3. 좋은 계단은 발이 먼저 알아봅니다
4. 사무실은 왜 점점 거실을 닮아가는가
5. 오래된 주방이 가르쳐주는 것

### 메인 게시글 본문 (`post_detail.html`)

- H1: 건축에 대한 깊은 사고 — 짓는 일이 아니라 묻는 일이다.
- 섹션: 질문이 먼저 / 빛은 시간을 운반한다 / 비례는 몸이 알아본다 / 재료는 시간을 기억한다
- Juhani Pallasmaa 인용

---

## 티스토리 표준 정합성 (옵션 A 완료)

이전 세션에서 **티스토리 기본 스펙에 없는 요소를 모두 제거**했음.

### 제거됨

- 뉴스레터 구독 폼·밴드·CTA
- "읽는 시간 N분" 메타
- 헤더 메뉴 Archive / About
- 푸터 다단 그리드 (Read / Follow / Contact)

### 표준 메뉴로 단순화

- 헤더 메뉴: **홈 / 태그 / 방명록** (티스토리 표준 GNB)
- 푸터: 카피라이트 한 줄 (© 공간노트 / Powered by Tistory · Theme by Miterlab)

### Dead CSS 잔존 (의도)

최소 변경점 원칙에 따라 HTML 마크업만 제거하고 CSS 룰은 dead code 로 남김. 다음 작업 시 일괄 정리 가능.

남은 dead 룰: `.newsletter-band*`, `.newsletter-form*`, `.site-footer-inner`, `.footer-brand-block`, `.footer-col*`, `.clp-cta*`, `.btn-light`, `.btn-outline-light`

---

## 현재 활성 / 향후 작업

### 활성 패널 (3개 라우트)

- `#theme-base` — 전체 테마 기본형
- `#theme-campaign` — 전체 테마 캠페인형
- `#post` — 게시글 상세 (Stanton 블로그형)

### TODO: 비활성 슬롯 7개 (sidenav 에 disabled 로 자리만 잡혀있음)

헤더 · 푸터 · 사이드바 · 홈 목록 · 페이지네이션 · 태그 · 방명록

각 슬롯도 variant 비교 가능한 패널로 확장 예정.

### 다음 단계 후보

1. 캠페인형(`#theme-campaign`) 콘텐츠를 "홈" 다운 구성(블로그 소개·여러 글·CTA)으로 재구성
2. 헤더/푸터 variant 패널 활성화
3. 사이드바 variant (블로그 모드용)
4. 다른 디자인 테마 추가 (Stanton 톤, 카카오옐로우 톤 등 — 토큰 갈아끼우기)
5. dead CSS 룰 일괄 정리
6. 티스토리 변수 치환 단계 (`s_blog_title`, `[##_article_rep_title_##]` 등)

---

## 알아두면 좋은 함정

1. **`</script>` 이스케이프** — JS 의 template literal 안에 `</script>` 가 그대로 있으면 HTML 파서가 외부 스크립트 종료로 오인. 반드시 `<\/script>` 로 escape.
2. **`href="#"` 클릭 가드** — 모든 빈 앵커는 페이지 점프 차단. `wrapDoc()` 함수가 모든 iframe srcdoc 에 가드 스크립트를 자동 주입함. 새 a 태그 추가 시 별도 처리 불필요.
3. **file:// 의 query string 손실** — Safari 등 일부 브라우저는 `file:///...?preview=1` 의 query 를 누락. 모드 전환은 반드시 hash 로.
4. **이모지 절대 금지** — 셸 UI, 콘텐츠, 어디에도 사용하지 않음 (사용자 명시 규칙). 이전 시도들에서 🎨 📄 ✅ 등 모두 제거 완료.
5. **Unsplash 외 이미지 금지** — picsum.photos / placeholder.com 등 일반 더미 사용 금지. architecture-interior 카테고리 사진만.
6. **빌드 동기화** — `index.html` 안 TEMPLATES 수정 시 3개 풀스크린 파일도 재빌드 필요. 잊으면 미리보기와 새 창이 어긋남.

---

## 작업 원칙 (전역 + 프로젝트)

전역 규칙(`~/.claude/CLAUDE.md`) 상위 규칙 그대로 적용. 핵심만:

- 정중한 존댓말, 반말 금지
- 시각 표기 KST (UTC 금지)
- **배포 권한**: 사용자가 명시적으로 "배포해" 라고 해야 push/deploy 진행. 수정→빌드→커밋→푸시→배포 체이닝 금지
- 한 번에 한 단계씩, 사용자 확인 후 다음 단계
- 운영 안전: 운영 영향 변경은 사전 명시 승인 필요
- 모델: Sonnet/Opus 만 사용 (Haiku 금지)

### 이 프로젝트 추가 규칙

- **이모지 금지** (UI/문서/콘텐츠 어디에도)
- **이미지는 Unsplash architecture-interior 카테고리만**
- **최소 변경점 원칙** — 작업 범위 밖 코드는 건드리지 않음 (dead CSS 도 그대로)
- **빌드는 단일 source of truth (`index.html`)** → 풀스크린 파일은 재생성

---

## 변경 이력 요약

이전 세션 (Claude.ai 웹) 에서 진행한 단계:

1. 첨부 스킨 (`tstory_theme_basic.html`) 분석 — 9패널 통합 미리보기 구조 파악
2. Stanton / Clarkson Squarespace 사이트 분석 — 블로그/웹사이트 변형 패턴 추출
3. 모듈화 설계 (토큰 → 컴포넌트 → 레이아웃 모드 → 화면)
4. 1차 프로토타입 `index.html` 생성 (셸 + 2패널 활성)
5. 이미지 교체 (picsum → Unsplash 13장) + 콘텐츠 교체 ("공간노트" 건축 에세이)
6. `href="#"` 클릭 점프 차단 가드 스크립트 추가
7. 옵션 A 적용 — 티스토리 표준 외 요소 제거 (뉴스레터/Archive/About/읽는시간/다단푸터)
8. 이모지 4건 제거
9. 패널 재구성 — 전체 테마 패널에 variant 2종(기본/캠페인), 게시글 패널은 단일화
10. URL 라우팅 도입 — 해시 기반 (`#theme-base` / `#theme-campaign` / `#post`)
11. "새 창에서 열기" 동작 — `<a target="_blank">` + 정적 파일 직접 링크로 단순화 (3개 풀스크린 파일 빌드)

이번 세션 (Claude Code) 에서 진행한 단계:

12. GitHub 리포지토리 (`baekhahn/axz_tstory_theme`) Private → Public 전환
13. git 초기화 + 4개 파일 push (`old/`, `.DS_Store` 제외)
14. GitHub Pages 활성화 (main 브랜치, root) — https://baekhahn.github.io/axz_tstory_theme/
15. 이 핸드오프 문서 (`CLAUDE.md`) 작성

---

## 작업 시 컨벤션

### 검증 체크

코드 수정 후 매번 확인:

```bash
# 이모지 잔존 (반드시 0)
grep -cE '[🎨📄✅⚠️❌]' index.html clarkson_base_theme.html clarkson_campaign_theme.html post_detail.html

# JS 백틱 짝 (template literal 균형)
grep -o '`' index.html | wc -l   # 짝수여야 함

# picsum 잔존 (반드시 0)
grep -c 'picsum' index.html
```

### 풀스크린 파일 재생성

`index.html` TEMPLATES 변경 시 풀스크린 파일도 재빌드. 잊지 말 것.

### 커밋 정책

- 사용자가 "커밋해줘" / "푸시해줘" / "배포해" 라고 명시할 때만 진행
- 한 commit = 한 의미 단위
- 메시지는 의도 중심 ("왜"), 변경 범위 명시

### 로컬 미리보기

```bash
cd /Users/baekhahnwork/Documents/Baek_Codex/tstory_theme
python3 -m http.server 8000
# 또는 그냥 index.html 더블클릭 (file:// 도 정상 동작)
```

URL: http://127.0.0.1:8000/  (localhost 대신 127.0.0.1 사용)
