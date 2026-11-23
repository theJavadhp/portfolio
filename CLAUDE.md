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

1. **Single self-contained `index.html`.** All CSS is inline in `<style>` in the head. No separate stylesheets, no JS files, no build step, no framework, no npm dependencies. The whole site must work by opening the file. **Exception (Sep 14, 2026):** `work/*.html` — one dedicated page per case study holding a screenshot gallery (see below). Each of these pages is itself self-contained (own inline `<style>`, no shared CSS/JS file) — the exception is "more than one HTML file," not "no longer self-contained."
2. **No external runtime dependencies.** No CDN links for fonts, icons, or libraries. If you need an icon, inline the SVG. **One approved exception (Sep 10, 2026):** Schibsted Grotesk is self-hosted from `fonts/schibsted-grotesk-latin.woff2` (one ~46KB variable file covering weights 400–900, latin subset, SIL OFL — keep `fonts/OFL.txt` beside it) and used for all text. It replaced Bitter the same day at Javad's request ("like Bricolage Grotesque, but more formal"). Don't add a second font or swap it without asking.
3. **`.nojekyll` must stay.** It stops GitHub Pages running Jekyll.
4. **`01_Resume_Javad_Hakimpanah_ATS.pdf` must stay at repo root** — the hero links to it relatively. Don't rename or move it.
5. **Relative links only** for internal assets. The site is served from a subpath (`/portfolio/`), so absolute paths like `/images/foo.png` will 404. Use `images/foo.png`.

---

## File structure

```
portfolio/
├── index.html                            # the entire site (CSS, inline SVG art, small script)
├── work/                                 # one page per case study: full case text + screenshot gallery
│   ├── framechain.html
│   ├── skyporter.html
│   ├── reno-studio.html
│   ├── ehsan-foods.html
│   ├── mofid.html
│   ├── client-sites.html
│   ├── a2mate.html                       # "More projects" pages (added Nov 22, 2026)
│   ├── trimostudio.html
│   ├── trimotech-site.html
│   └── glass-bakeoff.html
├── 01_Resume_Javad_Hakimpanah_ATS.pdf    # linked from the intro and footer
├── fonts/schibsted-grotesk-latin.woff2   # self-hosted site font
├── fonts/OFL.txt                         # its license (required by the OFL)
├── images/og-card.png                    # Open Graph / Twitter share image (1200×630)
├── images/                               # also holds case-study screenshots (see below)
├── .nojekyll                             # required for GitHub Pages
├── .gitignore
├── README.md                             # deploy instructions
└── CLAUDE.md                             # this file
```

**Case-study screenshots (added Sep 14, 2026):** each case study on `index.html` stays illustration-only (flat riso SVG, no real screenshots inline — a photorealistic device mockup was tried inline and didn't match the site's flat aesthetic) and ends with a "Read more →" link to `work/<slug>.html`.

Each `work/<slug>.html` page: a full-bleed **21:9 header banner** (`<img class="hero-shot">`, `object-fit: cover`, and `height: auto` — without it the `height="600"` attribute pinned the banner at 600px, so it was a tall zoomed crop on phones and a thin strip on wide screens; fixed Nov 22, 2026) using that project's first/primary screenshot, sitting above the back link and title; then the full duplicated Problem/Approach/Decision/Outcome/Stack text; then, only if there's more than one screenshot, a "More screenshots" `.gallery` grid (thin `--rule` border, no drop shadow) below the text for the rest. A project with no screenshot yet shows a diagonal-hatch "Screenshot coming soon" placeholder in that same 21:9 slot (see `work/framechain.html`, `reno-studio.html`, `ehsan-foods.html`).

**To add a screenshot Javad sends:** optimize it, drop it in `images/`, then either (a) it's the project's first/only image — replace the `.hero-shot-empty` div with `<img class="hero-shot" src="../images/<file>" alt="..." width="1400" height="600">`, or (b) it's an additional image — append an `<img>` to that page's `.gallery` div (add the `<h2 class="gallery-head">More screenshots</h2><div class="gallery">...</div>` block if this is the first extra image). Device mockups (phone-in-hand, etc.) are fine as the header or in the gallery, just not inline on the main `index.html` page. Current screenshots: Mofid (real sign-in screen, header, plus a 7-image gallery added Nov 22, 2026 from Javad's own portfolio files: mobile account opening, My Mofid, desktop sign-in, registration back office, user management, Pellekan, website; very wide mockups use `.gallery img.wide` to span the row), SkyPorter (real screen in an iPhone mockup, header; splash, onboarding and explore screens in a `.gallery.phones` grid, added Nov 22, 2026 from the trimotech.ca build), Reno Studio (four iPhone-app screens from the trimotech.ca build — header is a composite of all four on the paper colour with the riso offset, gallery has each one captioned), and client-sites (Altin Landscaping as header, EliteViewGlass in the gallery — both live captures of the deployed sites).

The four "More projects" pages (Nov 22, 2026) use real material from Javad's repos, not mockups: A2MATE shows posts it made for the trimotech brand (`A2MATE/data/brands/trimotech/posts/`); TrimoStudio shows frames from finished renders (`infographic creator/projects/*/renders/final.mp4`); trimotech.ca shows captures of its own `dist/` build served locally; the glass bake-off shows the v3 run (`prompt enhancement/results/`). Gallery items there are `<figure>`s with a `<figcaption>`; `.gallery.phones`, `.gallery.frames` and `.gallery.posts` set the column width for tall images, and UI screenshots are full-width `figure.wide`.

**A2MATE and TrimoStudio UI screenshots (Nov 22, 2026, at Javad's request):** each page's header and "The app" gallery are captures of the real apps, run from copies in a cloud sandbox — never on his Mac. **Don't start his real instances to take screenshots:** on start, A2MATE begins a timer that emails page owners and another that publishes due posts to Instagram, and TrimoStudio's server runs the two-week storage rule that clears old projects. The copies used: A2MATE's committed source plus only the trimotech brand's data (no `.env`, no client brands, no owner email), all providers set to `fixture`; Geist self-hosted in the copy because `next/font/google` can't download in the sandbox. TrimoStudio's `backlot` and supporting folders plus two Trimotech projects, with a placeholder `KIE_API_KEY` so the UI shows generation as available, as it does on his machine (nothing was generated). Captured at 1400px wide, 2× pixel density, then downscaled.

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
4. **My Works** (`#work`) — 8 case studies (`#trimostudio`, `#a2mate`, `#framechain`, `#skyporter`, `#reno-studio`, `#client-sites`, `#ehsan-foods`, `#mofid`), each with a riso illustration and Problem / Approach / Decision / Outcome / Stack, ending in a "Read more →" link to that project's `work/*.html` page. **Merged Sep 14, 2026** — this used to be two sections ("Selected work" summaries + a separate "Case studies" section covering the same 6 projects at more depth); they were identical in substance, so they're now one section and one nav link. Don't re-split them without asking.
**TrimoStudio and A2MATE moved to the top of My Works (Nov 22, 2026, at Javad's request)** as full case studies; their text mirrors `work/*.html` except the Outcome lines, which on the page referred to images below. FrameChain and TrimoStudio are **separate projects** (Javad asked whether they were the same): FrameChain is his own from-scratch Next.js app (`idea to video factory`, Aug–Sep), TrimoStudio is his work on an OpenMontage fork (`infographic creator`, Oct–Nov). Don't merge them.
4b. **More projects** (`#more-work`, added Nov 22, 2026) — two compact cards (`#trimotech-site`, `#glass-bakeoff`): riso illustration, title, meta, one-paragraph summary, "Read more →". The full case study lives only on each `work/*.html` page. Then the UX certificate coursework section.
5. **Skills** (`#skills`) — 6 groups
6. **About** (`#about`) — one paragraph
7. **Footer** (`#contact`) — "Let's talk.", email, LinkedIn, résumé

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
| May 2026 – present | Product Designer & Front-End Developer | Trimotech (early-stage startup, Toronto — he's a co-founder but the site deliberately does **not** say so) |
| Feb 2023 – May 2026 | Independent Designer & Content Creator (freelance; clients include Ehsan Foods) | Self-employed |
| Oct 2016 – Jan 2023 | UI/UX Designer (software teams) | Mofid (online brokerage & stock trading platform, Tehran, Iran) |
| Jan 2013 – Sep 2016 | Graphic Designer | Mofid |

Timeline updated Nov 22, 2026 at Javad's instruction: Ehsan Foods is client work inside the freelance period, and Mofid shows both roles. The company is written **Trimotech** — the name it has used on its own site since Oct 2026 — on the site, the résumé and (pending) LinkedIn; it was "Trimo Tech" here until Javad said "Trimotech is ok" (Nov 22, 2026). ~13 years total. Site currently says "over a decade." He is positioning as **mid-level** despite the tenure — this is his explicit choice, don't "correct" it.

**Education:** Bachelor of Computer Engineering, Mehr Higher Education Institute, Arak, Iran, 2013 (confirmed Nov 22, 2026); UX/UI Design Certificate, University of Toronto School of Continuing Studies, Jun 2023.
**Languages:** English (professional), Persian (native). Canadian citizen.
**Contact:** javadhp@outlook.com · linkedin.com/in/javadhakimpanah

### Projects featured on the site

**FrameChain** (Aug–Sep 2026, Trimotech, solo — 221 commits, ~28k LOC)
Next.js 16, React 19, TypeScript, Prisma, Zod, Tailwind. Repo: `~/workspace/idea to video factory`. Nine-stage pipeline turning a website URL into a hero background video — canonical list is `lib/stages.ts`: analyze (scrape) → brief → story → refine → lock (chain plan) → frames (keyframes) → motion → assemble → export. AI: Anthropic Claude called directly (reasoning/copy); image and video models called through KIE — nano-banana (pro/edit), GPT Image 2, Kling 3.0, Seedance 2.5. **No fal integration exists in the repo or its git history** (checked Sep 10, 2026) — removed from the site. The résumé was corrected the same day to name Claude and the KIE-hosted models instead of "KIE and fal" / "four AI providers". Provider abstraction with fixture fallbacks so the full flow runs offline at zero cost. Spend-reservation system quotes cost before paid steps and blocks runs over a configured cap. Test coverage throughout.

**SkyPorter** (Apr–Jun 2026, Flutter — 53 of 64 commits his, ~26k LOC)
Peer-to-peer baggage-sharing marketplace, iOS + Android. 28 screens: two five-step guided listing flows (offer space / look for space), explore, matching, in-app chat, notifications, saved listings, profile. Repo: `~/workspace/baggage_share_mobile_app`. Flutter + Dart, Google & Apple Sign-In (Apple button is iOS-only; Google shows on both platforms), native iOS tab bar, Firebase Cloud Messaging, service layer against a Node.js REST API. Unfinished listings can be saved as drafts; the look-for-space flow shows a weight × price-per-kg estimated total. `lib/fair_pricing.dart` (a fairness meter for listing cards) exists but is **not wired in** — don't claim it. Backend was built by a teammate — **do not attribute it to Javad**.

**Reno Studio** (May 2026 – present, Trimotech — 77 commits his, web client only)
AI home-renovation preview: upload a photo, describe a change, get a photorealistic result. He owns the **web client** — guided studio flow, stone → colour → pattern material picker across two supplier catalogs (UniLock, Techo-Bloc), provider-aware prompt composition, R2-backed asset delivery, dynamic step count. Also wrote the design specs and implementation plans. Backend (NestJS/Postgres/Redis/BullMQ) is a teammate's — **not his**. Repo: `~/workspace/reno-platform`. Start date: Javad confirmed May 2026 (Sep 10, 2026), though his first commit is Jun 7, 2026; the same day he moved his Trimotech start to May 2026 so the two agree. R2 decision is his (design doc 2026-06-15): 116 images (~17 MB) stripped from unpushed git history and served from R2 instead.
**iOS app (added to the site Nov 22, 2026):** `apps/ios` in the same repo is a Flutter iPhone client, and all 41 of its commits are his (Sep 30 – Oct 7, 2026): bearer-token sign-in with a Keychain refresh token, Dart mirrors of `@reno/contracts`, entitlement-scoped modules, persisted studio draft, photo pre-check and upload, generation screen with polling/retry/tweak/save/share, projects with filters, account, Liquid Glass tab bar, buy-credits screens (web, mobile web and iOS). The repo's ownership split puts `apps/web` and `apps/ios` on the front-end side, so "web client & iOS app owner" holds. README mentions TestFlight builds; the site doesn't claim a store release.

**A2MATE** (Nov 3–18, 2026, Trimotech, solo — 390 commits, all his; 194 test files; ~35k lines of TypeScript outside tests, not cited on the site). Repo: `~/workspace/A2MATE` (no remote). Local Next.js 16 / React 19 app that turns a month's Instagram calendar into carousels, single posts, stories and reel covers for several brands. Sources for the case study: `README.md` and `docs/superpowers/specs/2026-11-03-a2mate-design.md` — per-brand kit approved once; calendar import from PDF/CSV/picture/text with flags (date outside month, weekday mismatch, duplicates, missing time); Claude Code (headless) writes posts; slides rendered with Playwright; checks for slides, captions, sources and Canadian spelling (cspell en-CA); every factual claim needs a recorded source or the post is blocked; redo one slide from a short note; ready-to-post package; spend estimated and capped; never posts to Instagram itself; README written for a teammate taking it over. The 2026-11-21 trimotech carousel is marked `posted`. Brands in `data/` include two real clients — keep them off the site.

**TrimoStudio** (Oct 7 – Nov 19, 2026, Trimotech — 249 of the repo's commits are his). Repo: `~/workspace/infographic creator` (origin TrimoTech/VideoFactory), a fork of the open-source **OpenMontage** (github.com/calesthio/OpenMontage, AGPLv3). Always credit OpenMontage: it supplies the pipelines, render engines, cost tracking and the original Backlot board (calesthio built the board; Javad has 163 commits in `backlot/` since). His: Studio page and brief intake, twenty gallery style playbooks (16 with code-rendered previews), KIE connector (images, image-to-video, narration, music), step-by-step project page, the Oct 8 UI redesign (spec `docs/superpowers/specs/2026-10-08-studio-ui-redesign-design.md`: two headers per page, one destination under several names, five button styles → one global bar, one project header, one stepper; plain ES modules and CSS), autopilot MCP server (`trimostudio`) with caps and a docked assistant, Pro styles, learned styles, captions, Send to A2MATE, Storage page. The site's frames come from Trimotech-topic videos only.

**trimotech.ca** (Sep 21 – Oct 18, 2026, Trimotech). Repo: `~/workspace/Trimo_website/trimotech.ca` (origin TriMoTech/trimotech.ca). **Mohammad made the initial commit — the one-page site with the canvas particle field (`constellation-v2.js`) and the build script — so the site doesn't claim the hero or the particle field for Javad.** His (51 commits): the blog (`tools/blog.mjs`, a ~1,200-line Markdown renderer on `node:fs`/`node:path` only; post formats, charts, stat blocks, covers, RSS, required sources), IndexNow, local SEO, privacy page, service pages, pricing as a cart, About page, Work page (device mockups, triangle backdrops, parallax), mobile menu. "About 360 KB" is the hand-authored site per that repo's CLAUDE.md (160 KB of it the og image). Blog posts are drafted by a scheduled writer with his brief (`docs/blog-writer.md`) — the site says he built the blog, not that he wrote the articles.

**Glass bake-off** (Aug 14 – Oct 2, 2026, for Elite View Glass). Folder: `~/workspace/prompt enhancement` (not a git repo; context in `bakeoff/CLAUDE.md`). Python stdlib-only local tool: one prompt across six kie.ai image-editing models with before/after sliders, a fragment picker built from the client's catalog, an analyze loop using Claude, and a findings page that checks real install photos against the prompt's rules. Verdicts quoted on the page come from its "Model notes" table (gpt-image-2 the only model to keep the exact 1672×941 frame with no drift or tint and all hardware; slowest by ~2.5×). Prompt bodies v2–v5 live in `reno-platform/docs/prompt-templates/` (his commits). The images are the client's own photos; Javad confirmed (Nov 22, 2026) he's OK showing them.

**Client marketing sites** — Altin Construction, Altin Landscaping, EliteViewGlass. Cloudflare Workers + D1 migrations. Labelled **Trimotech** on the site since Nov 22, 2026 (was "Freelance"): the résumé already lists these sites under Trimotech and trimotech.ca's Work page shows them as its builds. Javad: "since I worked on them it's ok to have them under my name."

**Ehsan Foods** (freelance client, 2023–2024; shown as "Freelance client" since Nov 22, 2026) — confirmed by Javad (Sep 10, 2026): simplified browse, checkout, and the category structure; tightened typography and spacing; the customer journey got faster; one visual system across web, packaging, and social.

**Mofid** (Jan 2013 – Jan 2023; graphic designer until Sep 2016, then UI/UX designer on the software teams) — ten-year tenure, the last six designing brokerage and trading interfaces. Confirmed by Javad (Nov 22, 2026): lead designer in role, not his official title, working with two other designers in a team of ten; worked on EasyTrader, My Mofid, Pellekan, the OAuth sign-up/sign-in (designed it and built its front end; the old login wasn't mobile-friendly as customers moved from laptops to phones; still in use) and internal admin panels. Visit figures come from his own Similarweb reports for Nov 2022 – Jan 2023: reg.emofid.com about 490,000 visits a month, 91% mobile; my.emofid.com about 2.1 million, 87% mobile. Confirmed by Javad (Sep 10, 2026): asked which Mofid work he designed, he named the website and the sign-in/registration flow. The sign-up redesign was concept-to-final with patterns adopted platform-wide; the old flow was friction-heavy, hurt completion, and was visually inconsistent with the platform; the redesign cut the steps to a usable account. **Order entry, portfolio views, and market data were not confirmed** and were removed from the site and the résumé. He confirmed his Mofid work covered mobile as well as web.

---

## Current gaps — prioritized backlog

**1. Real product screenshots — in progress, most projects still missing.**
Solved for Mofid (real sign-in screenshot, sourced from an old Framer portfolio at javadhp.framer.website), SkyPorter (a real screen composited into an iPhone mockup), and the client-sites case study (live captures of altinlandscaping.com and eliteviewglass.com) — see `work/*.html` above. Reno Studio got its iPhone screens on Nov 22, 2026 (from the trimotech.ca build's `dist/assets/work/`). Still open: **FrameChain and Ehsan Foods** have no screenshots yet (their `work/*.html` pages show a "coming soon" placeholder), and Reno Studio has none of its web client. A2MATE and TrimoStudio got UI screenshots on Nov 22, 2026 (see above for how — and why not from his running apps). Checked Sep 14, 2026 — the previously-listed local source material turned out mostly unusable:

- `~/workspace/baggage_share_mobile_app/flutter_01.png` / `flutter_02.png` are **0-byte broken files**; `baggae-share.png` is just the app icon, not a screenshot. None of it was usable for SkyPorter — the real screenshot came from Javad directly instead.
- `~/workspace/AltinConstruction/public/assets/images/`, `AltinLandscaping/public/assets/images/`, `EliteViewGlass/public/img/`+`public/assets/` are content/asset images (photos, icons), not screen captures of the built sites — the client-sites screenshots were captured live from the deployed sites instead, not from these folders.
- FrameChain and Reno Studio still have **no** exportable screenshots anywhere — genuinely need capturing from a running instance or provided by Javad.

When Javad sends more screenshots: optimize (resize + JPEG ~70-75 quality via `sips`, or better if available), add `loading="lazy"`, always set a factual `alt`, drop them in `images/` with relative paths, and append an `<img>` to the relevant `work/<slug>.html`'s `.gallery` div — nothing else needs to change. Device mockups (phone-in-hand, etc.) are fine inside a `work/` gallery; keep the main `index.html` case studies illustration-only.

**1b. Resolved Nov 22, 2026:** the client sites are labelled Trimotech (they were "Freelance"); the company is written Trimotech everywhere; Javad is OK with the glass bake-off showing the client's photos. The four new projects and Reno's iPhone app were added to `facts.yaml` at his request, and the base résumé (`01_Resume_Javad_Hakimpanah_ATS.pdf`) was re-rendered from it.

**2. Not yet checked on a real phone.** Verified in emulation (Sep 10, 2026) at true 390, 768, 1024 and 1440px widths — no horizontal overflow, menu works, focus order sane — but not on a physical iOS/Android device.

**Done Sep 10, 2026:** case-study visual hierarchy (illustrations + sticky art), favicon, Open Graph / Twitter card, `.placeholder-note` removed, skip link, visible focus ring, reduced-motion support, and every text colour checked against WCAG AA (see the design-system table).

**Done Sep 14, 2026:** "UX certificate coursework" section added (Simplist, Easy Travel, Fridge Friend — clearly labeled as coursework, not client work); "Production marketing sites for home-services clients" case study added; per-project `work/*.html` screenshot pages added (see above).

---

## Working agreements

- **Ask before restructuring.** The content and its wording were worked over carefully. Layout, styling, and additions are fair game; rewriting the case-study copy is not, unless asked.
- **Keep it fast.** A visit costs about 61KB: `index.html` (~14KB gzipped) plus the 46KB font — no images load on the page itself. That's a feature — he designs performance-conscious interfaces and the site should demonstrate it. No loading screens.
- **Test by opening `index.html` directly** in a browser (`python3 -m http.server 8000`), and check the résumé link resolves.
- **Deploy = `git push origin main`.** Live in about a minute.
- If you change anything factual, tell Javad explicitly so he can update the résumé in `~/workspace/jobjob/` (`profile/facts.yaml`, rendered by `resume/render_resume.js`) to match. The résumé, portfolio, and his LinkedIn all have to agree.
