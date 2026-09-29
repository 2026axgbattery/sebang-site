# TECH · 구조

## 서버

- `pipeline/serve.py` — 파이썬 정적 서버(포트 8080) + gzip + 사용 기록 API(`/site/api/log`) + 선택 Basic 인증. 서버 PC 한 대, 인터넷 불필요.
- 입구 `serve/index.html` · 공통 머리줄 `serve/common/appbar.js`(모든 앱 통합 검색 `find.json`).

## 앱

| 주소 | 소스 | 형태 |
|---|---|---|
| `/site/` | `pipeline/assets/site_tmpl3.html` → `build_site_server.py` | 한 페이지 앱(해시 라우팅 `#/p/코드` …) + `data.json` + 3D 쉘 `shell/*.bin` |
| `/site/#/bs/…` | Battery System (`out/bs_app/Battery_System_v13_0.html`) | 사이트 안 iframe, 사이트 탭 줄이 앱 메뉴를 대신 |
| `/site/#/load/…` | 적재 조회 (`build_load.py`) | 사이트 안 iframe |
| `/site/academy.html` | `pipeline/assets/academy_tmpl.html` | three.js 3D 분해 |
| `/dwg/` | `pipeline/dwg_app` | 도면 · 금형 · 부품 · 제품 체인 |
| `/www/` | `build_site_server.build_public` | 외부 공개판(사내 정보 제거) |

## 빌드 흐름 (`build_all.py`)

```
build_serve → build_site_server (data.json · 영어/일본어 · 공개판) → build_unified(/dwg/ /3dv/)
→ build_load_layouts → load_shells → build_load → build_load_single
→ extract_bs_link.js → build_site_link.py (serve/site/link/*.json) → appbar.py
```

## 사이트 안 주요 장치

- **사내판 전용 코드**는 `/*INT{*/ … /*}INT*/` 구간 — 영어 · 일본어 · 공개판 빌드에서 잘라냄.
- **Battery System 사이트 디자인**: `patch_bs_theme.py` 가 모든 문서(본문 · iframe · 섀도루트)의 CSS 규칙 값을 사이트 토큰으로 다시 씀.
- **연계 자료** `link/`: sales(판매 · 수익) · bsp(BS 전용 제품) · buyer(바이어 표기) · plate(극판 표준화) · load(적재 · 컨테이너 키).
- **컨테이너 담기**: `localStorage 'cntr.v1'` 에 `제품코드|고객|파렛트|변형` 키 + 수량을 써서 적재 조회로 넘김.
- **3D 뷰어**: three.js r128, 극성 거울 · 라벨(앞 · 뒤 · 카바 윗면) · 색 바꾸기 · PNG.
- **넓은 화면**: `html.w16/w24/w30` 단계 + 3800px 이상은 zoom (vh/vw 는 `--vh1/--vw1`).

## 점검

Playwright(headless, RTX 5090 GPU): `test_site_sales.js` · `test_site_buyer.js` · `test_site_one.js` · `test_site_crawl.js`(1,000여 화면) · `audit_bs_theme.js`.
