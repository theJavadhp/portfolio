# CLAUDE.md — Portfolio site for Javad Hakimpanah

Context for Claude Code working on this repo. Read this fully before making changes.

---

## What this is

A personal portfolio site for **Javad Hakimpanah**, a UI/UX Designer and Front-End Developer in Toronto who is **actively job hunting** (targeting mid-level UI/UX Designer and Front-End Developer roles, Canada + US-remote, $90–130K CAD).

The site's job is to get him interviews. Every change should be evaluated against: *does this make a hiring manager more likely to book a call?*

**Live:** https://thejavadhp.github.io/portfolio/
**Repo:** https://github.com/theJavadhp/portfolio
**Deploy:** GitHub Pages, `main` branch, root folder. Push to `main` = deploy. No CI.

---

## Hard constraints

Do not break these without asking:

1. **Single self-contained `index.html`.** All CSS is inline in `<style>` in the head. No separate stylesheets, no JS files, no build step, no framework, no npm dependencies. The whole site must work by opening the file.
2. **No external runtime dependencies.** No CDN links for fonts, icons, or libraries. If you need an icon, inline the SVG. **One approved exception (Sep 10, 2026):** Schibsted Grotesk is self-hosted from `fonts/schibsted-grotesk-latin.woff2` (one ~46KB variable file covering weights 400–900, latin subset, SIL OFL — keep `fonts/OFL.txt` beside it) and used for all text. It replaced Bitter the same day at Javad's request ("like Bricolage Grotesque, but more formal"). Don't add a second font or swap it without asking.
3. **`.nojekyll` must stay.** It stops GitHub Pages running Jekyll.
4. **`01_Resume_Javad_Hakimpanah_ATS.pdf` must stay at repo root** — the hero links to it relatively. Don't rename or move it.
5. **Relative links only** for internal assets. The site is served from a subpath (`/portfolio/`), so absolute paths like `/images/foo.png` will 404. Use `images/foo.png`.

---

## File structure

```
portfolio/
├── index.html                            # the entire site (CSS, inline SVG art, small script)
├── 01_Resume_Javad_Hakimpanah_ATS.pdf    # linked from the intro and footer
├── fonts/schibsted-grotesk-latin.woff2   # self-hosted site font
├── fonts/OFL.txt                         # its license (required by the OFL)
├── images/og-card.png                    # Open Graph / Twitter share image (1200×630)
├── .nojekyll                             # required for GitHub Pages
├── .gitignore
├── README.md                             # deploy instructions
└── CLAUDE.md                             # this file
```

---

## Design system

Redesigned Sep 10, 2026 in the design language of [robbowen.digital](https://robbowen.digital/) — at Javad's request — but rebuilt from scratch with his own palette and art. **Don't copy that site's code, artwork, or exact purple/cyan brand colors**; recognisably cloning a well-known designer's personal site would hurt him with design-literate reviewers.

Defined as CSS custom properties in `:root`. Use these — don't hardcode colors.

| Token | Value | Use | Contrast on `--paper` |
|---|---|---|---|
| `--paper` | `#f5f8fb` | page ground | — |
| `--frame` | `#ffffff` | fixed viewport frame | — |
| `--ink` | `#13204f` | text, headings | 14.6:1 |
| `--slate` | `#4a5578` | secondary text | 6.9:1 |
| `--line` | `#c93d1c` | riso coral: line art, buttons, links | 4.7:1 |
| `--fill` | `#bfdcf5` | riso blue: offset fills, hatch, dots | decorative only |
| `--pen` | `#2f6fd1` | coloured full stops, rules, the hero pen curve, focus ring | 4.6:1 |
| `--rule` / `--chip` | `#d5dee9` / `#bccadb` | hairlines, chip outlines | decorative only |

The old coral `#ff7a59` and blue `#7ab7ff` fail on a light ground (2.4:1 and 2.0:1) — don't bring them back for text.

**Theme picker (added Sep 11, 2026):** the same 9 tokens are overridden per theme via `[data-theme="x"]` blocks — Riso (default, no attribute), Teal & Coral, Purple & Pink Glow, Warm Sand & Terracotta, Navy & Mint, Electric Blue & Lime. Six two-tone swatch buttons (`.theme-dot`, conic-gradient of `--line`/`--fill`) sit in the top bar after "Hire me". A head-inline script applies a saved `localStorage` choice before first paint (no flash); a body-end script wires clicks, persistence, and keeps `<meta name="theme-color">` in sync. Every new theme's `--ink`/`--slate`/`--line`/`--pen` must hit ≥4.5:1 on its `--paper`, **and** `--pen` must stay visually distinct from `--ink` (not just contrast-legal) since it colors the heading full stops — check a rendered screenshot, not just the contrast ratio. `--frame` stays white across all themes by design (matches the fixed viewport frame). Adding a 7th theme: one CSS block + one button in the markup, nothing else. Switching themes cross-fades (a universal `transition` on color/fill/stroke/box-shadow, ~220ms, gated under `prefers-reduced-motion: no-preference`) rather than snapping instantly.

**Type:** one family — Schibsted Grotesk (self-hosted, see constraint 2) — for everything, via `--sans` (system sans is only the fallback). Body 17px/1.65; headings 700 with negative tracking (hero −0.03em, section headings −0.028em, case titles −0.022em); nav and "Hire me" are 600 uppercase at +0.16em. Section headings end in a `--pen` full stop (`<span class="stop">.</span>`). Headings use `text-wrap: balance`; hyphenated compounds that break badly get a `.nowrap` span (never change the words to fix a wrap).

**Visual language:** two-colour "riso" line illustrations — coral stroke over a pale-blue fill shifted about 5–7px down-left. In SVG, each shape is defined once in `<defs>` and drawn with `<use>` as `.rz-fill` (offset) + `.rz-line`; add `.rz-base` (paper fill) underneath when a shape must hide what's behind it. Patterns: `url(#hatch)` / `url(#dots)` (shared paint servers at the top of `<body>`). Buttons are an outlined label over an offset hatch (`.btn`, `.btn.solid`).

**Layout:** light theme, fixed white frame, sticky top bar, left-aligned `.wrap` (1140px max). The nav collapses to a Menu button at 920px (links wrap instead when JS is off). Grids collapse to one column at 760–860px.

**Motion:** concentrated in the hero only — a one-time draw-on of the pen curve, a pointer-following bezier handle, and layers that lean toward the cursor, with a slow idle drift on touch. Everything is off under `prefers-reduced-motion`. Don't add per-section scroll reveals.

**Components:** `.hero` + `.scene` (interactive SVG), `.intro`, `.work` (2-col list with `.meta` + `.chips`), `.case` (sticky `.case-art` illustration + `.facts` definition list), `.skills`, `.about`, footer `.foot`.

---

## Page structure

1. **Top bar** (sticky) — JH monogram, name + role, anchor nav, "Hire me" mailto
2. **Hero** — "Hi, my name is **Javad**." with the original headline ("I design products and ship the front-end myself.") as its subline, beside the interactive design-tool scene
3. **Intro** ("Let's work together.") — the positioning paragraph and 3 CTAs (email, résumé, LinkedIn)
4. **Selected work** (`#work`) — 6 items; titles link to their case study
5. **Case studies** (`#case-studies`) — 5 write-ups (`#framechain`, `#skyporter`, `#reno-studio`, `#ehsan-foods`, `#mofid`), each with a riso illustration and Problem / Approach / Decision / Outcome / Stack
6. **Skills** (`#skills`) — 6 groups
7. **About** (`#about`) — one paragraph
8. **Footer** (`#contact`) — "Let's talk.", email, LinkedIn, résumé

Section anchors are linked from the nav — keep them stable.

---

## ⚠️ Accuracy rules — read this carefully

This is a résumé-adjacent document used in real job applications. **Factual errors here can cost him a job offer or get one rescinded.**

- **Never invent accomplishments, metrics, employers, dates, or technologies.** If you want to add a claim and can't source it from this file or from Javad directly, ask him.
- **Never change company names, job titles, or date ranges** without explicit instruction. These get verified in reference and background checks.
- **Don't add skills he hasn't confirmed.** He specifically had backend technologies (NestJS, PostgreSQL, Docker, AWS S3) removed because a teammate built that layer, not him. Don't reintroduce them. The same goes for fal and Vertex AI: neither appears in any of his code (checked Sep 10, 2026), and both were removed from the résumé.
- Existing numbers that ARE verified: 28 screens (SkyPorter), 53 of 64 commits (SkyPorter), nine-stage pipeline (FrameChain), two supplier catalogs (Reno Studio), ten-year tenure (Mofid).
- Wording like "roughly," "over a decade," and "primary developer" is deliberately hedged. Don't sharpen hedged claims into precise ones.

---

## Factual record

### Career timeline (continuous, no gaps)

| Period | Role | Company |
|---|---|---|
| May 2026 – present | Product Designer & Front-End Developer | Trimo Tech (early-stage startup, Toronto — he's a co-founder but the site deliberately does **not** say so) |
| Jul 2024 – May 2026 | Independent Designer & Content Creator | Self-employed |
| Jan 2023 – Jul 2024 | UX Designer & Graphic Designer | Ehsan Foods |
| 2013 – Jan 2023 | UI/UX Designer | Mofid (online brokerage & stock trading platform, Iran) |

~13 years total. Site currently says "over a decade." He is positioning as **mid-level** despite the tenure — this is his explicit choice, don't "correct" it.

**Education:** UX/UI Design Certificate, University of Toronto School of Continuing Studies, Jun 2023.
**Languages:** English (professional), Persian (native). Canadian citizen.
**Contact:** javadhp@outlook.com · linkedin.com/in/javadhakimpanah

### Projects featured on the site

**FrameChain** (Aug–Sep 2026, Trimo Tech, solo — 221 commits, ~28k LOC)
Next.js 16, React 19, TypeScript, Prisma, Zod, Tailwind. Repo: `~/workspace/idea to video factory`. Nine-stage pipeline turning a website URL into a hero background video — canonical list is `lib/stages.ts`: analyze (scrape) → brief → story → refine → lock (chain plan) → frames (keyframes) → motion → assemble → export. AI: Anthropic Claude called directly (reasoning/copy); image and video models called through KIE — nano-banana (pro/edit), GPT Image 2, Kling 3.0, Seedance 2.5. **No fal integration exists in the repo or its git history** (checked Sep 10, 2026) — removed from the site. The résumé was corrected the same day to name Claude and the KIE-hosted models instead of "KIE and fal" / "four AI providers". Provider abstraction with fixture fallbacks so the full flow runs offline at zero cost. Spend-reservation system quotes cost before paid steps and blocks runs over a configured cap. Test coverage throughout.

**SkyPorter** (Apr–Jun 2026, Flutter — 53 of 64 commits his, ~26k LOC)
Peer-to-peer baggage-sharing marketplace, iOS + Android. 28 screens: two five-step guided listing flows (offer space / look for space), explore, matching, in-app chat, notifications, saved listings, profile. Repo: `~/workspace/baggage_share_mobile_app`. Flutter + Dart, Google & Apple Sign-In (Apple button is iOS-only; Google shows on both platforms), native iOS tab bar, Firebase Cloud Messaging, service layer against a Node.js REST API. Unfinished listings can be saved as drafts; the look-for-space flow shows a weight × price-per-kg estimated total. `lib/fair_pricing.dart` (a fairness meter for listing cards) exists but is **not wired in** — don't claim it. Backend was built by a teammate — **do not attribute it to Javad**.

**Reno Studio** (May 2026 – present, Trimo Tech — 77 commits his, web client only)
AI home-renovation preview: upload a photo, describe a change, get a photorealistic result. He owns the **web client** — guided studio flow, stone → colour → pattern material picker across two supplier catalogs (UniLock, Techo-Bloc), provider-aware prompt composition, R2-backed asset delivery, dynamic step count. Also wrote the design specs and implementation plans. Backend (NestJS/Postgres/Redis/BullMQ) is a teammate's — **not his**. Repo: `~/workspace/reno-platform`. Start date: Javad confirmed May 2026 (Sep 10, 2026), though his first commit is Jun 7, 2026; the same day he moved his Trimo Tech start to May 2026 so the two agree. R2 decision is his (design doc 2026-06-15): 116 images (~17 MB) stripped from unpushed git history and served from R2 instead.

**Client marketing sites** — Altin Construction, Altin Landscaping, EliteViewGlass. Cloudflare Workers + D1 migrations.

**Ehsan Foods** (Jan 2023 – Jul 2024) — confirmed by Javad (Sep 10, 2026): simplified browse, checkout, and the category structure; tightened typography and spacing; the customer journey got faster; one visual system across web, packaging, and social.

**Mofid** (2013–Jan 2023) — ten years designing brokerage and trading interfaces. Confirmed by Javad (Sep 10, 2026): asked which Mofid work he designed, he named the website and the sign-in/registration flow. The sign-up redesign was concept-to-final with patterns adopted platform-wide; the old flow was friction-heavy, hurt completion, and was visually inconsistent with the platform; the redesign cut the steps to a usable account. **Order entry, portfolio views, and market data were not confirmed** and were removed from the site and the résumé. He confirmed his Mofid work covered mobile as well as web.

---

## Current gaps — prioritized backlog

**1. No real product screenshots. Still the biggest problem.**
Each case study now has a small line illustration (Sep 10, 2026), which breaks up the text, but illustrations aren't evidence of shipped work — a reviewer still can't see a single real screen. Portfolio review is where mid-level designers most often lose offers. Available source material on his machine:

- `~/workspace/baggage_share_mobile_app/flutter_01.png`, `flutter_02.png`, `baggae-share.png` — SkyPorter screenshots
- `~/workspace/baggage_share_mobile_app/assets/images/` — app assets
- `~/workspace/AltinConstruction/public/assets/images/` — 75 images
- `~/workspace/AltinLandscaping/public/assets/images/` — 66 images
- `~/workspace/EliteViewGlass/public/img/` + `public/assets/` — 86 images
- FrameChain and Reno Studio have **no** exportable screenshots checked in — he'd need to capture those from a running instance.

If adding images: optimize aggressively (WebP, sized for display), add `loading="lazy"`, always set `alt`, and keep them in an `images/` folder with relative paths. A horizontal screenshot strip per case study would be the highest-value addition. Frame screenshots so they sit well on the light paper ground (a thin `--line` or `--rule` border, no drop shadows).

**2. Not yet checked on a real phone.** Verified in emulation (Sep 10, 2026) at true 390, 768, 1024 and 1440px widths — no horizontal overflow, menu works, focus order sane — but not on a physical iOS/Android device.

**Done Sep 10, 2026:** case-study visual hierarchy (illustrations + sticky art), favicon, Open Graph / Twitter card, `.placeholder-note` removed, skip link, visible focus ring, reduced-motion support, and every text colour checked against WCAG AA (see the design-system table).

---

## Working agreements

- **Ask before restructuring.** The content and its wording were worked over carefully. Layout, styling, and additions are fair game; rewriting the case-study copy is not, unless asked.
- **Keep it fast.** A visit costs about 61KB: `index.html` (~14KB gzipped) plus the 46KB font — no images load on the page itself. That's a feature — he designs performance-conscious interfaces and the site should demonstrate it. No loading screens.
- **Test by opening `index.html` directly** in a browser (`python3 -m http.server 8000`), and check the résumé link resolves.
- **Deploy = `git push origin main`.** Live in about a minute.
- If you change anything factual, tell Javad explicitly so he can update the résumé in `~/Documents/Claude/Projects/Jobjob/` to match. The résumé, portfolio, and his LinkedIn all have to agree.
