# Handoff: GM Creative Production Pipeline (Interactive Workflow Board)

## Overview
An interactive, single-screen "operations canvas" that visualizes GM's creative
production pipeline for marketing campaigns. The flow starts at **GM → Client Brief**,
then everything is orchestrated inside a **Smartsheet** container that holds **three
parallel swim lanes** (columns) and **three phase rows**. The board is designed as a
pitch artifact (used to win the business), so it favors a bold, cinematic, neon-on-dark
"mission control" look with two key interactions: **hover a step to zoom it**, and a
**Run flow** button that animates the sequence.

- **Three lanes (columns):** `T1` (Tier 1 – Traditional Advertising), `T2` (Tier 2 – DCO / Scale Media), `TS` (Tier Social – Social).
- **Three phase rows (left rail):** `HUMAN` (strategy & planning), `CRAFT` (make the work), `DELIVERY` (ship & run).
- Below the three phase rows, the `T2` lane continues with its downstream machinery (DAM handoff, legal review, hub, trafficking, archive, measurement).

## About the Design Files
The file in this bundle (`GM Creative Pipeline.dc.html`) is a **design reference created
in HTML** — a working prototype that demonstrates the intended look, layout, and behavior.
It is **not production code to copy directly.** The task is to **recreate this design in the
target codebase's existing environment** (React, Vue, Svelte, etc.) using that project's
established patterns, component primitives, and animation libraries. If no front-end
environment exists yet, choose the most appropriate framework for the project and implement
the design there.

> Note on the file format: the prototype is authored as a "Design Component" (`.dc.html`).
> You can open it directly in a browser to interact with it. Internally it is plain
> HTML + inline styles + a small vanilla-JS class for the interactions — there is no build
> step or framework dependency to reproduce; treat it as a visual/behavioral spec.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, radii, glows, and interaction
timing are all specified below and should be reproduced faithfully. Recreate the UI
pixel-accurately using the codebase's existing libraries/patterns.

## Screens / Views
There is **one screen**: a fixed-aspect design canvas of **1660 × 1560 px** that is scaled
to fit the viewport width (see *Responsive behavior*). It is composed of a sticky header
bar and the board.

### Header bar (sticky, top)
- **Layout:** `position: sticky; top: 0; z-index: 50`. Flex row, `align-items: flex-end; justify-content: space-between`, `gap: 28px`, `flex-wrap: wrap`, padding `22px 36px 18px`, bottom border `1px solid rgba(255,255,255,0.07)`. Background `linear-gradient(180deg, #090f17 0%, #080d14 75%, rgba(8,13,20,0.92) 100%)` with `backdrop-filter: blur(8px)`.
- **Left block:**
  - Eyebrow: `GM · MARKETING OPERATING MODEL` — JetBrains Mono 500, 12px, letter-spacing 0.22em, color `#3fe0d8`.
  - Title: `Creative Production Pipeline` — Space Grotesk 700, 30px, letter-spacing -0.015em, color `#f4f8fb`.
  - Subtitle: `Tier 1 · Tier 2 · Tier Social — three lanes, running in parallel` — Space Grotesk 400, 14px, color `#7e8a99`.
- **Right block:** legend + controls.
  - **Legend chips** (JetBrains Mono 500, 11px, letter-spacing 0.08em, color `#8c97a8`), each an 11×11px swatch + label, gap 16px:
    - `Stage` — swatch is a 3px-radius square with `1.5px solid #3fe0d8` border (outline only).
    - `Platform` — solid `#f25cc1` square.
    - `Automation` — solid `#a6e635` square.
  - Sub-line: `— — —  dashed = asset / data flow` — JetBrains Mono 500, 11px, color `#5b6675`.
  - Vertical divider: 1px × 46px, `rgba(255,255,255,0.1)`.
  - **Phase status text** (driven by Run flow): JetBrains Mono 500, 12px, letter-spacing 0.12em, color `#3fe0d8`. Idle text = `HOVER ANY STEP FOR DETAIL`; while running = `PHASE n/7 — <PHASE NAME>`.
  - **Run / Reset button:** JetBrains Mono 600, 13px, letter-spacing 0.1em, text color `#04110f`, background `#3fe0d8`, no border, radius 10px, padding `13px 22px`, box-shadow `0 0 26px -6px rgba(63,224,216,0.7)`. Hover background `#7af0ea`. Label toggles between `▶  Run flow` and `■  Reset`.

### Board (the 1660×1560 canvas)
All elements are **absolutely positioned** within the canvas. Coordinates below are in
design px (origin = canvas top-left).

**Entry chain (above the container):**
- `GM` box — `left 40, top 64, 92×72`. Border `1.6px solid rgba(63,224,216,0.6)`, radius 12px, card background (see tokens). Centered label `GM` — Space Grotesk 700, 24px, `#eaf0f5`.
- `CLIENT BRIEF` box — `left 600, top 58, 700×88`. Border `1.6px solid rgba(63,224,216,0.6)`, radius 14px. Eyebrow `ENTRY POINT` (mono 11.5px, `#647284`) + title `CLIENT BRIEF` (Space Grotesk 600, 23px).
- `SMARTSHEET` label chip — `left 188, top 178`. Flex row, gap 9px, padding `7px 14px`, border `1.4px solid rgba(197,105,207,0.55)`, radius 10px, purple-tinted background `linear-gradient(180deg, rgba(30,18,32,0.7), rgba(14,10,18,0.85))`. 8px lime-ish square `#c569cf` + label `SMARTSHEET` (mono 600, 13px, letter-spacing 0.18em, `#d68fdc`).

**Smartsheet container:** `left 170, top 212, 1455×1330`. Border `1.5px solid rgba(197,105,207,0.45)`, radius 22px, subtle radial fill `radial-gradient(120% 60% at 50% 0%, rgba(197,105,207,0.05), rgba(255,255,255,0.008) 60%)`, `pointer-events: none` (purely visual frame; the chip above is the interactive label).

**Column headers** (`top 244`): each is a baseline-aligned flex row, gap 11px.
- `T1` at `left 235` + `Tier 1 · Traditional Advertising`
- `T2` at `left 720` + `Tier 2 · DCO · Scale Media`
- `TS` at `left 1185` + `Tier Social · Social`
- Code (`T1/T2/TS`): Space Grotesk 700, 19px, `#3fe0d8`. Descriptor: Space Grotesk 400, 13px, `#7e8a99`.

**Phase rail labels** (left of container, `left 22`, width 150, padding `10px 14px`, `border-left: 2px solid rgba(63,224,216,0.5)`, radius `0 9px 9px 0`):
- `HUMAN` at `top 330` — sub `Strategy & planning`
- `CRAFT` at `top 482` — sub `Make the work`
- `DELIVERY` at `top 634` — sub `Ship & run`
- Label: Space Grotesk 700, 18px, letter-spacing 0.08em, `#d6efec`. Sub: JetBrains Mono 500, 10.5px, `#647284`.

**Lane geometry:** lanes are columns at `left 235` (T1, width 390), `left 720` (T2, width 390), `left 1185` (TS, width 400). The three phase rows sit at `top 300 / 452 / 604`, each box `118px` tall.

#### Nodes (cards)
Each node is a card: border `1.6px solid rgba(63,224,216,0.5)` (cyan) unless noted, radius 14px,
default background `linear-gradient(180deg, rgba(17,26,35,0.6), rgba(9,14,20,0.82))`,
padding `0 22px`, flex column, vertically centered. Each card has an **eyebrow** (JetBrains
Mono 500, 11.5px, letter-spacing 0.15em, `#647284`), a **title** (Space Grotesk 600, ~21–22px,
letter-spacing -0.01em, `#eaf0f5`), and optionally a **platform tag** (JetBrains Mono 600, 14px,
letter-spacing 0.14em). Platform tag color: **magenta `#f25cc1`** for Bynder/Figma/Celtra;
**lime `#a6e635`** for Ziflow/Clinch.

| id | Lane · Phase (eyebrow) | Title | Platform tag | Position (l, t, w, h) | Notes |
|---|---|---|---|---|---|
| `gm` | CLIENT | GM | — | 40, 64, 92, 72 | entry |
| `brief` | ENTRY POINT | CLIENT BRIEF | — | 600, 58, 700, 88 | entry |
| `smartsheet` | ORCHESTRATION | SMARTSHEET (chip) | SMARTSHEET | 188, 178 | purple chip |
| `preprod` | T1 · HUMAN | Pre-Production | — | 235, 300, 390, 118 | |
| `shoot` | T1 · CRAFT | Shoot | — | 235, 452, 390, 118 | |
| `post` | T1 · DELIVERY | Post | — | 235, 604, 390, 118 | |
| `t1dam` | T1 · ARCHIVE | Final Assets — DAM | BYNDER (magenta) | 235, 756, 390, 118 | |
| `dco` | T2 · HUMAN | DCO Pipeline | — | 720, 300, 390, 118 | |
| `figma` | T2 · CRAFT | Asset Creation | FIGMA (magenta) | 720, 452, 390, 118 | |
| `celtra` | T2 · DELIVERY | Scale Adaptation | CELTRA (magenta) | 720, 604, 390, 118 | |
| `t2dam` | T2 · HANDOFF | DAM Delivery | BYNDER (magenta) | 720, 756, 390, 108 | **dashed** border `1.6px dashed rgba(63,224,216,0.45)`, lighter fill |
| `ziflow` | T2 · REVIEW | Legal Review & Feedback Loop | ZIFLOW (lime) | 720, 894, 390, 128 | title wraps two lines |
| `assetcentral` | T2 · HUB | Asset Central | — | 720, 1042, 390, 60 | **lime** border `rgba(166,230,53,0.55)`, green-tinted fill, 8px lime square + title (Space Grotesk 600, 18px) |
| `clinch` | T2 · DISTRIBUTION | Traffick | CLINCH (lime) | 720, 1206, 390, 96 | |
| `t2final` | T2 · ARCHIVE | Final Asset — DAM | BYNDER (magenta) | 720, 1318, 390, 96 | |
| `insight` | T2 · MEASUREMENT | Reactive Insight | — | 720, 1438, 865, 86 | wide; right-aligned meta `BI-MONTHLY · CADENCE TBD` (mono 12px, `#7e8a99`) |
| `social` | TS · HUMAN | Social Strategy | — | 1185, 300, 400, 118 | |
| `content` | TS · CRAFT | Content Creation | — | 1185, 452, 400, 118 | |
| `community` | TS · DELIVERY | Community Mgmt | — | 1185, 604, 400, 118 | |

#### Connectors (SVG overlay, `pointer-events: none`)
Dashed cyan polylines with an arrowhead marker; **continuously animated** marching dashes
(see Interactions). Stroke `#4fc8c0`–`#5fd8cf`, `stroke-width 1.6–1.7`, `stroke-dasharray "7 7"`,
arrowhead marker stroked `#5fd8cf`.
- `GM → CLIENT BRIEF`: `M132,99 L596,100`.
- `CLIENT BRIEF → container` (down): `M950,146 L950,205`.
- **Asset/data flow A** — T1 final assets feed T2 asset creation: `M625,815 L674,815 L674,514 L714,514`, with a small lime up-triangle on the vertical at ~(674,548).
- **Asset/data flow B** — T2 scaled/approved assets feed TS content: `M1110,664 L1150,664 L1150,514 L1179,514`, with a lime up-triangle at ~(1150,548).

## Interactions & Behavior

### Hover a step (primary detail interaction)
On `mouseenter` of any node, that card:
- **Scales to 2×** in place (`transform: scale(2)`, `transform-origin: center center`), animated via `transition: transform .28s cubic-bezier(.2,.7,.2,1)`.
- **Lifts above neighbors** (`z-index: 60`).
- **Background becomes fully opaque** — swapped to `linear-gradient(180deg,#0f1822,#0a0f16)` so underlying cards do not show through. (The original translucent background is restored on leave.)
- Border brightens to `#7af0ea` and a glow box-shadow appears: cyan cards `0 0 0 1.5px #3fe0d8, 0 0 38px -6px rgba(63,224,216,0.75)`; lime cards use the `#a6e635` equivalent.
On `mouseleave`, all hover styles revert (transform cleared, z-index cleared, background restored).

> Implementation note: in the prototype the scale/z-index/opaque-bg are applied imperatively
> in JS (not via `:hover`) to guarantee they fire; the border/glow use a `:hover` rule. In a
> component framework, a single hover state driving all of these is cleaner.

### Run flow (animated sequence)
Clicking **Run flow** plays a 7-step timeline (`setInterval`, **1500ms** per step). Each step
lights its nodes with a bright glow; already-played nodes keep a soft glow; the matching phase
rail label also lights up. The button becomes **Reset** while playing; Reset stops the timer
and clears all glows. The timeline (groups of node ids per step) — note the phases sweep
**across all three lanes at once** to convey parallelism:

1. `gm`, `brief`, `smartsheet` — phase label "CLIENT BRIEF"
2. `preprod`, `dco`, `social` — phase "HUMAN" (rail HUMAN lights)
3. `shoot`, `figma`, `content` — phase "CRAFT" (rail CRAFT lights)
4. `post`, `celtra`, `community` — phase "DELIVERY" (rail DELIVERY lights)
5. `t1dam`, `t2dam`, `ziflow` — phase "CONSOLIDATE"
6. `assetcentral`, `clinch`, `t2final` — phase "APPROVE & ROUTE"
7. `insight` — phase "MEASURE & LOOP"

Glow values used:
- Bright cyan: `0 0 0 2px #3fe0d8, 0 0 36px -4px rgba(63,224,216,0.9), inset 0 0 30px -14px rgba(63,224,216,0.65)`
- Bright lime: `0 0 0 2px #a6e635, 0 0 36px -4px rgba(166,230,53,0.85), inset 0 0 30px -14px rgba(166,230,53,0.6)`
- Soft cyan (played): `0 0 0 1px rgba(63,224,216,0.45), 0 0 16px -8px rgba(63,224,216,0.5)`
- Soft lime (played): `0 0 0 1px rgba(166,230,53,0.45), 0 0 16px -8px rgba(166,230,53,0.5)`
- Lime nodes are: `ziflow`, `assetcentral`, `clinch`.

### Connector animation (always on)
The dashed connectors continuously "march" via `@keyframes flow { to { stroke-dashoffset: -280 } }`,
applied as `animation: flow 5s–6s linear infinite`, to convey live asset/data flow.

### Responsive behavior
The 1660×1560 board is scaled to the available width: `scale = min((wrapWidth - 8) / 1660, 1)`,
applied with `transform-origin: top left`, centered with `margin-left: (wrapWidth - 1660*scale)/2`,
and the wrapper height set to `1560*scale + 8`. Recomputed on load (with a few delayed passes for
font loading) and on `resize`. The page scrolls vertically; the header is sticky. (In a component
build, a CSS `transform: scale()` on a fixed-size board, or a responsive re-layout, are both valid;
the key requirement is the board never overflows horizontally and the header stays reachable.)

## State Management
Minimal:
- `playing: boolean` — is the Run-flow timeline active.
- `step: number` (−1 idle, 0–6 while playing) — current timeline index; drives node/phase glows and the header phase text.
- A timer handle for the 1500ms interval (cleared on Reset / unmount).
- Hover is transient (no persisted state needed) — the hovered card's transform/z-index/background are applied directly.
- Derived: per-node glow box-shadow string and per-phase-label glow are computed from `playing` + `step`.

## Design Tokens
**Colors**
- Page background: `radial-gradient(120% 80% at 50% -10%, #0d1825 0%, #06090f 55%, #04060a 100%)`
- Header background: `linear-gradient(180deg, #090f17 0%, #080d14 75%, rgba(8,13,20,0.92) 100%)`
- Card background (default, translucent): `linear-gradient(180deg, rgba(17,26,35,0.6), rgba(9,14,20,0.82))`
- Card background (hover, opaque): `linear-gradient(180deg, #0f1822, #0a0f16)`
- Cyan (stage / structure): `#3fe0d8`; bright/hover `#7af0ea`; glows `rgba(63,224,216,*)`
- Magenta (platform): `#f25cc1`; orchid container `rgba(197,105,207,*)`; chip label `#d68fdc`; chip dot `#c569cf`
- Lime (automation / hub): `#a6e635`; bright `#c4f06a`; glows `rgba(166,230,53,*)`
- Connector dashed stroke: `#4fc8c0` / `#5fd8cf`
- Text: primary `#eaf0f5` / `#f4f8fb`; muted `#7e8a99`; faint `#647284`, `#5b6675`; eyebrow `#647284`
- Hairline borders/dividers: `rgba(255,255,255,0.07–0.13)`

**Typography**
- Display / titles / labels: **Space Grotesk** (400, 500, 600, 700)
- Tags / metadata / eyebrows / mono UI: **JetBrains Mono** (400, 500, 600)
- Notable sizes: H1 30px/700; card title 21–22px/600; section code 19px/700; phase label 18px/700; platform tag 14px/600; eyebrow 11.5px/500; legend 11px/500.

**Radius:** card 14px · small box 12px · chip 10px · container 22px · pill 999px
**Border width:** 1.4–1.6px (cards), 1.5px (container)
**Spacing:** card padding `0 22px` (content vertically centered), `0 26px` on the wide insight box; header padding `22px 36px 18px`.
**Timing:** hover scale 280ms `cubic-bezier(.2,.7,.2,1)`; glow transitions 400–450ms ease; Run-flow step 1500ms; connector march 5–6s linear infinite.

## Assets
- **Fonts:** Google Fonts — Space Grotesk and JetBrains Mono (loaded via `fonts.googleapis.com`). Substitute your codebase's equivalents or self-host.
- **No raster/vector image assets.** Arrows and the entry triangle are inline SVG. Platform names (Smartsheet, Figma, Celtra, Bynder, Ziflow, Clinch) are rendered as **text tags**, not logos — if you want real logos, source the official brand marks and respect their guidelines.
- The two original hand sketches that informed this design are in `uploads/Asset 1@2x.png` and `uploads/Asset 2@2x.png` of the source project (reference only).

## Files
- `GM Creative Pipeline.dc.html` — the full interactive prototype (open in a browser to interact). Contains the markup (inline-styled), the SVG connector overlay, and the JS class implementing hover-zoom, Run-flow sequencing, and fit-to-width scaling.
