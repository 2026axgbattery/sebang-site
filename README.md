# sebang-site · 세방 배터리 영업 지원 시스템

세방전지 사내 업무용 웹 사이트입니다. 제품 찾기 · 사양 비교 · 제품 3D · 견적에 더해, Battery System(설계 · 판매 · RFQ 1·2·3안 매칭)과 배터리 적재 조회(파렛트 · 컨테이너)를 한 사이트에서 씁니다.
영업 · 생산 · 기획 · 제품개발 누구나, 흩어져 있던 BOM · 성능 · 판매 · 도면 · 적재 자료를 한 곳에서 찾도록 만들었습니다.

> **사내망 전용.** 아래 주소는 회사 네트워크 안에서만 열립니다.
> 이 저장소에는 **문서만** 있습니다. 제품 · 판매 · 고객 · 도면 데이터와 빌드 결과(`serve/`, `out/`)는 넣지 않습니다.

## 사이트 주소

| 화면 | 주소 |
|---|---|
| 영업 지원 사이트 (첫 화면) | http://10.10.162.168:8080/site/ |
| 배터리 찾기 | http://10.10.162.168:8080/site/#/find |
| Battery System (업무 도구) | http://10.10.162.168:8080/site/#/bs |
| 적재 조회 · 컨테이너 시뮬레이션 | http://10.10.162.168:8080/site/#/load |
| 3D 아카데미 (분해 · 구조) | http://10.10.162.168:8080/site/academy.html |
| 도면 · BOM 통합 탐색기 | http://10.10.162.168:8080/dwg/ |
| 사내 도구 모음 (입구) | http://10.10.162.168:8080/ |

---

## 1. 처음 설정 (Windows 기준, 1회)

1. **Python 3.13** (miniconda) · **Node.js** 설치. 파이썬 패키지: `openpyxl`, `Pillow`, `fontTools`, `edge-tts`(영상용).
2. **Playwright**(화면 점검 · 자료 추출용): `npx playwright install chromium` 후 `NODE_PATH` 를 그 `node_modules` 로.
3. **ffmpeg**(영상 합성용, 선택): `winget install Gyan.FFmpeg`
4. 원본 자료 위치(사내 PC): BOM LIST · 금형통합DB · Battery System HTML · VC 정보 마스터 · 적재 기준표 — `pipeline/sources.json` 에 경로.
5. 서버 PC 에서 `서버시작.bat` (로그아웃해도 유지하려면 `서버_로그아웃에도유지.bat`). 포트 **8080**.

## 2. 실행

| 하려는 것 | 명령 |
|---|---|
| 전체 다시 만들기 (사이트 · 도면 · 3D · 적재 · 연계 자료 · 머리줄) | `python pipeline\build_all.py` |
| 사이트 화면만 다시 (데이터 그대로, 템플릿만 고쳤을 때) | `python pipeline\build_site_pages.py` |
| 사이트 데이터까지 (성능 · BOM · 거래처) | `python pipeline\build_site_server.py` |
| BS · 적재 → 사이트 연계 자료 | `node pipeline\extract_bs_link.js` → `python pipeline\build_site_link.py` |
| Battery System 앱 (브랜드 · 바이어 · 수정 · 글꼴 · 사이트 디자인) | `python pipeline\make_bs_app.py` → `build_serve.build_bs()` → `python pipeline\appbar.py` |
| 적재 조회 | `python pipeline\build_load.py` |
| 서버 시작 / 중지 | `서버시작.bat` / `서버중지.bat` |
| 점검 (오류 · 화면 넘침) | `node pipeline\test_site_sales.js` · `test_site_one.js` · `audit_bs_theme.js` |

## 3. 폴더 구조

```
C:\Drawing
├─ pipeline\              빌드 · 추출 · 점검 스크립트 (Python · Node · PowerShell)
│  ├─ assets\             사이트 템플릿(site_tmpl3.html) · 3D 아카데미 · 번역표(i18n_en/ja) · 영상 장면
│  ├─ common\             모든 앱 공통 머리줄(appbar.js)
│  ├─ dwg_app\            도면 · BOM 탐색기 소스
│  └─ serve.py            사내 서버 (정적 파일 + 사용 기록 API, gzip)
├─ serve\                 서버가 내보내는 결과 (build_all 이 새로 만듦 — 저장소에 넣지 않음)
│  ├─ site\  bs\  load\  dwg\  3dv\  common\  www\(외부 공개판)
├─ out\                   중간 결과 · 엑셀 보고서 · 영상 (저장소에 넣지 않음)
├─ 입력\                  사람이 채우는 엑셀 (국가 확인 · 경쟁사 교차표 · 차량 적용표)
├─ DXF\ · 3D\ · 제품도\   도면 · CAD 원본 (저장소에 넣지 않음)
├─ DESIGN.md              디자인 기준 (이 저장소의 design.md)
└─ CLAUDE.md              작업 규칙
```

## 4. 자료 기준

| 자료 | 출처 | 쓰는 곳 |
|---|---|---|
| 제품 6,292종 · 사양 · 5레벨 제품군 | BOM LIST 260901 (분류 시트) | 사이트 전체 |
| 성능 C20 · RC · CCA · 중량 · 납 중량 | Battery System 성능 DB (`window.P`, 11,898행) | 제품 페이지 수치 |
| 판매 · 수익 (25년 · 26상반) | Battery System 판매실적 | 제품 페이지 「판매 · 적재 · 극판」 (사내판만) |
| 거래처 · 팀 · 국가 | 영업 세계지도 + Battery System | 고객 · 브랜드, 거래처 페이지 |
| 바이어 표기 검토 | VC 정보 마스터 × 제품마스터 | 거래처 페이지 |
| 도면 · 금형 | 금형통합DB · DXF 590장 | 도면 · BOM 탐색기, 제품 페이지 |
| 파렛트 · 컨테이너 적재 | 적재 조회 최종 DB (VC × PALLET LIST × 적재 기준표) | 적재 조회, 견적 → 컨테이너 |
| 3D | 세방 CAD(STEP) · 2D 도면으로 만든 쉘 · COS 도면 | 제품 3D · 3D 아카데미 |

- 성능 값이 빈 제품은 **같은 설계**(제품군 · (+)(−) 극판 코드 · 매수)의 실측 최빈값으로 채우고 `≒` 표시.
- 극성: L = A · D = (−) 좌, R = B · E = (+) 좌.

## 5. 데이터 갱신

- **매일 02:30 자동**: `pipeline/auto_refresh.py` 가 원본 파일이 바뀌었는지 보고, 바뀐 것만 다시 만들어 서버에 반영 (예약: `schedule_auto_refresh.ps1`).
- 손으로: `pipeline\update_site.ps1 [-Bom] [-Perf] [-Map] [-Labels]` — 임시 폴더에서 만들고 점검 통과하면 운영에 바꿔 넣음.
- 사람이 고치는 값은 `입력\*.xlsx` 에 적고 빌드하면 반영.

## 6. 개발 로드맵 (제안)

- Battery System 연계 남은 것: 통합 매칭 결과 → 견적 목록 · 담은 제품 공유 · 라인업 사다리 · 데이터 한 줄기 · 로그인 · 권한 통일
- 판매 금액 · 이익률을 권한별로 보이기
- 소개 영상(2분) — 각본 · 녹화 스크립트 준비됨 (`pipeline/promo_*`)
- 3D: MF 일체형 카바 · EN 카바 종류별 쉘 보강

## 7. 알아둘 점

- **사내 정보가 들어 있는 사이트입니다.** 외부에 줄 때는 `serve/www`(외부 공개판: 도면 · 금형 · 판매 · 고객명 · 극판 품번 뺀 것)만.
- 세방고딕 2.0 에는 `—` `–` 글자가 비어 있음 → 화면 글에 쓰지 말 것 (`·` `:` `→`).
- `build_serve.py` 는 `serve/` 를 통째로 지우고 다시 만듦 → 그 뒤 `build_all.py` 의 나머지 단계가 꼭 따라와야 함.
- 파일 복사에 하드링크 금지 (같은 파일을 덮어써 다른 쪽도 바뀜).
- 디자인은 `design.md`(= DESIGN.md) 기준: 모서리 2px · 주황은 주요 단추 하나 · 초록은 선 · 링크 · 막대만.

---
세방전지 광주 기술혁신팀 · 제품개발
