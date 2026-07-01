# Handoff: QURIO 큐리오 상점 홈페이지 (쿠아 × 조준 방탈출)

## Overview

**과학카페 쿠아(QUA) × 프로젝트 조준** 협업 방탈출 게임 **『큐리오 상점 — 마법 취급합니다』** 의 공식 홍보 홈페이지 디자인입니다.

- **컨셉**: 오래된 마법책(그리무아, Grimoire)의 페이지를 한 장씩 넘겨보는 듯한 빈티지 판타지 무드
- **목적**: 방탈출 게임의 세계관·캐릭터·플레이 방식·엔딩·이용안내를 마법책 챕터 구조로 전달하여, 사용자가 페이지를 스크롤할수록 게임 세계에 몰입되도록 유도
- **주요 타깃**: 대전 여행객, 과학·판타지 콘텐츠에 관심 있는 방문객, 가족 단위 손님
- **전달 형식**: 세로 스크롤 롱 랜딩페이지 (총 8개 챕터/섹션)

---

## About the Design Files

이 번들에 포함된 `index.html` 및 이미지 파일들은 **HTML로 제작된 디자인 참조(prototype)** 입니다. 프로덕션 코드가 아니며, 그대로 배포용으로 붙여넣기 위한 파일이 아닙니다.

개발 담당자의 작업은 이 HTML 목업의 **레이아웃·타이포그래피·컬러·톤 앤 매너·인터랙션**을 그대로 유지하면서, **대상 코드베이스의 기존 프레임워크와 패턴에 맞춰 재구현**하는 것입니다. 예를 들어:

- 기존 코드베이스가 **Next.js/React**라면 컴포넌트를 잘게 쪼개어 서버 컴포넌트/클라이언트 컴포넌트로 나누어 재작성
- **Vue/Nuxt**라면 SFC 구조로 재구성
- **정적 사이트(Astro, Eleventy, Hugo)** 라면 각 챕터를 partial/include로 분리
- **아직 코드베이스가 없는 경우**, 이 홈페이지는 정적 사이트 특성이 강하므로 **Astro** 또는 **Next.js (App Router, 정적 export)** 를 추천합니다. SEO/OG 태그, 이미지 최적화(`next/image` 등), 폰트 프리로드가 자연스럽게 가능합니다.

빈티지 무드가 이 디자인의 정체성이므로, 프레임워크가 바뀌더라도 **폰트 스택, 배경 이미지, 잉크 번짐 SVG 필터, 세피아 컬러 팔레트**는 반드시 그대로 이관되어야 합니다.

---

## Fidelity

**High-fidelity (하이파이)**.

- 최종 컬러 팔레트, 타이포그래피, 스페이싱, SVG 일러스트, 배경 이미지가 모두 확정되어 있습니다.
- 개발자는 **픽셀 단위로 이 디자인을 재현**해야 하며, 임의로 폰트/컬러/여백을 바꾸지 마세요.
- 단, 대상 코드베이스에 이미 확립된 **디자인 토큰/유틸리티 클래스**(예: Tailwind 커스텀 테마)가 있다면, 아래 「Design Tokens」 섹션의 값들을 그 토큰 체계에 맞게 등록해 사용하시면 됩니다.

---

## Screens / Views

이 홈페이지는 **하나의 세로 스크롤 페이지**이며, 8개의 챕터(섹션)로 구성됩니다. 각 챕터는 시각적으로 **한 장의 양피지(page)** 로 표현되며, 어두운 배경 위에 낱장이 얹혀있는 구조입니다.

### 전역 레이아웃 (Global Frame)

- **최상위 배경**: `radial-gradient(ellipse at 30% 20%, #4a3418 0%, #2a1a08 40%, #150a02 100%)` — 어두운 서재/책상 느낌
- **컨테이너**: `.book` — `max-width: 1180px`, 좌우 중앙 정렬, `padding: 40px 24px 80px`
- **개별 페이지**: `.page` — 양피지 배경 이미지가 깔린 카드
  - `background-image: url('assets/bg_page_light.jpg')` (일반 페이지) 또는 `url('assets/bg_page_ornate.jpg')` (`.manual-bg` 클래스가 붙은 경우 — 장식 테두리가 있는 양피지)
  - `background-size: cover`, `background-position: center`
  - `padding: 90px 80px 110px` (일반), `130px 130px 130px` (`.manual-bg`)
  - `min-height: 700px`
  - `box-shadow: 0 30px 60px rgba(0,0,0,0.55), 0 10px 30px rgba(0,0,0,0.35), inset 0 0 120px rgba(120,80,30,0.15)` — 어두운 배경 위에 뜬 종이 느낌
  - `margin-bottom: 48px`
- **가독성 오버레이**: `.page::before` — 페이지 중앙에 반투명 크림색 그라디언트를 얹어 텍스트 가독성 확보
  - `background: radial-gradient(ellipse at center, rgba(252,244,220,0.55) 0%, rgba(252,244,220,0.35) 40%, transparent 75%)`
- **비네트**: `body::before` — 뷰포트 전체에 어두운 비네트, `mix-blend-mode: multiply`

### 페이지 상단 브랜드 바 (`.brand-bar`)

- 모든 페이지 최상단에 고정 위치가 아닌 문서 흐름의 첫 요소로 노출
- 텍스트: `QUA · SCIENCE CAFÉ ✦ PROJECT JOJUN ✦ ANNO MMXXVI`
- 색상: `--sepia (#c9a563)`, `✦`는 `--wax-red-hi (#a83226)`
- 폰트: `Cinzel`, 11px, `letter-spacing: 0.3em`

---

### 📖 Chapter I — 표지 (`data-screen-label="01 표지"`)

**Purpose**: 방문자에게 프로젝트의 정체성(QURIO)과 협업 관계(쿠아 × 조준)를 각인.

**Layout**:
- 4모서리 SVG 오너먼트(`.corner-ornament .tl/.tr/.bl/.br`, 90×90px, 상단 24px, 좌우 24px)
- 상단 중앙: 협업 배지 `.collab-badge` (`과학카페 쿠아 × 프로젝트 조준`, 얇은 이중선 테두리, `--ink-soft` 컬러)
- 중앙: 육망성/눈 엠블럼 SVG (140×140px, `--sepia-dark`)
- 아이브로우: `The Curio Shoppe · Est. Long Ago` (Cinzel 12px, letter-spacing 0.35em)
- 메인 로고: `<h1 class="title">QURIO</h1>`
  - Font: **Cinzel 900**, 크기 `clamp(48px, 8vw, 96px)`, letter-spacing `0.08em`
  - Color: `--ink-mid (#4a2f14)`
  - **Filter: `url(#ink-bleed)`** — SVG feTurbulence + feDisplacementMap 필터로 잉크가 종이에 번진 듯한 왜곡 효과 (매우 중요!)
- 서브 타이틀 (한글): `큐리오 상점 — 마법 취급합니다` (Nanum Myeongjo 800, clamp(22px, 3vw, 34px))
- 태그라인: `The Curio Shoppe · Where Magic is Sold` (IM Fell English italic 18px)
- 연도 스탬프: `— MMXXVI · CHAPTER I —`
- **오른쪽 아래 회전된 경고 도장** (`.warning-stamp`): 이중 붉은 테두리, `rotate(-8deg)`, "스토리상 필요한 경우가 아니라면 절대 개봉하지 마시오"

**Interactions**: 없음 (표지 페이지)

---

### 📖 Chapter II — 이야기의 시작 (`data-screen-label="02 이야기의 시작"`)

**Purpose**: 로그라인·시놉시스로 세계관 몰입.

**Layout**:
- 배경: `.page.manual-bg` (장식 테두리 있는 양피지)
- 상단 좌우에 종이테이프 장식 (`.tape.tl`, `.tape.tr` — 대각 줄무늬, 노란색 반투명, `rotate(-4deg)` / `rotate(3deg)`)
- 챕터 표시: `Chapter I · The Beginning` (Cinzel, `--wax-red`, letter-spacing 0.2em)
- 섹션 제목: `이야기의 시작` (Nanum Myeongjo 800)
- 중앙 로그라인: 붉은 색(`--wax-red`) 이탤릭 인용문, IM Fell English 19px
- **2단 컬럼** (`.story-columns`, `grid-template-columns: 1fr 1fr; gap: 60px`)
  - 각 컬럼 첫 문단 첫 글자는 **드롭캡** — UnifrakturCook 64px, `float: left`, `--wax-red`
- 하단 4-cell 인포 박스: 장르 / 무드 / 컨셉 / 세팅
- 우측 하단 손글씨 메모: `.handwritten` (Nanum Pen Script, `--wax-red`, `rotate(-3deg)`)

**Copy (전문 그대로)**:

로그라인:
> "나는 큐리오 마법 상점의 아르바이트생, 아쿠.  
> 설레는 첫 출근날, 마법을 잃고 기괴하게 변해버린 장난감들 뒤에  
> 숨겨진 은밀한 장난의 진실을 파헤쳐라."

시놉시스: (2단으로 나뉨) — 파일 참조

인포 4-cell:
- Genre: 판타지 · 미스터리
- Mood: 성장 · 추리 · 감성
- Concept: 일상이 마법이 되는 순간
- Setting: 과학카페 쿠아 전관

---

### 📖 Chapter III — 등장인물 (`data-screen-label="03 등장인물"`)

**Purpose**: 아쿠(플레이어) · 큐리오 점장 · 요정 세 존재 소개.

**Layout**:
- 3열 그리드 (`.character-grid`, `grid-template-columns: repeat(3, 1fr); gap: 30px`)
- 각 카드 (`.character-card`):
  - 상단/하단 얇은 세피아 라인 (`border-top/bottom: 1px solid rgba(139,105,49,0.5)`)
  - 원형 초상화 (110×110px, `border-radius: 50%`, 이중 테두리, radial gradient `#d4b283 → #8a6931`, inset shadow) — SVG로 직접 드로잉된 캐릭터 일러스트
  - 영문 롤: Cinzel 14px letter-spacing 0.25em `--wax-red` (예: `The Apprentice`)
  - 한글 이름: Nanum Myeongjo 800 20px `--ink-mid`
  - 설명: 14px, line-height 1.7

**세 캐릭터**:
1. **아쿠 (플레이어)** — The Apprentice — 앞치마 + 붉은 넥타이, 검은 앞머리
2. **큐리오 점장** — The Shopkeeper — 실크햇 실루엣, 금빛 눈, 붉은 나비넥타이
3. **요정들** — The Fairies — 반투명 날개 + 별사탕 마법가루

---

### 📖 Chapter IV — 진행 방식 (`data-screen-label="04 진행 방식"`)

**Purpose**: 게임 진행 방식·난이도·소요시간 안내.

**Layout**:
- 배경: `.page.manual-bg`
- 3-스텝 다이어그램 (`.steps`)
  - 각 스텝 번호는 로마자 (`Ⅰ Ⅱ Ⅲ`)를 원형 배지에 표시 (60×60px, 크림색 배경 + 이중 테두리, Cinzel 900 24px `--wax-red`)
  - 스텝 위에 점선 연결선 (`.steps::before` — `background-image: radial-gradient(circle, --sepia-dark 1px, transparent 1.5px); background-size: 8px 2px; repeat-x`)
- 하단 매뉴얼 조판 (`.manual-lines`) — 만년필로 채워 넣은 서식지 스타일
  - `repeating-linear-gradient`로 밑줄 라인 반복 (34px 간격)
  - 각 행은 `키(굵게) · · · · · · 값(dotted leader)` 형식
- 우측 하단 손글씨(영문) 메모: Special Elite 폰트

**Copy**:
- Ⅰ Enter the Shoppe — 상점에 입장하다
- Ⅱ Inspect & Observe — 이상 현상 점검
- Ⅲ Reveal the Truth — 진실에 도달하다

매뉴얼 항목:
- 난이도: 중 (中) · 전 연령 가능
- 소요시간: 약 40분
- 문제 수: 25 ~ 30 문항
- 진행: 비선형 탐색 (Non-linear)
- 기믹: 실물 전시 조작 · 감각 체험 · 추리

---

### 📖 Chapter V — 상점에 진열된 마법 장치들 (`data-screen-label="05 마법 장치"`)

**Purpose**: 카페 쿠아의 실제 과학 전시품 6종을 마법 아이템으로 소개.

**Layout**:
- 3×2 그리드 (`.object-list`, `grid-template-columns: repeat(3, 1fr); gap: 26px 40px`)
- 각 아이템 (`.object-item`): 좌측 60×60px SVG 아이콘 + 우측 텍스트
  - 한글명: Nanum Myeongjo 700 17px `--ink-mid`
  - 영문명: IM Fell English italic 12px `--wax-red`
  - 설명: 13px `--ink-soft`
- 하단 인용 박스: 왼쪽 이중 붉은 세로선 (`border-left: 3px double var(--wax-red)`), 크림색 반투명 배경, 이탤릭

**6개 오브제** (SVG 아이콘은 `index.html` 인라인 참조):

| # | 한글명 | 영문명 | 아이콘 구성 |
| - | --- | --- | --- |
| 1 | CMYK 전구 | CMYK Lights | 백열전구 실루엣 + 소켓 나사산 + 내부 C/M/Y/K 4색 오브(붉은/세피아/검은/속 빈 원) + 방사선 |
| 2 | 오디오 스펙트럼 | Audio Spectrum Visualizer | 8개의 높이 다른 막대 그래프(가운데 최고) + 중앙 대시 기준선 + 상단 사인파 멜로디 |
| 3 | 하늘연꽃 (키네틱아트) | Sky-Lotus | 연꽃 꿃잎 + 줄기 + 반짝임 |
| 4 | 새 시계 | The Cuckoo-Herald | 원형 시계 + 시계바늘 + 상단에 붉은 새 |
| 5 | 태양계 오라리 | The Orrery | 중앙 태양 + 동심원 국도 3개 + 행성 3개 |
| 6 | 토로이드 램프 | Toroid Lamp | 받침대 + 지지대 + 도넛형 유리 튜브 + 중앙 에서 사방으로 뻗어나가는 6갈래 플라즈마 광선 |

※ 이 중 **CMYK 전구**, **오디오 스펙트럼**, **토로이드 램프** 3개 아이콘은 실제 연관 과학 전시품을 묘사하도록 재설계되었습니다. 나머지 3개를 포함해 모두 동일한 라인아트 세피아 스타일(`stroke-width: 1.2`, `stroke="currentColor"`, 반투명 `rgba(139,105,49,x)` 채움, `--wax-red` 강조)를 따릅니다.

---

### 📖 Chapter VI — 엔딩 · 요정마을 별사탕 (`data-screen-label="06 엔딩과 별사탕"`)

**Purpose**: 게임 엔딩이 실제 카페 굿즈(별사탕)로 이어짐을 소개.

**Layout**:
- 2단 그리드 (`.candy-showcase`, `grid-template-columns: 1fr 1fr; align-items: center; gap: 40px`)
- 좌측: 별사탕 유리병 SVG 일러스트 (220×260px)
  - 코르크 뚜껑 + 유리병 몸통 + 컨페토(별사탕) 17개가 색색으로 채워짐
  - `radialGradient` 필터로 유리 하이라이트 표현
  - `filter: drop-shadow(0 8px 16px rgba(0,0,0,0.3))`
- 우측: 텍스트
  - 영문 상단: `FAIRY VILLAGE · KONPEITO` (Cinzel 14px letter-spacing 0.25em `--wax-red`)
  - 헤드라인: Nanum Myeongjo 800 32px — `이 게임의 엔딩은, 당신의 손 안에 남습니다.`

**Copy 정확값**:
> 사건을 해결한 아쿠는 마력난에 처한 요정들에게 **‘요정마을 마법의 별사탕’**을 건네며 위기를 함께 넘깁니다. 이야기가 끝난 뒤, 이 별사탕은 *실제 카페 메뉴*가 됩니다.
  - 본문 2문단
  - 하단 라벨 박스: 이중 붉은 테두리 (`border: 1px double var(--wax-red)`), 크림 반투명 배경, `(요정마을) 별사탕 · 현장에서 시식·구매 가능`

**Copy 정확값**:
> 사건을 해결한 아쿠는 마력난에 처한 요정들에게 **'요정마을 마법의 별사탕'** 을 건네며 위기를 함께 넘깁니다. 이야기가 끝난 뒤, 이 별사탕은 *실제 카페 메뉴* 가 됩니다.

---

### 📖 Chapter VII — 이용 안내 · FAQ (`data-screen-label="07 이용 안내"`)

**Purpose**: 소요시간·인원·난이도·가격 등 실용 정보와 자주 묻는 질문 안내.

**Layout**:
- 배경: `.page.manual-bg`
- 상단 4-cell 정보 그리드 (`.info-grid`, `grid-template-columns: repeat(4, 1fr); gap: 20px`)
  - 각 셀 상하에 `❦` 장식 문자 (세피아 컬러, 60% opacity)
  - 레이블: Cinzel 11px letter-spacing 0.3em
  - 값: Nanum Myeongjo 800 22px `--ink-deep`
- 안내 문구 (이탤릭): "※ 초등학생 이하 어린이는 보호자 동반이 필요합니다."
- 장식 구분선 (`.divider-flourish` — 좌우 얇은 그라디언트 라인 + 중앙 SVG 곡선)
- FAQ 2열 그리드 (`.faq-list`)
  - 각 아이템 하단 점선 구분 (`border-bottom: 1px dashed rgba(139,105,49,0.5)`)
  - Q./A. 접두어는 IM Fell English italic 800 붉은색/세피아

**정보 4-cell**:
- Duration: 40분
- Party Size: 1 – 4인
- Difficulty: 中 (전 연령 가능)
- Entry Fee: 15,000원 / 1인

**FAQ 6개** (전문은 `index.html` 참조)

---

### 📖 Chapter VIII — 방문하기 (`data-screen-label="08 방문하기"`)

**Purpose**: 운영시간, 위치, 방문 CTA.

**Layout**:
- 상단 좌우 종이테이프 장식
- 2열 그리드 (운영시간 | 위치)
- **운영시간 테이블** (`.schedule-table`, `max-width: 500px`):
  - 각 행 하단 점선 구분
  - 휴무일(`.closed`)은 `--wax-red` 이탤릭 IM Fell English로 "— Closed —" 표기
- **위치 카드**: 이중 세피아 테두리, 크림 반투명 배경, 중앙 정렬
  - 붉은 핀 아이콘 SVG (50×50px)
  - 카페명: Nanum Myeongjo 800 22px
  - 영문 부제: Cinzel italic 13px `--wax-red`
  - 주소 본문: 15px `--ink-soft`
- **CTA 버튼** (`.visit-btn`):
  - 배경: `--wax-red (#7a1f14)`, 텍스트 `#f4e0b0`
  - 폰트: Cinzel 700 14px letter-spacing 0.25em
  - `border: 3px double #f4e0b0`
  - 다층 그림자 (외부 + 인셋 하이라이트 + 인셋 로우라이트)
  - `hover`: `translateY(-2px)` + 강한 그림자
  - `::before` / `::after`에 `❦` 장식 문자
- 하단 육망성 SVG 구분선 + 영문 인용문 (IM Fell English italic 20px `--wax-red`) + 한글 해석

**Copy (운영시간)**:
| 요일 | 시간 |
| --- | --- |
| 월요일 · Mon | — Closed — |
| 화 – 금요일 · Tue–Fri | 11:00 – 20:00 (12:00 – 13:00 휴게) |
| 토요일 · Sat | — Closed — |
| 일요일 · Sun | 10:00 – 21:00 |

**위치**:
> 과학카페 쿠아 (QUA) — SCIENCE CAFÉ QUA · DAEDEOK  
> 대전광역시 유성구 신성로61번안길 53  
> 대덕연구개발특구 내 위치

**CTA**: `RING THE BELL` (클릭 시 `alert('운영시간 내 카페 쿠아에 방문해 주세요.')` — 실제 개발 시 예약/문의 페이지 또는 지도 앱 링크로 대체)

---

### Footer

- 상단 장식 구분선 (`.divider-flourish` — 세피아 톤)
- 브랜드 라인: `QUA · SCIENCE CAFÉ × PROJECT JOJUN` (Cinzel letter-spacing 0.3em, `×`는 `--wax-red-hi`)
- 주소 라인: `과학카페 쿠아 (QUA) · 대전광역시 유성구 신성로61번안길 53 / MMXXVI`
- 저작권 (opacity 0.5): `© QUA × JOJUN · The Curio Shoppe · All Curiosities Reserved`

---

## Interactions & Behavior

이 홈페이지는 **정보 전달 위주의 정적 랜딩페이지**로, 인터랙션은 최소화되어 있습니다.

### 필수 인터랙션

| 요소 | 동작 |
| --- | --- |
| `.visit-btn` (RING THE BELL) | Hover 시 `transform: translateY(-2px)` + 그림자 강화 (`transition: transform 0.15s ease`). 클릭 시 alert 노출 (실 서비스에서는 문의 폼/지도 링크로 교체) |
| 페이지 전체 스크롤 | 표준 세로 스크롤 (스무스 스크롤 옵션은 선택적으로 추가 가능) |

### 추가 권장 인터랙션 (선택)

- **스크롤 진입 애니메이션**: 각 `.page`가 뷰포트에 진입할 때 `opacity 0 → 1` + `translateY(20px → 0)`, 700ms ease-out. Intersection Observer 사용 권장.
- **패럴랙스**: 배경 어두운 그라디언트를 스크롤에 따라 미묘하게 이동시키는 효과 (선택).
- **커서**: 데스크톱에서 커서를 깃펜(quill) 아이콘으로 커스터마이즈해도 컨셉과 잘 맞음 (선택).

### 반응형

- **900px 이하** (`@media (max-width: 900px)`):
  - `.page` padding을 `60px 32px 80px`로 축소, `.page.manual-bg`는 `70px 40px 80px`
  - 코너 오너먼트 90px → 60px
  - `.story-columns`, `.character-grid`, `.info-grid`, `.object-list`, `.steps`, `.candy-showcase`, `.faq-list` 모두 1열로 전환
  - `.steps::before` (점선 연결선) 숨김
  - `.warning-stamp` 크기·위치 축소 (`bottom: 30px; right: 30px; font-size: 11px; padding: 6px 12px`)
  - `.tape` (종이테이프) 숨김

### 접근성

- 모든 SVG 장식에 `aria-hidden="true"` 권장
- 링크/버튼 포커스 상태를 별도 스타일링 (현재 목업에는 미포함 — 개발 단계에서 반드시 추가)
- 색 대비 확인: `--ink-mid (#4a2f14)` vs 크림색 배경은 WCAG AA 이상 통과
- 폰트 크기가 clamp()로 반응형이지만, `rem` 기반 리팩터링 권장 (사용자 폰트 확대 지원)

---

## State Management

정적 랜딩페이지이므로 **클라이언트 상태 관리는 최소**합니다.

- 스크롤 위치: 브라우저 기본 (`scroll-restoration: auto`)
- 반응형: CSS 미디어 쿼리만으로 처리
- 폰트 로드 상태: `<link rel="preconnect">` + Google Fonts 사용 (FOUT 최소화를 위해 `font-display: swap` 확인 필요)
- 만약 예약/문의 폼을 추가한다면, 그때 폼 상태 + API 연동 필요

---

## Design Tokens

### Colors (CSS Variables — `:root`에 정의)

```css
--ink-deep:      #2a1a08;   /* 가장 진한 잉크 */
--ink-mid:       #4a2f14;   /* 본문 헤딩 */
--ink-soft:      #6b4a24;   /* 본문 서브 */
--ink-faded:     #8a6a3e;   /* 흐릿한 텍스트 */
--sepia:         #c9a563;   /* 세피아 */
--sepia-dark:    #8a6931;   /* 진한 세피아, 장식 */
--wax-red:       #7a1f14;   /* 실링왁스 붉은색, 강조 */
--wax-red-hi:    #a83226;   /* 밝은 왁스 레드 */
--parchment:     #e8d5a8;   /* 밝은 양피지 */
--parchment-dark:#b89768;   /* 어두운 양피지 */
--gold:          #b58a3d;   /* 골드 액센트 */
```

### Background (root)

```css
background:
  radial-gradient(ellipse at 30% 20%, #4a3418 0%, #2a1a08 40%, #150a02 100%);
```

### Typography

**폰트 스택** (Google Fonts):
- **Cinzel** (400, 500, 700, 900) — 영문 대문자 로마네스크, 헤딩 전용
- **IM Fell English** (400, italic) — 본문 이탤릭, 태그라인
- **IM Fell DW Pica** (400, italic) — 대체 로만
- **UnifrakturCook** (700) — 드롭캡 전용 블랙레터
- **Nanum Myeongjo** (400, 700, 800) — 한글 헤딩 및 강조
- **Gowun Batang** (400, 700) — 한글 본문
- **Nanum Pen Script** — 손글씨 여백 주석
- **Gaegu** (400, 700) — 대체 손글씨
- **Special Elite** — 타자기 스타일 (영문 여백 주석)

**타입 스케일**:

| 용도 | Font | Size | Weight | Letter-spacing |
| --- | --- | --- | --- | --- |
| Hero 제목 (QURIO) | Cinzel | `clamp(48px, 8vw, 96px)` | 900 | 0.08em |
| 한글 서브 타이틀 | Nanum Myeongjo | `clamp(22px, 3vw, 34px)` | 800 | 0.02em |
| 섹션 제목 (영문) | Cinzel | `clamp(30px, 4vw, 46px)` | 700 | 0.12em |
| 섹션 제목 (한글) | Nanum Myeongjo | `clamp(24px, 3.2vw, 32px)` | 800 | 0.01em |
| 챕터 표시 | Cinzel | 18px | 600 | 0.2em |
| 챕터 표시 (한글) | Nanum Myeongjo | 22px | 700 | — |
| 본문 (한글) | Gowun Batang | 16px | 400 | — |
| 아이브로우 | Cinzel | 12px | 500 | 0.35em |
| Info Cell 레이블 | Cinzel | 11px | 500 | 0.3em |
| Info Cell 값 | Nanum Myeongjo | 22px | 800 | — |
| 손글씨 (한글) | Nanum Pen Script | 22px | — | — |
| 손글씨 (영문) | Special Elite | 15px | — | 0.05em |

### Spacing

기준 스케일 (임시): 4 · 8 · 12 · 16 · 20 · 24 · 30 · 40 · 48 · 60 · 80 · 90 · 110 · 130

주요 간격:
- 페이지 간 gap: `margin-bottom: 48px`
- 페이지 내부 padding: `90px 80px 110px` (기본), `130px 130px 130px` (`.manual-bg`)
- 섹션 내부 그리드 gap: `20px ~ 60px` (섹션마다 다름)
- 컨테이너 최대 폭: `1180px`

### Shadows

- **페이지 카드**: `0 30px 60px rgba(0,0,0,0.55), 0 10px 30px rgba(0,0,0,0.35), inset 0 0 120px rgba(120,80,30,0.15)`
- **CTA 버튼**: `0 6px 12px rgba(0,0,0,0.4), inset 0 2px 4px rgba(255,220,180,0.2), inset 0 -3px 8px rgba(0,0,0,0.3)`
- **CTA 버튼 hover**: `0 10px 18px rgba(0,0,0,0.5), inset 0 2px 4px rgba(255,220,180,0.3)`
- **초상화 원형**: `inset 0 4px 12px rgba(60,30,10,0.4)`
- **별사탕 유리병**: `drop-shadow(0 8px 16px rgba(0,0,0,0.3))`

### Border Radius

- 페이지 카드: `3px` (거의 각진 종이 느낌)
- 초상화: `50%` (원형)
- 스텝 번호: `50%` (원형)
- CTA 버튼: 0 (각진 도장 느낌)

### 특수 효과

**잉크 번짐 SVG 필터** (반드시 문서 상단에 정의):

```html
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <filter id="ink-bleed" x="-5%" y="-5%" width="110%" height="110%">
      <feTurbulence type="fractalNoise" baseFrequency="0.85" numOctaves="2" seed="7"/>
      <feDisplacementMap in="SourceGraphic" scale="1.2"/>
    </filter>
    <filter id="ink-bleed-strong" x="-10%" y="-10%" width="120%" height="120%">
      <feTurbulence type="fractalNoise" baseFrequency="0.6" numOctaves="3" seed="3"/>
      <feDisplacementMap in="SourceGraphic" scale="2.5"/>
    </filter>
  </defs>
</svg>
```

주요 헤딩(`h1.title`, `.subtitle-ko`, `h2.section-title`, `h2.section-title-ko`, `h3.chapter-ko`)에 `filter: url(#ink-bleed)` 적용됨. **이 필터는 이 디자인의 정체성이므로 반드시 유지.**

---

## Assets

### 이미지 (배경 텍스처)

| 파일 | 크기 | 용도 |
| --- | --- | --- |
| `assets/bg_page_light.jpg` | 2752 × 1536 | 일반 페이지 배경 (챕터 I, III, V, VI, VIII) — AI 생성, 밝은 크림색 양피지 텍스처 |
| `assets/bg_page_ornate.jpg` | 2752 × 1536 | 장식 테두리 페이지 배경 (챕터 II, IV, VII — `.manual-bg`) — AI 생성, 코너에 나침반/오각별/깃펜 알케미 심볼이 그려진 양피지 |

**개발 팁**:
- 두 이미지는 각 5-6MB로 크므로, 프로덕션 빌드 시 **WebP/AVIF로 변환** 후 `<picture>` 태그로 서빙 권장
- Next.js라면 `next/image` + `placeholder="blur"` 사용
- 반응형 서빙: 데스크톱 원본 + 태블릿(1400px) + 모바일(800px) 3단계 준비

### 아이콘 · 일러스트

모두 **인라인 SVG**로 `index.html`에 포함되어 있으며, 별도 파일 없이 그대로 이관 가능합니다:

- 4모서리 오너먼트 (커스텀 draw)
- 육망성 엠블럼 (Hero)
- 캐릭터 3종 초상화 (아쿠 / 점장 / 요정)
- 오브제 6종 아이콘 (스털링 아메리카노, 뇌 초콜릿, 하늘연꽃, 새시계, 오라리, 자기장)
- 별사탕 유리병 (컨페토 17개 포함)
- 위치 핀 아이콘
- 각종 divider flourish SVG (곡선, 육망성)

### 폰트

Google Fonts에서 CDN 로드. 프로덕션에서는 **셀프 호스팅 + `font-display: swap`** 권장:
```
Cinzel, IM Fell English, IM Fell DW Pica, UnifrakturCook,
Nanum Myeongjo, Gowun Batang, Nanum Pen Script, Gaegu, Special Elite
```

한글 폰트(Nanum Myeongjo, Gowun Batang)는 파일 크기가 크므로 **서브셋(KR 로케일)** 처리 필수.

---

## Files

이 핸드오프 폴더 내부:

- `README.md` — 이 문서
- `index.html` — 홈페이지 원본 목업 (React/Vue 등으로 이관할 때 레이아웃/스타일 기준점)
- `assets/bg_page_light.jpg` — 밝은 양피지 배경
- `assets/bg_page_ornate.jpg` — 장식 테두리 양피지 배경

---

## 개발자 체크리스트

- [ ] SVG `<filter id="ink-bleed">`를 문서 최상단(또는 layout 컴포넌트)에 정의했는가?
- [ ] 9종 웹폰트(영문 5 + 한글 4)가 모두 로드되는가?
- [ ] `.page.manual-bg`와 일반 `.page`가 서로 다른 배경 이미지·padding을 사용하는가?
- [ ] `data-screen-label` 속성이 각 섹션에 유지되었는가? (SEO 및 앵커 네비게이션에 유용)
- [ ] 900px 이하에서 모든 그리드가 1열로 붕괴되는가?
- [ ] CTA 버튼의 alert이 실제 문의/예약 URL로 교체되었는가?
- [ ] 이미지에 alt 텍스트, SVG에 aria-hidden 처리 되었는가?
- [ ] 배경 이미지가 WebP/AVIF로 최적화되었는가?
- [ ] 한글 폰트가 서브셋 처리되었는가?
- [ ] OpenGraph 태그(og:title, og:description, og:image)가 추가되었는가?
- [ ] 카카오톡·페이스북·트위터 공유 시 썸네일이 예쁘게 표시되는가?

---

## 문의

- 디자인 결정 배경, 카피 톤앤매너에 대한 질문은 **송정현 대표(과학카페 쿠아 QUA)** 로 문의
- 방탈출 게임 시나리오 세부 사항은 **프로젝트 조준** 파트너와 확인
