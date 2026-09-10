# 투비AX(TOBE AX) 홈페이지 구조 v3 — as-built
> `index.html` 실제 구현 기준 · 2026.09.09
> 배포: https://kimchul123.github.io/tobis/ · 저장소 `kimchul123/tobis`
>
> **v2(설계 브리프)와의 관계**: v2는 빌드 전 계획(S1–S7)이었고, 실제 구현은 15개 섹션으로
> 갈라졌다. 이 문서는 계획이 아니라 **지금 화면에 있는 것**을 적는다. v2에서 살아남은 것과
> 버려진 것은 §6에 정리했다.

---

## 0. 파일 현황

| 파일 | 크기 | 성격 | 색인 |
|---|---|---|---|
| `index.html` | 346KB / 3,729줄 | **운영본.** 다크/라이트 토글 | 노출 |
| `index2.html` | 33KB | 스토리 안 — 연대기(회사가 주인공) | `noindex` |
| `index4.html` | 29KB | 스토리 안 — 하루(사람이 주인공) | `noindex` |
| `index5.html` | 327KB | 차콜 단일 배색 안 | `noindex` |
| `white/index.html` | 1KB | 구 화이트 URL → 루트로 리다이렉트 | `noindex` |

참고본 셋은 **비교용으로만 유지**한다. 연락처·제품명 같은 공통 사실이 바뀌면 네 곳을 함께 고쳐야 갈라지지 않는다.

**단일 HTML 파일**이다. 외부 CSS/JS 없음. 폰트만 Google Fonts(Noto Sans KR, IBM Plex Mono)를 링크한다.
로고 2종과 오시는길 지도가 base64로 인라인돼 있어 **약 92KB(파일의 27%)** 를 차지한다.

---

## 1. 화면 구조 — 15개 섹션 4막

전용 스크롤 컨테이너(`.scroller`) 안에 `<section>` 15개가 들어간다. 각 섹션은 기본 `min-height:100vh`.

```
HERO
 └ s1     금융의 새로운 표준 / AI Native로 완성하다

1막 · PERSPECTIVE — 세상은 이렇다
 ├ s1c1   01 · 우리의 자리      도메인 20년과 AI가 만나는 자리입니다
 ├ s1c2   02 · 규칙의 변화      다음 규칙은 아직 이름이 없습니다
 ├ s1c4   03 · 개발의 변화      코드는 부산물입니다
 └ s1c7   04 · 기술의 수명      모델은 3개월, 가장 밝은 별도 저뭅니다

2막 · PRODUCTS + SOLUTION — 무엇을 파는가 / 어떻게 만드나
 ├ s3p    PRODUCTS · 무엇을 파는가   설계에서 심사, 지급까지 한 구조 위에 올립니다
 ├ s3d1   SOLUTION 01 · 무엇으로 만드나   커버링크 — 위키가 원본, 코드는 출력
 ├ s3d2   SOLUTION 02 · 어떻게 만드나     위키 작성만으로 80%가 생성됩니다
 ├ s3c4   SOLUTION 03 · 무엇을 만드나     가입설계부터, 새 업무는 '작성'으로 열립니다
 ├ s3c5   SOLUTION 04 · 어떤 구조인가     쓰던 스택 위에 그대로 얹힙니다
 └ s3c8   SOLUTION 05 · 무엇이 달라지나   가입설계의 속도·품질·비용, 구조 자체가 바뀝니다

3막 · 증명
 ├ s2     REFERENCE · AI Track Record   현장에서 구축한 결과로 증명합니다
 └ s4     Project Archive               우리가 걸어온 모든 프로젝트

4막 · 사람과 연결
 ├ s5     Our Team    원본을 쓰는 사람들
 └ s6     Contact Us
```

**id가 순서와 어긋난다.** `s1c4`가 `s1c7`보다 앞, `s3p`가 `s3d1`보다 앞이다. 편집을 거치며 순서만 바뀌고
id는 스크립트·네비게이션·테마 셀렉터가 참조하고 있어 그대로 뒀다. **id를 바꾸려면 6곳의 셀렉터 목록을 함께 고쳐야 한다.**

### 네비게이션
상단 6개 · 모바일 메뉴 6개 · 푸터 4열. `Products`는 별도 항목이 아니라 `Solutions`(→ `#s3p`)에 통합돼 있다.

```
Perspective(#s1c1) · Solutions(#s3p) · Reference(#s2) · Archive(#s4) · Team(#s5) · Contact(#s6)
```

---

## 2. 머릿말 체계

세 규칙으로 통일돼 있다. 새 섹션을 넣을 때 이 문법을 따른다.

1. **아이브로** = `{챕터} {번호} · {질문}` — 구분자는 가운뎃점 하나 (하이픈·엠대시 금지)
2. **h3** = 서술 단정문, `~습니다`로 끝냄
3. **소제목**(`.cl-subh`) = `명사구 — 보충`, 문장형 금지

```
PERSPECTIVE 01 · 우리의 자리        PRODUCTS    · 무엇을 파는가
PERSPECTIVE 02 · 규칙의 변화        SOLUTION 01 · 무엇으로 만드나
PERSPECTIVE 03 · 개발의 변화        SOLUTION 02 · 어떻게 만드나
PERSPECTIVE 04 · 기술의 수명        SOLUTION 03 · 무엇을 만드나
REFERENCE      · AI Track Record    SOLUTION 04 · 어떤 구조인가
                                    SOLUTION 05 · 무엇이 달라지나
```

---

## 3. 제품 — Cover 시리즈 5종

`s3p`에 2계층으로 놓인다. 네이밍 검토 문서는 별도 아티팩트로 있다.

| 계층 | 제품 | 역할 | 상태 |
|---|---|---|---|
| FOUNDATION | **CoverLink** | AI 개발 플랫폼 — 위키가 원본, 코드는 출력 | — |
| FOUNDATION | **CoverStudio** | 에이전트 제작 환경 | — |
| BUSINESS | **CoverPlan** | 가입설계 · 청약 | 실서비스 |
| BUSINESS | **CoverUW** | 언더라이팅 · 심사 | 고도화 중 |
| BUSINESS | **CoverClaim** | 보험금 청구 · 지급 | 준비 중 |

- 카드 셋(Link · Studio · Plan)에 해당 SOLUTION 섹션 링크가 걸려 있다. 힌트 문구는 호버에서만 드러난다.
- `CoverUW`는 요청에 따라 링크를 뺐다. `CoverClaim`은 갈 곳이 없어 링크가 없다.
- ⚠️ **`CoverClaim 준비 중` 배지는 미확인 값**이다. 보험금 지급 관련 수행 실적이 사이트 어디에도 없어 실적처럼 쓰지 않았다. 확인 필요.

**제품군에서 뺀 넷**: `CoverDocs` · `CoverDev`(내부 문서 — 제품 아님) · `CoverSales` · `CoverFee`(영업관리 — 범위 밖).

---

## 4. 인터랙티브 자산

| 섹션 | 자산 | 동작 |
|---|---|---|
| s1 | 별 캔버스 | 시드 고정(20260908) — 새로고침해도 같은 하늘. `ResizeObserver`로 재생성 |
| s1c1 | 도메인×AI 교차 차트 | 데스크톱/모바일 SVG 2벌 |
| s1c2 | 패러다임 타임라인 | 노드 클릭 → 하단 상세 교체. **데스크톱 가로 / 모바일 세로 2벌** |
| s1c7 | 모델 카드 행 + 은하 별자리 | 가로 스크롤 · 별 13개 클릭 → 상세 패널 |
| s1c4 | BEFORE/AFTER 플립 | 버튼으로 원본이 뒤집힘 |
| s3d1 | OKF 파이프라인 · 파일 샘플 | 실제 약관 위키 구조를 반영한 `.md` 샘플 |
| s4 | 연도 필터 | `all / 2026 / 2025-2022 / 2021-2016 / 2015-2012` |
| 전역 | AI 어시스턴트 | 우하단 런처 + 대화 패널 |

### 모바일 대응 패턴
가로로 긴 SVG는 **데스크톱/모바일 2벌 교체**가 원칙이다(`.thc-*` · `.cd-*` · `.tl-*`). 640px 분기.
1000유닛 SVG를 375px에 밀어 넣으면 글자가 약 4.8px로 찍혀 읽히지 않는다.

---

## 5. AI 어시스턴트

우하단 런처(Aurora Spark — 3색 그라디언트 + 회전하는 오로라 링) → 대화 패널.

**백엔드 연결 지점은 `window.TobeChat` 하나다.**

```javascript
window.TobeChat.endpoint = 'https://api.2bis-consulting.com/rag/chat';
window.TobeChat.headers  = { 'X-Api-Key': '...' };
```

| 방향 | 형식 |
|---|---|
| 요청 (POST) | `{ message, history:[{role,content}], page:{url,title} }` |
| 응답 (JSON) | `{ answer, sources:[{title,url}] }` |
| 응답 (스트리밍) | `text/event-stream` — `data: {"delta":"…"}` / `{"sources":[…]}` / `[DONE]` |

- `send()`를 직접 넣으면 호출 전체를 갈아끼울 수 있다.
- 셋 다 비어 있으면 **로컬 FAQ 10항목**으로 답한다(회사소개 / AI 도입 절차 / CoverLink / 가입설계 AI / 하네스 / OKF / 보안·규제 / 실적 / 연락처 / 채용). 답변 아래 근거 칩이 붙는다.
- 추천 질문 5개: `AI 도입, 어떻게 시작하나요?` · `CoverLink가 뭔가요?` · `가입설계 AI 사례` · `투비는 어떤 회사인가요?` · `프로젝트 문의`
- 접근성: ESC 닫기, 열림/닫힘 포커스 이동, 닫힌 동안 `inert`, `aria-live`, 데스크톱만 Enter 전송, `prefers-reduced-motion` 대응. 대화는 저장하지 않는다.
- ⚠️ **로컬 FAQ가 Cover 시리즈를 모른다.** "제품 뭐 있어요?"에 기본 응답으로 빠진다.

---

## 6. 비주얼 시스템

### 색
```
CI Primary  #1A87FE   (Pantone 2727C)   — 채움·보더·큰 활자·그래픽
CI Secondary #2B2B2B  (Pantone 419C)    — 라이트 모드의 잉크
작은 글자용  #0F5FD6  (--blue-ink)      — 흰 배경 5.8:1
보조         #17C3B2 teal · #7C5CFC violet · #22D3A5 mint · #F5A524 amber
```

> **#1A87FE는 브랜드 색이지 본문 글자색이 아니다.** 흰 배경 3.6:1로 AA 미달이라,
> 작은 글자에는 명도를 낮춘 `--blue-ink`를 쓴다. 이 규칙은 CSS 주석에도 박아 뒀다.

### 챕터 리듬
같은 화면이 길게 이어지지 않도록 바닥 톤을 교대시킨다.

| | 다크 | 라이트 |
|---|---|---|
| 기준 톤 | `#0a0e17` | `#F5F8FC` |
| 패널 톤 (SOLUTION 01–04 · ARCHIVE) | `#101627` | `#EBF1F9` |
| 강조 ① SOLUTION 05 | 블루/틸 방사 + `#070b14` | **다크 밴드 `#2B2B2B`** |
| 강조 ② TEAM | 틸/블루 방사 + `#070b14` | **다크 밴드 `#2B2B2B`** |
| 강조 ③ PRODUCTS | 브랜드 틴트 + 패널 톤 | 밝은 브랜드 틴트 |

라이트 모드에서 SOLUTION 05와 TEAM 두 장만 다크 밴드로 눌러 준다. `index5.html`은 이 배색을 전체로 넓힌 안이다.

### 테마 전환
`<style id="themeLight" media="not all">` 를 토글로 켜고 끈다. `localStorage['tobis-theme']`에 저장하고,
`<head>`의 조기 복원 스크립트가 첫 페인트를 맞춰 깜빡임을 막는다.

**인라인 SVG는 `--sv-*` 변수로 색을 뺐다.** 하드코딩하면 라이트에서 사라진다 —
실제로 은하 라벨이 `#DCEBFF`로 박혀 있어 흰 배경에서 안 보이던 것을 `--sv-label-*` 변수로 고쳤다.

### 타이포
`Noto Sans KR` 본문 · `IBM Plex Mono` 아이브로/숫자/코드. 브레이크포인트 `880px` · `640px`.

---

## 7. v2 설계 브리프에서 달라진 것

| v2 계획 | 실제 구현 |
|---|---|
| 7섹션 (S1–S7) | **15섹션 4막** — PERSPECTIVE 4 + PRODUCTS/SOLUTION 6 + 증명 2 + 사람 2 + 히어로 |
| "규칙이 네 번 바뀌었습니다" | **"다음 규칙은 아직 이름이 없습니다"** — 진행선이 하네스에서 멈추므로 실제로 지나온 변화는 두 번. 숫자를 빼고 비어 있는 마지막 노드를 가리키게 바꿈 |
| "모델은 3개월짜리입니다" | "모델은 3개월, **가장 밝은 별도 저뭅니다**" — 타일 벽 대신 **은하 별자리** 메타포 |
| 사이트 전체를 관통하는 펄스 라인 | **채택하지 않음.** 섹션별로 다른 다이어그램을 씀 |
| S5만 라이트로 반전 | 라이트 모드에서 **SOLUTION 05 · TEAM 두 장을 다크 밴드**로 (반대 방향) |
| Pretendard | **Noto Sans KR** |
| 서브 페이지 4개 | **단일 페이지.** Projects는 `s4` 아카이브로, Platform은 SOLUTION 01–05로 흡수 |
| 모델 보드 JSON 월 1회 갱신 | JSON 없이 HTML 하드코딩. **갱신 루틴 미구축** |

**v2에서 그대로 살아남은 것**: "세상은 이렇다 → 투비는 이렇게 준비했다" 2단 구조(s1c2 하단),
위키 기반 OKF 다이어그램, 코드→스펙 역전, 로봇·뇌·회로기판 금지.

---

## 8. 열린 항목

1. **SEO 메타 전무** — `description`·OG/Twitter 카드·favicon·canonical 없음. 링크 공유 시 썸네일도 설명도 안 나온다. 비용 대비 효과가 가장 크다.
2. **고정 헤더(83px)가 섹션 상단을 덮는다** — 뷰포트보다 긴 섹션으로 앵커 이동 시. `.scroller`에 `scroll-padding-top:88px`.
3. **개인정보 수집 동의 절차 없음** — 문의 폼이 이름·연락처·이메일을 받는데 동의 체크박스와 처리방침 링크가 없다.
4. **인라인 base64 92KB** — 지도 JPEG를 별도 파일 + `loading="lazy"`로 빼면 초기 HTML이 크게 준다.
5. **SVG 인터랙션 키보드 접근 불가** — 타임라인 노드·은하 별자리에 `tabindex`/`role`/Enter 핸들러 없음.
6. **OKF 슬롯 `setInterval`** — 화면 밖에서도, `prefers-reduced-motion`과 무관하게 계속 돈다.
7. **TEAM 소제목이 규칙에서 벗어남** — "다섯 그룹이 하나의 흐름으로 움직입니다"는 문장형.
8. `100vh` → `100dvh` (모바일 툴바 대응).

---

## 9. 배포

GitHub Pages. `main`에 푸시하면 자동 빌드된다(30초~2분).

```
저장소   kimchul123/tobis
브랜치   main
URL      https://kimchul123.github.io/tobis/
```

로컬 작업 폴더는 git 저장소가 아니다. 수정 시 저장소를 클론해 파일을 덮고 커밋·푸시한다.

---

*Last updated 2026.09.09 · index.html 기준*

---

## 사명 변경 — TOBE AX (2026-09-10 확정)

| 항목 | 값 |
|---|---|
| 국문 | 투비AX |
| 영문 | TOBE AX |
| 법인 등기명 | (주)투비AX (구 (주)투비아이에스컨설팅) |
| 도메인 | tobeax.io — **구입 예정, 아직 미확보** |
| 로고 | **별도 제작 예정** — 현재 base64 로고는 구 TOBIS 마크 |

기존 TOBIS는 *TO Be Intelligent Systems*의 약자였으므로,
TOBE AX는 어근 "TO BE"를 그대로 승계한다. 새 로고 브리프에 사용 가능.

### 적용 완료
- 전 파일 `TOBIS` → `TOBE AX` (문구·타이틀·카피라이트·로고 alt)
- 챗봇 명칭 전 파일 `Cover 어시스턴트`로 통일
  — `TOBE AI` / `TOBE AX`가 한 글자 차이라 충돌하기 때문
- RAG 연결 지점 `window.TobisChat` → `window.TobeChat`
- 테마 저장 키 `tobis-theme` → `tobeax-theme`
- 구 사명은 푸터·챗봇 회사소개의 `(구 …)` 병기로만 잔존

### 미적용 (대기)
- **이메일**: `@2bis-consulting.com` 28곳 유지.
  tobeax.io 미구입 상태라 지금 바꾸면 열리지 않는 주소가 노출됨.
  도메인 확보 즉시 일괄 교체.
- **로고 이미지**: 신규 CI 제작물 수령 후 교체 (1안 2개 · 2안 1개).
