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
2. **No external runtime dependencies.** No CDN links for fonts, icons, or libraries. System font stack only. If you need an icon, inline the SVG.
3. **`.nojekyll` must stay.** It stops GitHub Pages running Jekyll.
4. **`01_Resume_Javad_Hakimpanah_ATS.pdf` must stay at repo root** — the hero links to it relatively. Don't rename or move it.
5. **Relative links only** for internal assets. The site is served from a subpath (`/portfolio/`), so absolute paths like `/images/foo.png` will 404. Use `images/foo.png`.

---

## File structure

```
portfolio/
├── index.html                            # the entire site
├── 01_Resume_Javad_Hakimpanah_ATS.pdf    # linked from hero
├── .nojekyll                             # required for GitHub Pages
├── .gitignore
├── README.md                             # deploy instructions
└── CLAUDE.md                             # this file
```

---

## Design system

Defined as CSS custom properties in `:root`. Use these — don't hardcode colors.

| Token | Value | Use |
|---|---|---|
| `--bg` | `#0e0e10` | page background |
| `--bg-soft` | `#17171b` | cards, skill groups |
| `--fg` | `#ececef` | body text |
| `--muted` | `#9a9aa3` | secondary text |
| `--line` | `#26262d` | borders, dividers |
| `--accent` | `#ff7a59` | coral — CTAs, tags, section labels |
| `--accent-2` | `#7ab7ff` | blue — links, case-study labels |
| `--maxw` | `1080px` | container width |
| `--radius` | `14px` | card corners |

**Type:** system stack (`-apple-system, BlinkMacSystemFont, "Inter", "Segoe UI", Roboto, sans-serif`). Base 16px/1.55. Hero uses `clamp(32px, 5vw, 56px)`.

**Layout:** dark theme, single column, `.wrap` container. Two-column grids collapse to one at 720px.

**Existing components:** `.card` (work grid), `.case` (case study with `.row` label/body pairs), `.skills .group`, `.chip` (tech tags), `.btn` / `.btn.primary`.

---

## Page structure

1. **Header** — name, role line, anchor nav
2. **Hero** — headline, positioning paragraph, 3 CTAs (email, résumé, LinkedIn)
3. **Selected work** — 6 cards in a 2-col grid
4. **Case studies** — 5 deep write-ups, each Problem / Approach / Decision / Outcome / Stack
5. **Skills** — 6 grouped cards
6. **About** — one paragraph
7. **Footer** — contact

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
**Contact:** mjhp29@yahoo.com · linkedin.com/in/javadhakimpanah

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

**1. No images anywhere. This is the biggest problem.**
Five well-written case studies with zero visuals read as a written document, not a designer's portfolio. Portfolio review is where mid-level designers most often lose offers. Available source material on his machine:

- `~/workspace/baggage_share_mobile_app/flutter_01.png`, `flutter_02.png`, `baggae-share.png` — SkyPorter screenshots
- `~/workspace/baggage_share_mobile_app/assets/images/` — app assets
- `~/workspace/AltinConstruction/public/assets/images/` — 75 images
- `~/workspace/AltinLandscaping/public/assets/images/` — 66 images
- `~/workspace/EliteViewGlass/public/img/` + `public/assets/` — 86 images
- FrameChain and Reno Studio have **no** exportable screenshots checked in — he'd need to capture those from a running instance.

If adding images: optimize aggressively (WebP, sized for display), add `loading="lazy"`, always set `alt`, and keep them in an `images/` folder with relative paths. A horizontal screenshot strip per case study would be the highest-value addition.

**2. Case studies have no visual hierarchy break.** Five in a row is a wall of text. Consider collapsing them behind expand/detail, or leading each with a hero image.

**3. Mobile hasn't been tested.** Grids collapse at 720px but nothing's been verified on a real device.

**4. No favicon.**

**5. No Open Graph / Twitter card meta.** When he shares the URL in a LinkedIn DM or application, it currently previews as a bare link.

**6. The `.placeholder-note` at the end of the case studies section is a to-do note to himself.** Remove it once images are added.

**7. Accessibility unaudited.** Dark theme with `--muted` (#9a9aa3) on `--bg` (#0e0e10) should pass, but contrast hasn't been checked systematically, and there's no skip-link or focus-visible styling.

---

## Working agreements

- **Ask before restructuring.** The content and its wording were worked over carefully. Layout, styling, and additions are fair game; rewriting the case-study copy is not, unless asked.
- **Keep it fast.** Currently ~20KB, no requests beyond the document. That's a feature — he designs performance-conscious interfaces and the site should demonstrate it.
- **Test by opening `index.html` directly** in a browser (`python3 -m http.server 8000`), and check the résumé link resolves.
- **Deploy = `git push origin main`.** Live in about a minute.
- If you change anything factual, tell Javad explicitly so he can update the résumé in `~/Documents/Claude/Projects/Jobjob/` to match. The résumé, portfolio, and his LinkedIn all have to agree.
