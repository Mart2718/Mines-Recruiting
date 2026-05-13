# Mines Softball Recruiting Page — Design System

**Version:** 1.0
**Last updated:** May 11, 2026
**Owner:** Marty Romero
**Scope:** A reusable design specification for the Colorado School of Mines Softball recruiting web page (`index.html`, `videos.js`) and any companion assets (graphics, social cards, printable one-pagers).

This document is intended to be read top-to-bottom by anyone — human or LLM — who is about to build, edit, or extend the page. It captures the visual language, component patterns, voice, and accessibility commitments, plus a list of what is missing or undecided and needs your call.

---

## 1. Brand Foundations

### 1.1 Two parallel brand systems

Mines uses two related but distinct visual identities. The recruiting page should respect both:

| System | Authority | Where it lives | Notes |
|---|---|---|---|
| **Institutional brand** (mines.edu) | Communications & Marketing | brand.mines.edu | Primarily blue + white + Colorado red accent. Heritage-driven. |
| **Athletics brand** (Orediggers) | Mines Athletics | minesathletics.com | Bolder, darker navy + silver, sports-paced photography. Blaster mascot marks are athletics-only. |

The recruiting page is an athletics-facing artifact. Lead with athletics palette and energy; defer to institutional standards for type, logo lockups, and editorial style.

### 1.2 Voice & tone

The page is talking to a 16–18-year-old prospect, their parents, and (often) their travel-ball coach — usually all in the same scroll. The voice should be:

- **Confident, not boastful.** Mines doesn't need to oversell — the rankings, salaries, and outcomes do the work. State facts with calm authority.
- **Specific over generic.** "110 stolen bases in 124 attempts in 2026" beats "we play fast." Real numbers, real names, real places.
- **Warm in human moments.** When talking about coach, teammates, M Climb, E-Days — drop the formality. Recruits feel belonging or they don't.
- **Honest about rigor.** Mines is hard. Don't hide it; frame it as the reason a Mines degree is worth what it's worth.
- **Athlete-first, scholar-equal.** Both identities matter. Never imply one comes at the cost of the other.

Avoid: generic recruiting clichés ("family atmosphere," "next level"), exclamation points stacked together, all-caps shouting outside of display type, anything that sounds like a brochure from 2008.

Use: short declarative sentences. Numbers. Place names. Player names where you have permission. Mount Zion. Clear Creek. The M.

---

## 2. Color System

### 2.1 Tokens (use these in CSS variables)

The token names below are what already appears in your context file. I've kept them so existing CSS keeps working, but the **values are tuned to align with Mines Athletics** (Blaster Blue family) rather than a generic navy.

```css
:root {
  /* --- Primary navy ramp (athletics) --- */
  --navy-deep:  #0B1A33;   /* darkest — footer, hero overlay */
  --navy:       #122341;   /* primary athletics blue (usteamcolors source) */
  --navy-mid:   #21314d;   /* Mines institutional Dark Blue (PMS 533 C) */
  --navy-blast: #09396C;   /* Blaster Blue (PMS 534 C) — athletics signature */
  --navy-light: #879EC3;   /* Light Blue (PMS 535 C) — soft accents */
  --navy-pale:  #CFDCE9;   /* Pale Blue (PMS 538 C) — section tints */

  /* --- Accent: gold (recruiting-page choice, not official Mines) --- */
  /* See §2.3 — this is a design decision you've made for this page.
     Justified by the "City of Golden" tie-in and by needing a warmer
     CTA color than silver provides. */
  --gold:       #C8960C;   /* primary gold — borders, accent rules */
  --gold-light: #F0B429;   /* bright gold — hover, highlights, CTA */
  --gold-pale:  #FFF8E7;   /* pale gold — background tint blocks */

  /* --- Neutrals (Mines institutional) --- */
  --silver:     #BDBCBC;   /* Cool Gray 4 C — secondary text on dark */
  --silver-mid: #81848A;   /* PMS 877 C metallic equivalent */
  --gray-warm:  #75757D;   /* accessible body text on white */
  --white:      #FFFFFF;
  --off-white:  #F7F8FA;   /* page background alt */

  /* --- Single permitted accent for emergencies / errors --- */
  --co-red:     #CC4628;   /* Colorado Red (PMS 173 C) — ≤10% use */
}
```

### 2.2 Usage rules

- **70 / 20 / 10 rule.** Roughly 70% navy family, 20% neutral (silver/white/off-white), 10% gold accent. Colorado Red is a *fifth color* and should appear only as a thin stroke or icon, never as a background fill.
- **Text on navy** — use `--white` or `--silver` (≥4.5:1 contrast). Never use `--gold` for body text; it fails AA on most navies. Gold is for UI accents and short display words only.
- **Hero / header backgrounds** — `--navy-deep` to `--navy-blast` gradient is the signature.
- **Section tints** — alternate between `--white`, `--off-white`, and `--navy-pale` to give the scroll rhythm. Never tint a section in gold-pale unless the section is short and celebratory (e.g., the rankings strip).
- **Borders & rules** — 2px gold rules between hero sections; 1px `--silver` rules inside cards.
- **Hover states** — links and buttons shift from `--gold` to `--gold-light`; icons shift from `--silver` to `--white` on dark backgrounds.

### 2.3 Flagged decision: gold vs. silver

Mines' *official* athletics palette is **blue + silver** (#BDBCBC). Your current page introduces **gold** (#C8960C / #F0B429) as a secondary accent. Reasoning that supports keeping gold:

- Ties to "City of Golden" / Pikes Peak gold rush heritage.
- The Mines accent palette does include "Golden Tech" (#F1B91A), so a gold note isn't off-brand — it's an accent.
- Silver alone reads cold and gray on screen; gold gives the page warmth and a CTA color that pops on navy.

If you ever need a fully on-brand version (e.g., a piece that has to go through Mines Marcom review), swap `--gold*` for `--silver` and `--white` and the system holds. **Note this in the README** so a future editor doesn't get confused.

---

## 3. Typography

### 3.1 Current page choice

| Role | Family | Source | Why |
|---|---|---|---|
| Display / section titles | **Bebas Neue** | Google Fonts | Tall, athletic, condensed — reads as scoreboard / jersey. |
| Subheads / labels | **Barlow Condensed** | Google Fonts | Same energy as Bebas with more weight range. |
| Body / UI | **Barlow** | Google Fonts | Open, modern sans; great at 16–18px. |

These are **not** the official Mines fonts — Mines uses **Montserrat** for web headers and **Open Sans** for body (Halyard, Oswald, Boyrun, Roboto Mono are print-only). Your Bebas/Barlow stack is a deliberate athletics-flavored choice and reads stronger on a recruiting page than Montserrat would. Document the choice in the repo README.

### 3.2 Type scale (16px base)

```css
--fs-display:  clamp(3.5rem, 7vw, 6rem);     /* hero title (Bebas Neue) */
--fs-h1:       clamp(2.25rem, 4vw, 3.25rem); /* section title (Bebas Neue) */
--fs-h2:       clamp(1.5rem, 2.5vw, 2rem);   /* subsection (Barlow Cond. 700) */
--fs-h3:       1.25rem;                       /* card title (Barlow Cond. 700) */
--fs-eyebrow:  0.875rem;                      /* uppercase tag (Barlow Cond. 600, letter-spacing 0.12em) */
--fs-body:     1rem;                          /* 16px (Barlow 400) */
--fs-body-lg:  1.125rem;                      /* lead paragraph */
--fs-small:    0.875rem;                      /* meta, captions */
--fs-stat:     clamp(2.5rem, 5vw, 4rem);      /* big-number stats (Bebas Neue) */
```

### 3.3 Type rules

- **Display & H1 are uppercase Bebas Neue.** Don't lowercase them; the typeface's character is in the all-caps reading.
- **Letter-spacing matters.** Bebas Neue at large sizes wants `letter-spacing: 0.02em` to feel modern instead of squished.
- **Line-height.** Display: 1.0–1.05. Headings: 1.15. Body: 1.55–1.65.
- **Don't mix more than two weights of Barlow in one card.** Pick one regular + one bold.
- **Never set body copy in Bebas Neue.** It's a display-only face.
- **Numbers in stats blocks** use tabular-nums: `font-variant-numeric: tabular-nums;` so columns of stats line up.

---

## 4. Layout & Spacing

### 4.1 Grid

- Max content width: **1200px**, centered.
- Outer gutter: **24px** on mobile, **48px** at ≥768px, **clamp** to 64px at ≥1280px.
- Card grids: **1 col mobile → 2 col at 720px → 3 col at 1024px** (3 is the default for stats and major lists; 4 is allowed for short logo/ranking strips).

### 4.2 Spacing scale

Use a single spacing token set; do not invent one-off values.

```css
--sp-1:  4px;
--sp-2:  8px;
--sp-3:  12px;
--sp-4:  16px;
--sp-5:  24px;
--sp-6:  32px;
--sp-7:  48px;
--sp-8:  64px;
--sp-9:  96px;
--sp-10: 128px;
```

Section vertical rhythm: **`--sp-9` top and bottom** on desktop, **`--sp-7`** on mobile. Cards: **`--sp-5`** internal padding minimum.

### 4.3 Section pattern

Every major section follows the same shape:

1. **Eyebrow tag** (uppercase Barlow Condensed, gold, letter-spaced)
2. **Section title** (Bebas Neue, navy on light bg / white on dark bg)
3. **One-line lede** (Barlow 1.125rem, gray-warm)
4. **Body content** (cards, stats, prose, or photo strip)
5. **Optional CTA strip** (gold rule above, link to questionnaire)

This rhythm gives a recruit a predictable reading pattern — by section 3 they know where to look.

---

## 5. Component Patterns

### 5.1 Hero

- Full-bleed background image (use `Team.png` or `M Climb Softball.jpg` as default).
- Linear-gradient overlay: `linear-gradient(180deg, rgba(11,26,51,0.55) 0%, rgba(11,26,51,0.85) 100%)`.
- Display title in white Bebas Neue.
- Single primary CTA button (gold) → questionnaire.
- Single secondary text link (white underlined) → schedule or roster.
- Height: `min(85vh, 720px)`.

### 5.2 Stat card

- Background: `--navy-blast` or `--white`.
- Big number (Bebas Neue, `--fs-stat`, gold on navy / navy on white).
- Label below (Barlow Condensed uppercase, letter-spaced).
- Optional micro-context line in `--silver` / `--gray-warm`.
- Border-radius: 8px. Subtle box-shadow `0 4px 16px rgba(11,26,51,0.08)` on white cards only.

### 5.3 Ranking row

A 4-column strip used for the rankings band (#1 Niche, #1 WSJ, etc.):

- Number (Bebas Neue, gold, `--fs-stat`).
- Description (Barlow Condensed 600, 2 lines max).
- Source + year (Barlow, `--fs-small`, `--silver-mid`).
- Vertical silver divider between columns at ≥720px.

### 5.4 Person card (coach / staff)

- 1:1 square photo, top.
- Name (Bebas Neue, navy).
- Title (Barlow Condensed uppercase, gold).
- 2–3 line bio (Barlow body).
- "Read full bio →" link.

Use `Coach Echohawk.jpg` for Echo-Hawk's card.

### 5.5 Facility card

- 16:9 photo with subtle navy-deep bottom gradient.
- Facility name overlaid bottom-left in white Bebas Neue.
- Caption block below image with 2–3 facts (capacity, year renovated, signature feature).

Use `Field.png` for Joe Coors Jr. Softball Field. Facts to surface:

- Located at the base of Mount Zion, west end of the Clear Creek Athletics Complex.
- Seats 250.
- Panoramic views of Mount Zion, Mount Galbraith, and Clear Creek Canyon beyond the outfield fence.
- Major renovation 2018–19 (new dugouts, press box, backstop, seating, Daktronics scoreboard).
- Artificial turf installed Fall 2024 (project led by alumnae Kerry Siggins '01, Kari Gonzales '02, Kim Alanis '04 MS '05).
- Named for Joe Coors, Jr. in August 2020 via anonymous donation.

### 5.6 Photo strip

A 3-up or 4-up edge-to-edge band of campus / city photos. No captions — purely vibe. Use:

- `GoldenCO_WashingtonStreet.jpg` — Golden's "Howdy Folks" arch.
- `clear-creek-golden-co-coors-brewery.jpg` — Clear Creek through downtown.
- `M Climb.png` or `m-climb 2.jpg` — the M Climb tradition.

### 5.7 Major-by-category card

Used in the Academics tab. Three-column responsive grid.

- Eyebrow: category name (e.g., "Computing & Data").
- List of majors with starting-salary range to the right (Barlow tabular-nums).
- Bottom rule in gold; "See all 21 majors →" link.

### 5.8 CTA / Questionnaire band

The recruiting questionnaire (`https://minesathletics.com/sb_output.aspx?form=8`) should appear **at least three times** on the page: top hero, after Echo-Hawk bio, and as a sticky bottom band on mobile.

- Background: `--navy-deep`.
- Headline: "Ready to be an Oredigger?" (Bebas Neue, white).
- One sentence (Barlow, silver).
- Big gold button: "Start the Questionnaire →".
- Below button, small print: "Takes about 5 minutes."

### 5.9 Video embed

Use the `videos.js` config pattern already in the repo. Each embed is a 16:9 iframe with rounded 8px corners and a navy-blast border. Always pair with a short caption (Barlow Condensed, uppercase eyebrow) so the page still makes sense if a video fails to load.

---

## 6. Iconography & Graphical Style

- **Icon set:** prefer a single open-source set — Lucide or Heroicons (outline weight) — at 24px default. Never mix two icon sets in one page.
- **Stroke weight:** 1.5–2px.
- **Color:** `--gold` on navy backgrounds; `--navy-blast` on white. Never multi-color icons.
- **Emoji:** the current tab labels in your context file use emoji (⚾🏆🎓💼🏔). These are fine for tab nav, but **do not embed emoji inline in body copy** — they break the tonal register.
- **Shapes & decorative elements:** thin gold horizontal rules, occasional 1px silver divider, no drop shadows on the page background, no gradients except in the hero overlay and CTA band.

---

## 7. Imagery Guidelines

### 7.1 What's already in the folder

| File | Suggested use |
|---|---|
| `Team.png` | Hero background OR Program tab anchor image |
| `Coach Echohawk.jpg` | Coach person card |
| `Field.png` | Joe Coors Jr. Field facility card (primary) |
| `Fields.png` | Facility card alternate / wide view |
| `M Climb.png` | Campus Life tab — M Climb tradition |
| `M Climb Softball.jpg` | Hero alternate (softball-specific M Climb) |
| `m-climb 2.jpg` | Photo strip |
| `GoldenCO_WashingtonStreet.jpg` | Golden city panel — Washington Ave. arch |
| `clear-creek-golden-co-coors-brewery.jpg` | Golden city panel — Clear Creek |

### 7.2 Photo treatment

- **Crop tight on action and faces.** Long-lens softball photos cropped to show eye-level intensity beat wide stadium shots for emotional pull.
- **Saturation:** lift slightly (+5 to +10) so navy uniforms read rich, not muddy. Don't crush blacks.
- **Avoid stock photography.** Every image on this page should be real Mines/Golden imagery. If you ever need a placeholder, use a flat navy block with white Bebas Neue text saying what should go there, not a stock photo.
- **Alt text is required for every image.** See §9.

---

## 8. Tabbed Navigation

The page uses 5 tabs (your existing structure — keep it):

1. ⚾ **The Program** — overview, 2026 highlights, Coach Echo-Hawk, Joe Coors Jr. Field, questionnaire CTA
2. 🏆 **Athletic Excellence** — NCAA championships, achievement stats, women's athletics
3. 🎓 **Academics** — 21 majors by category with salary ranges, 6 career pathway cards
4. 💼 **Career Outcomes** — 4 outcome stats, ranking rows, testimonial
5. 🏔 **Campus Life** — Golden CO 6-panel, photo strip, traditions, campus stats

Tab styling:

- Desktop: horizontal tabs, navy bar, active tab underlined in 3px gold, inactive in silver.
- Mobile: collapse to a sticky select / accordion (don't try to fit 5 tabs across a phone).
- Active tab state must be reflected in the URL hash (`#program`, `#excellence`, etc.) so links are shareable.

---

## 9. Accessibility (WCAG 2.1 AA)

Non-negotiable on a Mines page — Mines is highly attentive to DOJ digital accessibility requirements.

- **Color contrast:** all text ≥4.5:1 against its background; large display text ≥3:1. The gold-on-navy combination is fine for ≥24px display text; **never** use gold for body copy.
- **Focus states:** visible 2px gold outline with 2px offset on every interactive element. Do not remove default outlines without replacing them.
- **Tab order:** logical top-to-bottom. Tab nav must be keyboard-operable (left/right arrows between tabs).
- **Alt text:** every `<img>` has an `alt` attribute. Decorative images get `alt=""`. Player / coach photos describe the person and context ("Head Coach Tobin Echo-Hawk in the Joe Coors Jr. Field dugout"). M Climb photos describe the tradition.
- **Headings:** one `<h1>` per page (the hero title), proper `<h2>` → `<h3>` nesting inside sections. Don't skip levels.
- **Iframes** (videos, questionnaire if embedded) carry a meaningful `title` attribute.
- **Reduced motion:** wrap any auto-playing background or scroll-triggered animation in `@media (prefers-reduced-motion: reduce)` and disable.
- **Captions:** any video embed needs captions (per your standing accessibility commitment). Note this in `videos.js` comments so the next person remembers.

---

## 10. Tone & Microcopy Patterns

### 10.1 Headline patterns that work

- **Number + verb + place.** "13–7 at Joe Coors Jr. Field." "First 100-steal season in program history."
- **Place + meaning.** "Golden, Colorado. 12 miles west of Denver. A different gravity."
- **One-line promise.** "An engineering degree. An NCAA roster spot. The Rockies out the dugout window."

### 10.2 CTAs

Use verb-first language. Tested and good:

- Start the Questionnaire →
- Visit Campus →
- See the 2026 Schedule →
- Meet Coach Echo-Hawk →

Avoid: "Click here," "Learn more" (alone), "Submit."

### 10.3 Stat labels

Always pair the number with a unit and a year/scope:

- ✅ "110 stolen bases — 2026 season, NCAA DII"
- ❌ "110 SB"

---

## 11. File & Code Conventions

- **One `index.html`** — single file for the recruiting page. Keep CSS inline in a `<style>` block at top until it exceeds ~600 lines, then split to `styles.css`.
- **`videos.js`** — config-only file. YouTube IDs go here, nothing else. Comment each entry with where it appears on the page.
- **CSS variables** at `:root` — never hardcode hex values inside component rules.
- **Class naming** — BEM-ish (`.card`, `.card__title`, `.card--coach`) or simple utility names. Stay consistent within a file.
- **No frameworks** unless you decide to add one explicitly; this page is light enough to be hand-rolled HTML/CSS/JS, which keeps Netlify deploys instant.
- **Image filenames** — lowercase, hyphen-separated for any new images added (`joe-coors-field-pano.jpg`). The existing mixed-case filenames are fine to keep but rename on next batch.

---

## 12. What's Missing / Open Questions

Things to decide or source before the page is "done."

- [ ] **Official Coach Echo-Hawk headshot URL** from Mines Athletics CDN (current local `Coach Echohawk.jpg` is fine as placeholder; verify license for public web use).
- [ ] **Joe Coors Jr. Field photo licensed for web use** (current `Field.png` works; confirm origin).
- [ ] **Recruiting / highlight video IDs** — placeholders in `videos.js` need real YouTube IDs.
- [ ] **Player testimonial quotes** with permission to publish (Cassidy Chvatal, Kendall Aragon, Kellan Ton are candidates).
- [ ] **Major-spotlight quotes** — "I'm a Mechanical Engineering major and I play CF" style.
- [ ] **Scholarship & financial-aid section for parents** — currently absent.
- [ ] **Roster snapshot** — should the page link to the official roster, embed a small subset, or both?
- [ ] **Decision: keep gold accent or revert to silver-only?** (See §2.3.)
- [ ] **Social proof band** — any chance of a 30-second coach video clip embedded in the hero?
- [ ] **Open Graph image** — a 1200×630 social-share card with team photo + "Mines Softball Recruiting" overlay. Not yet created.
- [ ] **Favicon** — using a Mines-branded favicon (the "M") is recommended; confirm licensing or use a generic softball icon.
- [ ] **Analytics** — decide whether to add Plausible / GA4 to track which CTAs convert.
- [ ] **Sticky mobile CTA** for the questionnaire — designed in §5.8, not yet built.

---

## 13. Quick-Reference Cheat Sheet

```
PRIMARY      navy-blast  #09396C     headings, buttons, accent bars
DARK         navy-deep   #0B1A33     hero overlay, footer
ACCENT       gold        #C8960C     CTAs, rules, hover
HOVER        gold-light  #F0B429     button hover
NEUTRAL      silver      #BDBCBC     secondary text on navy
ALERT        co-red      #CC4628     ≤10% use, never bg

DISPLAY      Bebas Neue, uppercase, 0.02em tracking
HEADING      Barlow Condensed 700
BODY         Barlow 400, 16px, line-height 1.6

GRID         max 1200px / gutter 24–64px / 1–2–3 col responsive
SECTION      ~96px vertical rhythm
RADIUS       8px on cards, 0 on bands
SHADOW       0 4px 16px rgba(11,26,51,0.08) on white cards only

CTA URL      https://minesathletics.com/sb_output.aspx?form=8
COACH URL    https://minesathletics.com/sports/softball/roster/coaches/tobin-echo-hawk/1118
FIELD URL    https://minesathletics.com/facilities/joe-coors-jr-softball-field/11
CITY URL     https://minesathletics.com/facilities/city-of-golden/16
```

---

## 14. Sources

- [Joe Coors, Jr. Softball Field – Mines Athletics](https://minesathletics.com/facilities/joe-coors-jr-softball-field/11)
- [Tobin Echo-Hawk – Coach Bio – Mines Athletics](https://minesathletics.com/sports/softball/roster/coaches/tobin-echo-hawk/1118)
- [Tobin Echo-Hawk Announced As Softball Head Coach (Dec 2024)](https://minesathletics.com/news/2024/12/3/tobin-echo-hawk-announced-as-softball-head-coach.aspx)
- [City of Golden – Mines Athletics](https://minesathletics.com/facilities/city-of-golden/16)
- [Softball Recruit Questionnaire](https://minesathletics.com/sb_output.aspx?form=8)
- [Mines Brand: Colors, Fonts & Graphic Elements](https://brand.mines.edu/fonts/)
- [Mines Visual Identity Hub](https://brand.mines.edu/visual-identity/)
- [Colorado School of Mines Visual Identity Guide (PDF)](https://brand.mines.edu/wp-content/uploads/sites/425/2023/03/colorado-school-of-mines-visual-identity-guide.pdf)
- [Colorado School of Mines Colors – US Team Colors](https://usteamcolors.com/colorado-school-of-mines-colors/)
