# TOBIS 홈페이지 시안 (2026-10)

제품소개서(CoverLink_제품소개서_v20261019)를 바탕으로 만든 새 홈페이지 디자인 시안.
방향: "투비가 무엇을 했고, 무엇을 가지고 있고, 무엇을 할 것인가" 중심으로 단순하게. 기존 메뉴 구조는 쓰지 않음.

- 디자인 캔버스(원본, 비공개): https://claude.ai/artifact/5B1zcStVrZrih8o62M5aQK
- **A안 (진행 중)** — `Main.dc.html` (PC) / `A_Mobile.dc.html` (모바일)
  - 첫 화면: 열쇠구멍 + 신경망 애니메이션, 문구 "보험을 아는 AI, 투비가 만듭니다"
  - 두 번째 화면: 회사 소개 → 해온 일 / 가진 것(네이비) / 할 일 / 문의
- B안 (보류) — `B_Home.dc.html` / `B_Mobile.dc.html`

## 파일 안내

- `*.dc.html`, `canvas.json` — 디자인 캔버스용 원본 파일. 브라우저에서 바로 열리는 웹페이지가 아니다
  (캔버스 런타임과 업로드 자산 `/_blob/...` 을 참조함).
- `clients/` — 고객사 로고 15개 (2bis-consulting.com 고객사 영역에서 가져옴).
- TOBIS 로고 원본은 `assets/logo/tobis/` 에 있다.

시안이 확정되면 이 파일들을 기준으로 실제 홈페이지 HTML 을 만든다.
