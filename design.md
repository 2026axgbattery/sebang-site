---
# gstack: design-md-format=spec
name: 도면·BOM 통합 탐색기 · 사이트 스타일
description: The SEBANG product-site look applied to a lookup tool. Orange notice strip, dark photo hero with one big search, bold square type, and a green chain that ties a drawing to its molds, parts and products.
colors:
  bg: "#FFFFFF"
  card: "#FFFFFF"
  surface: "#F6F6F5"
  ink: "#14191D"
  ink2: "#1C2328"
  ink3: "#242C32"
  ink4: "#2B363D"
  text: "#333F48"
  text2: "#5f6567"
  dg: "#333F48"
  line: "#D0D0CE"
  line2: "#ECECEB"
  g500: "#A2AAAD"
  g700: "#717779"
  orange: "#EB3300"
  orange6: "#C82B00"
  orange7: "#A42400"
  orange-tint: "#FDEFEB"
  orange-tint-line: "#F7AD99"
  green: "#0097A9"
  green4: "#33ACBA"
  green7: "#006A76"
  link: "#006A76"
  on-dark-muted: "#AAB4BA"
  on-dark-body: "#CFD6DA"
  on-dark-sub: "#B7C0C5"
  highlight: "#FDE6D6"
typography:
  hero:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: clamp(32px, 4vw, 52px)
    lineHeight: 1.1
    letterSpacing: -0.01em
  section:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: clamp(30px, 3.4vw, 44px)
    lineHeight: 1.12
    letterSpacing: -0.01em
  detail-code:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: clamp(32px, 3.6vw, 44px)
    lineHeight: 1.1
  list-title:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: clamp(28px, 3vw, 38px)
  sub:
    fontFamily: SebangGothic
    fontWeight: 400
    fontSize: 17px
  body:
    fontFamily: SebangGothic
    fontWeight: 400
    fontSize: 15px
    lineHeight: 1.55
  table:
    fontFamily: SebangGothic
    fontWeight: 400
    fontSize: 14px
  eyebrow:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: 12px
    letterSpacing: 0.16em
  button:
    fontFamily: SebangGothic
    fontWeight: 700
    fontSize: 14px
    letterSpacing: 0.1em
  label:
    fontFamily: SebangGothic
    fontWeight: 400
    fontSize: 13px
rounded:
  sm: 2px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  2xl: 32px
  3xl: 48px
  section: 80px
  section-tight: 52px
components:
  notice:
    backgroundColor: "{colors.orange}"
    textColor: "{colors.bg}"
  header:
    backgroundColor: "{colors.bg}"
    height: 72px
  header-search:
    borderColor: "{colors.line}"
    rounded: "{rounded.full}"
  header-search-button:
    backgroundColor: "{colors.ink2}"
    textColor: "{colors.bg}"
    rounded: "{rounded.full}"
  button-primary:
    backgroundColor: "{colors.orange}"
    textColor: "{colors.bg}"
    rounded: "{rounded.sm}"
  button-primary-hover:
    backgroundColor: "{colors.orange6}"
  button-dark:
    backgroundColor: "{colors.ink2}"
    textColor: "{colors.bg}"
    rounded: "{rounded.sm}"
  button-outline:
    backgroundColor: "{colors.bg}"
    textColor: "{colors.ink}"
    borderColor: "{colors.ink}"
    rounded: "{rounded.sm}"
  chip:
    borderColor: "{colors.line}"
    textColor: "{colors.ink}"
    rounded: "{rounded.full}"
  chip-key:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.bg}"
    rounded: "{rounded.full}"
  chip-warn:
    backgroundColor: "{colors.orange-tint}"
    borderColor: "{colors.orange-tint-line}"
    textColor: "{colors.orange7}"
    rounded: "{rounded.full}"
  tab-selected:
    textColor: "{colors.ink}"
    borderColor: "{colors.orange}"
  spec-tile:
    backgroundColor: "{colors.surface}"
  chain-node:
    backgroundColor: "{colors.surface}"
  chain-node-current:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.bg}"
  chain-line:
    borderColor: "{colors.green}"
  table-header:
    textColor: "{colors.text2}"
    borderColor: "{colors.ink}"
  table-row:
    borderColor: "{colors.line2}"
  band-dark:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.bg}"
  footer:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.on-dark-muted}"
---

# 도면·BOM 통합 탐색기 · 사이트 스타일

## Overview

**Creative North Star:** /dwg/ looks like the SEBANG product site (`http://10.10.162.168:8080/site/`), so the company's internal apps read as one family. The site's language (orange strip, logo header, dark photo hero, bold square type, pill chips, gray tiles, dark bands) carries a lookup tool whose job is "번호 하나로 다 이어진다": one number connects drawing, mold, part and product.

**Product context:** Internal, read-only lookup tool at Sebang Global Battery. Mold, design and quality staff type any identifier (drawing SEA-02-0022K, mold CCC00020, part MCC02189, product PCF05000K, model 12M24) and see the chain drawing → mold → part → product, revision history, BOM and product assembly drawings. 626 drawings, 359 molds, 1,701 parts, 9,436 products, 32,604 BOM rows, 95 product drawings.

**Mode per surface:** Home is a search surface in a Persuade-style frame (hero). Lists and details are Operate. The help page is Read.

**Source of the look:** `serve/site/index.html`, built by `pipeline/build_site_server.py`. Token names and values in this file are copied from that page's `:root`, so a change to one app can be mirrored in the other by name.

**Reference implementation:** the approved preview `.gstack/design-audit/preview2_tpl.html` (built by `.gstack/design-audit/build_preview2.py`).

**Key characteristics:**
- An orange notice strip on top carries the data dates.
- The home page opens on a dark factory-photo hero with one big white search field and an orange 찾기 button.
- Detail pages lead with a huge bold code, a row of pill chips, one orange primary button, and tabs with an orange underline.
- The chain (four gray tiles joined by green arrows, the current one dark) sits under the tabs on every detail page.
- Square corners (2px) everywhere except pills.

**History:** replaces the 2026-09-25 morning direction "도면대장" (paper, hairlines, orange as text only). That version is kept as `DESIGN.도면대장.bak.md`.

## Colors

**Strategy:** Full palette from the SEBANG CI, used the way /site/ uses it. Neutrals carry text and structure; Orange is the call to action; Green is links and the chain.

**Light or dark:** Light app with dark bands. The office scene (fluorescent light, desktop monitors) favors a white work area. Dark appears as bands the site already uses: the home hero, the stats band, the footer, and the current chain node. There is no full dark theme.

**Token jobs:**
- `bg` is the page and cards. `surface` is gray sections, spec tiles and chain nodes.
- `ink` is headings, codes and dark bands. `ink2` is the dark buttons and the header search button. `text` is body copy, `text2` is secondary copy and table headers. `g700` is the logo label. `g500` is never text.
- `line` is inputs, chips and filter panels; `line2` is row separators and the header bottom rule.
- `orange` is the notice strip, the one primary button per screen, the hero 찾기 button, the selected tab underline and nav hover. `orange6` is its hover. `orange7` is warning text (확인필요, 폐기, stale counts), and `orange-tint` with `orange-tint-line` is the warning chip.
- `green7` / `link` is every link and positive counts in cards. `green` is the chain line and spec-tile bars.
- On dark: `on-dark-muted` for eyebrows and small text, `on-dark-body` for hero paragraphs, `on-dark-sub` for section subtitles.

**CI rule check:** the CI says the two point colors are never co-primary. Here Orange is the only action color; Green only draws lines and links, never a button or a filled area. Point colors stay a small share of any screen.

## Typography

**One face: Sebang Gothic 2.0** (Light 300, Regular 400, Bold 700), CSS family name `SebangGothic` exactly as /site/ declares it. The user chose it explicitly. Files: `C:\Users\sebang\Downloads\SEBANG_GOTHIC_2.0_Fonts\WebFont\세방고딕 2.0_Light/Regular/Bold.woff2`, embedded as data URIs (offline intranet, no network fetch).

**Checked in the font files (2026-09-25, outlines, not just the character map):**
- Hyphen `-` draws, so codes like SEA-02-0022K are fine.
- **En dash `–` and em dash `—` are empty glyphs** (in the map, advance 908, no outline). They render as blank gaps. Never use them in UI text; use ` · `, `:` or `→`.
- `‹ ›` are missing; use `← →`.
- All ten digits share one width, so numbers align in columns. Keep `font-variant-numeric: tabular-nums`.
- Korean line breaking needs `word-break: keep-all` on the body, or headings split mid-word ("도 / 면부터").

**Scale (matches /site/):**

| Role | Size | Weight |
|---|---|---|
| Home hero headline | clamp(32px, 4vw, 52px), line-height 1.1 | Bold |
| Section heading | clamp(30px, 3.4vw, 44px) | Bold |
| Detail code (h1) | clamp(32px, 3.6vw, 44px) | Bold |
| List page title | clamp(28px, 3vw, 38px) | Bold |
| Subtitle under headings | 17px | Regular |
| Body | 15px, line-height 1.55 | Regular |
| Tables, chips, nav | 14 to 14.5px | Regular (nav and row-key codes Bold) |
| Labels, meta | 12.5 to 13px | Regular |
| Eyebrow | 12px, tracking .16em, uppercase | Bold |
| Buttons | 14px, tracking .1em, uppercase | Bold |

## Layout

- **Container:** `.wrap` max-width 1280px, side padding 32px (16px under 760px), as /site/.
- **Notice strip:** full width, orange, 14px, centered. Content for /dwg/: 금형통합DB date (with "N일 전"), BOM LIST version, 제품도 count, and a "빨리 찾는 법" link.
- **Header:** sticky, 72px, white, `line2` bottom rule. SEBANG logo (`serve/site/brand/sebang.svg`) with an 11px uppercase `g700` label "도면·BOM" after a divider; bold 14px nav (체인 탐색, 도면, 금형, 부품, 제품, 제품도 구성, 데이터 이슈, 사용법) with an orange underline on the current section; a pill search with a dark 찾기 button. Under 1100px the nav collapses behind a "메뉴" button that opens a full-width column; under 760px the header search hides.
- **Home:**
  1. Hero: `ink` ground with the plant photo (`serve/site/photo/plant_aerial.webp`) under the site's 90° gradient. Left: eyebrow, headline "번호 하나로 도면부터 제품까지", one paragraph. Right: label, big white input (18px) joined to an orange 찾기 button (58px), example links. Bottom: a row of seven translucent shortcut tiles (체인 탐색, 도면, 금형, 부품, 제품, 제품도 구성, 데이터 이슈) with counts.
  2. "할 일, 바로 보기": the site's question-card grid (4 columns) of data issues, each with a bold title, a big count (`orange7` when it needs action, `green7` otherwise) and one line of context.
  3. "최근 조회" on a `surface` band.
  4. A dark stats band "한 곳에 모은 연결" (626 / 359 / 1,701 / 9,436 / 95).
  5. Dark footer with four link columns and the white logo.
- **Detail:** breadcrumb (links underlined), h1 code, chip row (the first chip dark with the name; a warning chip when needed), action row (one orange primary, outline secondaries, text links on the right), tabs, then the chain, then a 1.2 : 1 split: drawing on a white well on the left (dark label tag top right), spec tiles + key/value table + revision list on the right, then related tables.
- **Lists:** breadcrumb, list title, subtitle, then a 250px filter panel (pill filters with counts, "모두 지우기") beside the results: a results heading with the count, a search field, a 표 / 도면 그림 segmented switch, a sort select, 내보내기, and the dense table.
- **Rhythm:** sections 80px top and bottom (52px for tight ones). Section heading, then subtitle 36px above content. Tables are dense inside generous sections.
- **Mobile:** single column; the chain turns vertical; tables scroll sideways inside their block; the page itself never scrolls sideways (grid columns use `minmax(0, 1fr)`).

## The chain

- Four nodes in order: 도면 → 금형 → 부품 → 제품. Each node is a `surface` tile with a 13px kind label (with a count, "금형 2"), the code in 22px Bold, and a 13px line of context. Nodes other than the current one are links (hover darkens the tile).
- The current node is `ink` with white text, the same move as the site's dark key chip.
- Between nodes: a 2px `green` arrow. The label above it names the match: `exact` (solid line), `normalized` (dashed), `BOM`. The text label is always there, so the grade never depends on line style alone.
- Warnings sit inside the node in `orange7` Bold, for example "입고 2001 · 개정 2018 → 반영 확인" when the drawing was revised after the mold arrived.
- A one-line legend under the chain explains the line styles.
- Motion: on opening a detail page the arrows draw out 120ms apart (220ms each); off under `prefers-reduced-motion`.

## Elevation & Depth

Flat, like the site. Depth comes from bands (white / gray / dark) and fills, not shadows. The only shadow is the site's `shadow2` on floating suggestion lists. There is no floating button over content: the site's bottom-left "빠른 찾기" pill is deliberately not used here, because /dwg/ is table-heavy and the old floating search covered numbers. The header search and the `/` key do the same job.

## Shapes

2px radius on buttons, inputs and tiles; 999px on chips, pill filters and the header search; nothing in between.

## Components

- **Buttons:** 14px Bold uppercase, tracking .1em, 14px × 24px padding (small: 9px × 14px, 13px). Orange primary, one per screen; dark; outline (1.5px `ink` inset); white-outline on dark bands. Hover per token. Disabled: 45% opacity, `not-allowed`.
- **Chips:** 999px, 1px `line`, 14.5px. Key chip `ink` fill; warning chip orange tint.
- **Tabs:** 16px, `text2`; selected is Bold `ink` with a 3px `orange` underline over the `line2` rule; counts inline ("쓰이는 제품 52").
- **Spec tiles:** `surface`, 13px label, 30px Bold number with a 13px unit, a 4px bar with a `green` fill.
- **Question cards (할 일):** white, 1px `line2`, hover border `ink`; 16px Bold title, 22px count, 13px context.
- **Tables:** header 13px Bold `text2` over a 2px `ink` rule, sticky under the header; rows 14px with `line2` separators; row-key code Bold `ink`; hover `surface`; numbers right-aligned.
- **Filter panel:** 1px `line2` box; heading row over a 2px `ink` rule; groups separated by `line2`; pill filters, selected pill `ink`.
- **Inputs:** 1px `line`, square; focus 2px `link` outline. The hero input focuses with a 2px `orange` inset outline, as on the site.
- **Focus:** `:focus-visible` 2px `link` outline, 2px offset, on everything interactive.
- **Empty states:** one sentence with what to type next and examples.

## Do's and Don'ts

- Do copy token names and values from `serve/site/index.html` when a new token is needed, so both apps stay in step.
- Do keep one orange primary button per screen, and keep Green to links, lines and bars.
- Do put `word-break: keep-all` on Korean text.
- Do check any new symbol against the font's outlines before using it.
- Don't use `–` `—` (empty glyphs) or `‹ ›` (missing).
- Don't add a second typeface.
- Don't float buttons or search boxes over tables.
- Don't use Green for buttons or filled areas, or Gray `g500` for text.
- Don't put changelog notices in the product; the orange strip is for data dates and the help link only.

## Motion

- **Approach:** minimal-functional, like the site.
- **Easing:** `cubic-bezier(.4,0,.2,1)`.
- **Duration:** hovers 150ms; chain arrows 220ms, staggered 120ms.
- **The one authored moment:** the chain drawing out when a detail page opens.

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-09-25 | First direction "도면대장" (paper, hairlines, orange as text only, home = search, chain as the spine) | /design-consultation after a /design-review baseline of C+ design / C AI-slop; user wanted a full redesign. Kept as `DESIGN.도면대장.bak.md`. |
| 2026-09-25 | Sebang Gothic 2.0 for every role | User asked for the SEBANG Gothic 2.0 WebFont. En/em dash glyphs found empty; ‹ › missing. |
| 2026-09-25 | **Direction changed to the /site/ look** | User: "http://10.10.162.168:8080/site/#/ 이런 디자인처럼 하고 싶은데". Tokens copied from `serve/site/index.html`. Kept from the first direction: the chain on every detail page, home = search (now inside the hero), data-issue cards, dense tables. |
| 2026-09-25 | Orange primary buttons back in | Matches the site and the SEBANG CI's own button rule. |
| 2026-09-25 | Site's floating "빠른 찾기" pill not used | Floating controls covered table numbers in the old /dwg/; header search plus `/` covers the job. |
| 2026-09-29 | Wide screens: container 1760px from 1600px wide, 2320 from 2400, 3160 from 2900; above 3800px CSS width the page zooms by width/2560 | User: "FHD 화면에 최적화", "5120*2160 해상도에서 최적화". Section padding 56/34 on wide screens; vw/vh go through --vw1/--vh1 so zoom does not double them. |
| 2026-09-29 | Battery System inner screens follow these tokens (patch_bs_theme.py) | User: "BS 안쪽 화면도 사이트 디자인으로". Teal fills → ink2, tints → surface, 2px corners, no shadows, no emoji in controls; bars keep green. |
