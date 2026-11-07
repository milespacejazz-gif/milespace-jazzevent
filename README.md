# Handoff: MileSpace · 臺中州廳草地音樂會 活動網站（水彩版）
【百年綠意 · 爵代新聲】MileSpace · Taichung State Hall Grassland Concert 2027

## Overview
This is a one-page event website for a free, outdoor jazz concert series. It runs four afternoons on the inner-court lawn of 臺中州廳 (Taichung State Hall): **2027/1/9, 1/10, 1/16, 1/17**.

- **Organizer:** 臺中市政府文化局
- **Producer (策劃執行):** MileSpace

The site has these jobs:
- Explain the concept
- Present the 9 bands, grouped by day
- Show each day's program
- Highlight **1/17 (Sun) as the extended three-band day, starting at 14:30**
- Promote the 1/16 swing-dance session
- Give venue info
- Introduce MileSpace
- Link to MileSpace's Instagram and Facebook

The site is in Traditional Chinese (`lang="zh-Hant"`), with English and script-font subtitles.

The visual theme is **watercolor**. The palette is sampled from the hero painting "Jazz Live at 台中州廳": deep navy ink, warm amber, and cream paper, with a subtle paper-grain overlay.

## About the Design Files
The files in this bundle are **design references created in HTML**. They are prototypes that show the intended look and behavior, not production code to ship directly.

Recreate the design in the target codebase's environment (React, Next.js, Astro, Vue, etc.) using its established patterns. If no environment exists yet, use a static-site framework (Astro, or Next.js with static export), because the content is static and SEO matters. Keep band and program content in a structured data file or CMS; `data.js` is the source of truth.

`index.html` runs as-is: open it in a browser with `site.css`, `site.js`, `data.js` and `assets/` beside it.

**Note on `site.css`:** it has two layers.
1. Base layout rules (lines 1–~280).
2. A `/* WATERCOLOR THEME LAYER */` block that overrides the base rules.

The final rendered values are described below. When the two layers conflict, the theme layer wins. When reimplementing, merge them into one set of rules.

## Fidelity
**High-fidelity.** Colors, typography, spacing, imagery, copy and interactions are final. Recreate the design faithfully.

---

## Design Tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| `--ink` | `#1E3557` | Navy: primary text, dark sections (lineup, footer, solid nav), info bar |
| `--ink2` | `#16284A` | Deeper navy |
| `--y` | `#E9A93B` | Amber: highlighter underlines, nav underline, accents |
| `--y2` | `#F0B648` | Light amber: chips, selected tab, section-title swash, card borders, logo-card shadow |
| `--cream` | `#FBF5E6` | Page/paper background, cards, light text on dark |
| `--cream2` | `#F3E7CC` | Venue section background |
| `--red` | `#B8503A` | Terracotta (brick): script subtitles, set labels, member roles, pills |
| `--muted` | `#6B6A62` | Secondary text on light |
| `--green` | `#5E7F4A` | Reserved (palm green) |
| `--sky` | `#7FA6CC` | Reserved (sky blue) |
| — | `#34496B` | Hairlines on navy |
| — | `#9FB0C6`, `#B3C1D3`, `#C7D2DF` | Secondary text on navy |
| — | `#F4E3BC` | Swing section background |
| — | `#3D3A33` | Body text in the MileSpace section |

### Typography (Google Fonts)
| Variable | Family | Use |
|---|---|---|
| `--serif` | Noto Serif TC 700/900 | All h1/h2/h3, pull quotes, venue labels |
| `--zh` | Noto Sans TC 400/500/700/900 | Body text and UI |
| `--disp` | Archivo 500–900 | Dates, times, numbers, English labels |
| `--script` | Kaushan Script | Section subtitles, preface numerals, footer "AFTERNOON OF JAZZ" |

- **Body line-height:** 1.85–2.0.
- **Display line-height:** 1.05–1.25.

### Radius & Shadow
- **Radius:**
  - Cards: 3–4px
  - Pills (nav CTA, swing keywords, social links): 999px
  - Badges and the modal close button: 50%
- **Shadows:**
  - Hero title card: `0 14px 40px rgba(30,53,87,.18)`
  - Info bar: `0 12px 30px rgba(30,53,87,.22)`
  - Scene frame: `0 18px 50px rgba(0,0,0,.35)`
  - Band cards: `0 10px 30px rgba(0,0,0,.25)`
  - Swing photo: hard offset `14px 14px 0 #1E3557`
  - MileSpace logo card: hard offset `14px 14px 0 #F0B648`

### Paper Texture
`body::before` is a fixed full-screen layer with these properties:
- Fractal-noise SVG
- `opacity .18`, `mix-blend-mode: multiply`
- `pointer-events: none`, `z-index: 200`

### Layout
- **Container `.wrap`:** max-width 1280px, centered, horizontal padding `clamp(20px,4vw,56px)`.
- **Section padding `section.block`:** `clamp(80px,10vw,140px)` top and bottom.
- **Anchors:** `scroll-behavior: smooth` and `scroll-padding-top: 64px`.

### Section Header Pattern
- **`h2`:** Noto Serif TC 900, `clamp(28px,3.2vw,44px)`, `letter-spacing .06em`, navy.
- **Swash:** behind the bottom of the title is an organic amber brush-stroke made with `::after`:
  - `height .42em`, background `#F0B648` at opacity .75
  - `border-radius: 70% 30% 60% 40% / 60% 70% 30% 40%`, rotated −1.6°
- **Subtitle (`.ssub`):** Kaushan Script, `clamp(18px,1.6vw,22px)`, terracotta.
- **On dark sections:** the title is cream, the swash is at opacity .55, and the subtitle is amber.

---

## Sections (top to bottom)

### 0. Fixed Nav
- **Layout:** fixed, 64px tall, z-index 50.
- **Initial state:** transparent over the hero painting.
- **Solid state:** after `scrollY > 0.6 × viewport height` the background becomes navy and the text cream.
- **Logo:** `wordmark_dark.png` cross-fades to `wordmark_light.png` when solid.
- **Links:**
  - Items: 活動理念 `#about` · 演出陣容 `#lineup` · 搖擺舞體驗 `#swing` · 場地資訊 `#venue` · 關於 MileSpace `#milespace`
  - Style: 14px, weight 500, gap 28px
  - Underline: a 2px amber underline grows from the left on hover and on the active item
  - Below 900px the links are hidden.
- **CTA "查看節目表 →":** pill-shaped, padding `10px 20px`, 700, 13px.
  - Transparent nav: navy background, amber text.
  - Solid nav: amber background, navy text.

### 1. Hero (`#top`)
- **Background:** cream.
- **Painting (`.art`):**
  - `assets/hero_wc.jpg`, `background-size: cover`, `background-position: center 22%`
  - Height `min(100vh, 75vw)`; `75vw` on screens 820px or narrower
  - A 90px gradient at the bottom fades the painting into cream
- **Title card (`.banner`):**
  - Overlaps the bottom of the painting with `margin: -48px clamp(20px,4vw,56px) 0`; `-28px 16px 0` at 820px or narrower
  - Background `rgba(251,245,230,.94)`, padding `26px 30px 24px`, rotated −0.3° (no rotation on mobile)
  - A semi-transparent amber "tape" strip sits at the top center via `::before`: 110×26px, `rgba(240,182,72,.55)`, rotated 2°
  - Load animation: fades up 16px over 1s with a .3s delay
  - **There are no logos in the hero card**; the client removed them.
  - **Line a:** "【百年綠意 · 爵代新聲】" — serif 900, `clamp(28px,3.4vw,50px)`, `margin-left: -.45em` (hangs the bracket).
  - **Line b:** "MileSpace · 臺中州廳草地音樂會" — Noto Sans TC 700, `clamp(17px,1.8vw,26px)`.
  - **English line:** "2027 · TAICHUNG STATE HALL · GRASSLAND CONCERT" — Archivo 700, 10px, `letter-spacing .36em`, terracotta, `margin-top 14px`.
- **Info bar (`.infobar`):**
  - 18px below the card with the same side margins
  - Navy background, 3px radius
  - Grid `auto 1fr auto`; single column at 820px or narrower, with the tag hidden
  - **Tag:** "活動資訊 / INFO" — amber box, navy text, 900, 20px.
  - **DATE cell:**
    - Label "DATE · 2027"
    - Dates "1 / 9 | 1 / 10 | 1 / 16 | 1 / 17" — Archivo 700, `clamp(17px,1.8vw,24px)`, separated by 2px amber rules
    - Each date links to `#lineup` **and selects that day's tab**
    - **1/17** is shown in amber, followed by the terracotta tag "三團 · 14:30 起", which pulses `scale 1 → 1.06` on a 2.4s infinite loop
  - **TIME cell:**
    - Main time: "下午 15:30 ~ 17:30" — Archivo 900, amber, `clamp(20px,2.2vw,30px)`
    - Line: "1/17（日）提早 **14:30** 開演 · 三團接力", with 14:30 on an amber chip
    - Small line: "PRESENTED BY MILESPACE · 草地自由入座"

### 2. Marquee
- **Container:** navy strip, amber Archivo 800 at 15px, `letter-spacing .3em`.
- **Content:** fixed phrases plus the band names, separated by a cream "✦" at 50% opacity.
- **Motion:** the content is duplicated and translated −50% over 40s, linear and infinite.
- **Accessibility:** `aria-hidden`.

### 3. Preface (`#about`)
- **Header:** "前言" / "Preface · About this afternoon".
- **Layout:** grid `1.05fr 1fr`, stacks at 900px or narrower.
- **Left column:**
  - Pull quote "把百年古蹟，/ 變成城市的**客廳**。" — serif 900, `clamp(34px,4.4vw,64px)`.
  - "客廳" gets an amber highlighter: `linear-gradient(transparent 58%, var(--y) 58%)`.
  - Below it, a 15px muted paragraph.
- **Right column:**
  - Ordered list of three paragraphs, 16px, line-height 2.
  - Numerals "01/02/03" are set in Kaushan Script, 22px, terracotta.
  - Key phrases in `<b>` get a highlighter.
- **Copy:** use the text exactly as written in `index.html`.

### 4. Scene Illustration (`#scene`)
- **Background:** split — the top 50% is cream, the bottom is navy (leading into the lineup).
- **Frame:**
  - `aspect-ratio: 4/3`, `width: min(1080px, 100% − gutter, (100vh − 120px) × 4/3)`
  - 10px white border (6px at 700px or narrower), `overflow: hidden`, large soft shadow
- **Image:** `assets/jazz-afternoon.png` — the client's 1024×768 watercolor of the State Hall lawn concert. `object-fit: cover`, base `scale(1.04)`. The whole image must stay visible.
- **Parallax:** `translateY((p − .5) × 3%)` as the frame moves through the viewport; disabled under `prefers-reduced-motion`.
- **Caption card:**
  - Right-aligned, overlapping the frame's bottom border
  - Navy, 3px radius, max-width 560px
  - Quote "紅磚拱廊、棕櫚樹影，/ 一張野餐墊，一個爵士午後。" — serif 900, `clamp(22px,2.4vw,32px)`
  - Tags 內庭草坪 / 自由入座 / 攜帶野餐墊 — 1px `#4A5F80` border, 13px
  - No "示意" label.

### 5. Lineup & Program (`#lineup`, navy section)
- **Header:** "演出陣容 · 節目表" / "Lineup · 9 Bands · 4 Afternoons".
- **Day tabs:**
  - 4 columns (2×2 at 760px or narrower), `#34496B` hairlines
  - Each tab shows:
    - Week/session label: Archivo 11px
    - Big date: Archivo 800, `clamp(36px,4.6vw,68px)`
    - Sub-line: 14px
  - Hover: `#263A5A`. Selected: amber background, navy text.
  - The 1/16 tab has a terracotta pill "搖擺舞體驗限定場".
  - **The 1/17 tab** has an inset 2px amber outline, an amber pill "三團加長場", and a sub-line ending in "**14:30 開演**".
- **1/17 special banner** (shown only when 1/17 is selected):
  - Amber block, grid `auto 1fr auto`
  - Left: a big "3 團"
  - Middle: title "1/17 週日 · 三團接力加長場" and copy
  - Right: the three bands with time chips — 14:30 郭馬克爵士五重奏 · 15:30 盜魂爵士樂團 · 16:40 Somm Jazz
- **Day view:** grid `1fr 360px`, gap 56px, stacks at 1060px or narrower.
- **Band card:**
  - A `<button>`, grid `1.15fr 1fr`, cream, 4px radius, soft shadow
  - Fades up 18px with a .08s stagger per card
  - **Photo side:** 4:3. Hover: scale 1.05 and saturate .9 → 1.1.
  - **Text side:** the following, top to bottom:
    - Amber time chip
    - Terracotta set label
    - "場次 0X / 09"
    - Name — serif 900, `clamp(26px,2.7vw,40px)`
    - English name
    - Lead quote
    - "樂團介紹 ——", where the line grows from 28px to 48px on hover
- **Schedule aside:**
  - Sticky at `top: 88px`, 1px border, 4px radius
  - Header: "{date} · 當日流程" plus the eyebrow "PROGRAM"
  - Rows use grid `104px 1fr`
  - Row variants:
    - `set`: amber background
    - `dance`: terracotta tint
    - `host`: amber title

### 6. Band Detail Drawer (`#modal`)
- **Panel:** right-side sheet, `min(880px,100%)` wide, cream, scrolls internally.
- **Motion:** slides in from +60px over .45s; the backdrop is `rgba(10,10,8,.72)` with `blur(4px)`.
- **Body scroll** is locked while the drawer is open.
- **Contents, top to bottom:**
  1. 16:9 photo
  2. Tag row
  3. Name (serif)
  4. English name
  5. Lead quote with a 4px amber rule
  6. Bio
  7. Two columns:
     - "PERSONNEL · 樂團編制", with roles in terracotta
     - "HIGHLIGHTS · 重要經歷", with amber square bullets
  8. Prev/next buttons that cycle through all 9 bands across days
- **Close button:** round, navy, with an amber ✕.
- **Closing:** the backdrop, the ✕ button, or the Esc key.

### 7. Swing Dance (`#swing`, background `#F4E3BC`)
- **Layout:** grid `1.2fr 1fr`.
- **Photo:** `dance_v2.jpg`, 3:2, 3px radius, hard navy offset shadow.
- **Badge:** circular, 150px (110px on mobile), cream with a 4px navy border, holding `dance2.jpg` (Let's Swing logo) with multiply blend.
- **Time chips:** "1/16 SAT · 16:20 – 16:40" (navy/amber) + "限定場" (terracotta).
- **Heading:** h3 "Let's Swing Taichung / 搖擺舞體驗".
- **Body:** two paragraphs.
- **Keywords:** pills "自由 / 即興 / 互動" with a 2px navy border.

### 8. Venue (`#venue`, background `#F3E7CC`)
- **Header:** "場地資訊" / "Floor plan · Getting there".
- **Map card:** white, 2px navy border, `floorplan.jpg`, caption "臺中州廳平面配置 · 俯視圖 / N ↑".
- **Definition list:** rows use grid `150px 1fr`.
  - **活動區位:** includes a legend — a terracotta dot for 舞台區 and an amber square for 控台.
  - **入場動線**
  - **開放入場:**
    - 1/9 and 1/10: 13:30
    - 1/16: 13:50
    - 1/17: opens 14:25, first band at 14:30
  - **建議攜帶:** navy chips 野餐墊 and 保暖外套.
  - **地點:** 臺中市西區民權路 99 號 (unconfirmed).

### 9. About MileSpace (`#milespace`) — NEW
- **Background:** cream, with a 1px `rgba(30,53,87,.12)` top rule.
- **Header:** "關於 MileSpace" / "Produced by · 企劃執行單位".
- **Layout:** grid `minmax(220px,.8fr) 1.2fr`, gap `clamp(36px,6vw,96px)`, vertically centered. At 820px or narrower it becomes one column and the logo card is capped at 280px wide.
- **Logo card:**
  - Square, white, 3px radius, padding 12%, rotated −1.2°
  - Hard amber offset shadow `14px 14px 0 #F0B648`
  - Contains `logo_dark.png`
- **Copy (exact):**
  - **Lead:** "讓音樂回到城市，<br>也回到**生活**裡。" — serif 900, `clamp(30px,3.8vw,54px)`, line-height 1.25, navy. "生活" gets the same amber highlighter as the preface.
  - **Paragraph 1:** "我們相信爵士不只發生在舞台上，更應融入日常的每一個時刻。"
  - **Paragraph 2:** "從一杯飲品、一段旋律，到老建築裡的相遇——MileSpace 持續以現場音樂、空間策展與城市文化為核心，點亮地方的生命力。"
  - Paragraph style: 16px, line-height 1.95, color `#3D3A33`, max-width 30em, 14px between paragraphs.

### 10. Footer (navy)
- **Padding:** 96px top, 40px bottom.
- **Brand row:** `logo_yellow.png` (height `clamp(120px,16vw,220px)`) next to "AFTERNOON / OF JAZZ" in Kaushan Script, amber, `clamp(44px,8vw,128px)`. Stacks at 700px or narrower.
- **Credits row:** 1px `#34496B` top rule.
  - "主辦單位 · ORGANIZER" + `tccab_light.png` (44px tall)
  - "策劃執行 · PRODUCED BY" + `wordmark_light.png` (26px tall)
- **Bottom row** (1px top rule, **right-aligned**):
  - **Social links block:** eyebrow "FOLLOW MILESPACE" (Archivo 11px, `.14em` tracking, `#8FA0B8`).
  - **Two pill links:**
    - **Instagram** `@milespace_jazz` → https://www.instagram.com/milespace_jazz/
    - **Facebook** `MileSpace` → https://www.facebook.com/profile.php?id=100095551352360
  - Both open with `target="_blank" rel="noopener"`.
  - Pill style: padding `10px 18px`, 1px `rgba(240,182,72,.6)` border, Archivo 700 15px in cream, handle in Noto Sans TC 13px amber, trailing "↗".
  - Hover: amber fill and navy text, `.2s` transition.
- **Removed per client:** the event title/date summary lines and the "PRESENTED BY MILESPACE" line are no longer in the footer.

---

## Interactions & Behavior
| Interaction | Behavior |
|---|---|
| Nav scroll state | Solid after 60% of viewport height; the logo swaps |
| Nav active link | Last section whose top is above 120px |
| Hero date click | Selects that day and smooth-scrolls to `#lineup` |
| Day tab click | Re-renders the cards and schedule, toggles the 1/17 banner, saves to `localStorage['milespace_day']` |
| Band card click | Opens the drawer |
| Drawer | Prev/next through all 9 bands; close with backdrop, ✕ or Esc |
| Scene parallax | ±1.5%; off under reduced motion |
| Scroll reveal | `.reveal`: opacity 0 + translateY 24px → visible over .9s, `cubic-bezier(.2,.7,.2,1)`; IntersectionObserver threshold .12; fires once |
| Social links | Open in a new tab |

**Easing used throughout:** `cubic-bezier(.2,.7,.2,1)`.

**Breakpoints:** 1060, 900, 820, 760, 700, 640, 600, 520px.

**Accessibility:**
- Tabs use `role="tablist"` / `role="tab"` / `aria-selected`.
- The drawer uses `role="dialog"` and `aria-modal`.
- Add focus trapping and focus return to the drawer when you reimplement it; the prototype has neither.

## State Management
- `selectedDay`: `'0109' | '0110' | '0116' | '0117'`. Default `'0109'`, persisted in localStorage.
- `openBandNo`: `string | null`, controls the drawer.
- `navSolid` and `activeSection`: derived from scroll position.
- No data fetching; all content is static in `data.js`.

## Data Model (`data.js`)
- **`days[]`:** `{ id, date, dow, zh, week, session, tag?, special?, start? }`. 1/17 has `special: true, start: '14:30'`.
- **`bands[]` (9 items):** `{ no, day, set, time, name, en, sub, img, pos, lead, bio[], members[[role,name]] | sections[[section,names]], highlights[] }`.
- **`program[dayId]`:** rows `[time, title, detail, variant?]`. 1/10 reuses the 1/9 program, and each list starts at the first band.
- **Day to band mapping:**
  - 1/9: 果子好聲音, Longfingers Quintet
  - 1/10: Old School Funk Unit, Kuljiyan 谷莉姎
  - 1/16: 爵序大樂團, JazzShip Swing (+ swing dance)
  - 1/17: 郭馬克爵士五重奏 14:30, 盜魂爵士樂團 15:30, Somm Jazz 16:40

## Assets (`assets/`)
| File | Content | Notes |
|---|---|---|
| `hero_wc.jpg` | Hero watercolor "Jazz Live at 台中州廳" | Positioned `center 22%` |
| `jazz-afternoon.png` | Scene watercolor (1024×768) supplied by the client | ~2 MB PNG; convert to WebP/JPG for production |
| `b01–b08.jpg`, `b09b.jpg` | Band photos | From the client's proposal PDF |
| `dance_v2.jpg` | Swing dancers photo | |
| `dance2.jpg` | Let's Swing Taichung logo | Multiply blend |
| `floorplan.jpg` | Venue floor plan | |
| `logo_dark.png` / `logo_yellow.png` | MileSpace full logo | MileSpace section / footer |
| `wordmark_dark.png` / `wordmark_light.png` | MileSpace wordmark | Nav / footer |
| `tccab_light.png` | 臺中市政府文化局 logo | Footer (`tccab_dark.png` is now unused) |
| `cover.jpg` | Old yellow-and-black hero | Unused; referenced only by base CSS that the theme overrides |
| `source/` | Original logo files | Ask the client for vector logos before launch |

**Before launch:**
- Get vector logos.
- Confirm image rights.
- Add OG/share images.
- Compress the two large watercolor images.

## Open Items (confirm with client)
1. Venue address 民權路 99 號 is unconfirmed.
2. Whether "策劃執行" should become "承辦單位" or "執行單位".
3. Whether co-organizer or sponsor logos are needed.
4. The 14:25 seating advice for 1/17.
5. The 文化局 logo now appears only in the footer, after it was removed from the hero.

## Files
- `index.html`: structure and all static copy
- `site.css`: styles (tokens in `:root`, with the watercolor theme layer at the end)
- `site.js`: marquee, nav, day tabs, band cards, drawer, parallax, scroll reveal
- `data.js`: days, bands, program
- `assets/`: images and logos
