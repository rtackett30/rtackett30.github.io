# rtackett30.github.io

Personal academic site for Ronald J. Tackett, Ph.D., Founding Head of the School of
Foundational Studies and Associate Professor of Physics at Kettering University.

Live at <https://rtackett30.github.io/>. Served by GitHub Pages from the `main` branch,
repo root. Static HTML with no build step: commit a file and it is deployed.

## Contents

| File | Purpose |
|---|---|
| `index.html` | Home page: bio, document cards, live blog feed |
| `cv.html` | Curriculum vitae |
| `talks.html` | Recent invited talks, with slide decks as PDFs |
| `teaching.html` | Teaching Philosophy |
| `admin.html` | Administrative Philosophy |
| `ai.html` | Professional Statement on the Use of Artificial Intelligence |
| `Tackett_CV_Redesigned.pdf` | PDF counterpart of `cv.html` |
| `Teaching_Philosophy_Tackett.pdf` | PDF counterpart of `teaching.html` |
| `Admin_Philosophy_Tackett.pdf` | PDF counterpart of `admin.html` |
| `AI_Statement_Tackett.pdf` | PDF counterpart of `ai.html` |
| `Tackett_CoLLT_Sept2026_In-the-Age-of-AI.pdf` | Slides, CoLLT, 4 Sep 2026 (exported from PowerPoint) |
| `Tackett_CoLLT_Apr2026_SoFS_Institutional_Profile.pdf` | Slides, CoLLT, 10 Apr 2026 (exported from PowerPoint) |
| `bc-lockup-light-tagline.svg` | *Boundary Conditions* lockup, used in the blog section of `index.html` |
| `Tackett_Mace.jpg` | Commencement photograph; the About-section image on `index.html` and the JSON-LD `image` |
| `sitemap.xml` | Sitemap, linked from `index.html` |
| `robots.txt` | Allows all crawlers; points to the sitemap |
| `404.html` | Styled not-found page, served automatically by GitHub Pages |
| `og-card.png` | 1200x630 link-preview card, referenced by `og:image` on every page |
| `favicon-32.png`, `apple-touch-icon.png`, `icon-512.png` | Site icons (RT monogram, portfolio branding, not the blog mark) |
| `googledab7e3e171bf116c.html` | Google Search Console ownership verification |

## Files that must not move or be renamed

- **`googledab7e3e171bf116c.html`**: Search Console verification uses the file method, so
  the filename *is* the credential and it must resolve at the repo root. Rename it or move it
  into a subfolder and site verification silently lapses. There is no verification meta tag in
  `index.html`; this file is the only mechanism in use.
- **`bc-lockup-light-tagline.svg`**: referenced by relative path from `index.html`. The
  `<img>` has an `onerror` handler that hides itself, so a missing file degrades quietly
  rather than showing broken alt text, which also means its absence is easy to miss.

## Editing conventions

- **American English** throughout: spelling, usage, punctuation.
- **No em dashes.** Use commas, semicolons, colons, or restructure the sentence. One em dash
  survives in Section I of the Administrative Philosophy, carried over from an earlier draft;
  remove it when that prose is next revised.
- Each page is self-contained: its CSS lives in a `<style>` block in its own `<head>`. There is
  no shared stylesheet, so a change to shared visual language has to be repeated per file.
- Design tokens are the `:root` custom properties at the top of each `<style>` block:
  `--accent` (#0D1F4C), `--orange` (#C9921A), `--ku-blue` (#27A9E1), and in `index.html`
  `--ku-gold` (#FFCE01).
## Mobile

Single-column responsive; breakpoints at 640px and 420px (600px on the document pages).
Things that were fixed and are easy to reintroduce:

- **No `white-space: nowrap` on hero text.** The `<h1>` and the title line both had it, which
  forced horizontal scrolling on a 320px screen. The remaining nowrap rules are on nav links
  (intentional; the bar scrolls) and inside CV cells, which are overridden at 600px.
- **The hero tagline is no longer hidden on mobile.** It was `display: none` below 640px, so
  "Scientist by training / Teacher by calling / Administrator by circumstance" vanished on
  phones. It now moves below the name with a top rule instead of the left rule.
- **`.about-figure` unfloats below 640px.** At 33% width on a phone the photo left roughly 30
  characters per line beside it. It now sits full width, capped at 260px, centered.
- **CV tables stack below 600px.** `.cv-table` and `.mentor-table` have nowrap columns that
  overflowed; each row becomes a block with left-aligned cells.
- **`html, body { overflow-x: hidden }` and `img, svg { max-width: 100% }`** guard against any
  residual sideways scroll.
- **Nav links are 44px tall** so the tap target meets guidance even though the label is 10-11px.

## Accessibility

The site targets WCAG 2.1 AA. Every text/background pair was measured; all pass. Before
changing any color, check it against its actual background:

| Use | Value | Ratio |
|---|---|---|
| Gold text on navy (hero) | `--ku-gold` #FFCE01 | 10.69:1 |
| Gold text on white (CV dates, pub numbers, years, course codes) | #8A6410 | 5.37:1 |
| Blue text, links, button fills | #177DA9 | 4.62:1 |
| Small print (AI-assistance credit) | #6F6F6F | 4.81:1 |

The three failures fixed in this pass, for reference: KU Light Blue #27A9E1 as text or as a
button fill measured **2.68:1**; the site gold #C9921A as text on white measured **2.76:1**;
the credit line at #bbb measured **1.84:1**. #27A9E1 remains the brand value and is fine as a
decorative border, but never as text on white.

Also in place: a `.skip-link` on every page, `aria-current="page"` on the active nav item,
`a:focus-visible` outlines (#177DA9 on light, #FFCE01 on the navy nav) because the browser
default was nearly invisible against the dark bar, and a `prefers-reduced-motion` block that
disables the hover transforms and transitions.

Known and accepted: `.cv-table` has no `<th>` cells, so screen readers announce it as a table
without headers. The content is scannable enough that this was left alone; adding headers
would introduce a visible header row.

- Two golds are in use, deliberately. `--orange` (#C9921A) is the site-wide accent on light
  backgrounds: section rules, card borders, the lede bar. `--ku-gold` (#FFCE01) is used only
  in the hero, where anything gold sits on navy and the darker value fails contrast. Do not
  swap one for the other; pick by background, not by preference.
- Fonts are Roboto and Roboto Slab, loaded from Google Fonts, with `preconnect` hints ahead of
  the stylesheet link.
- Contact icons are **inline SVG**, not a webfont. The Font Awesome CDN stylesheet was removed;
  path data is taken from Font Awesome Free 6.5.0, whose icons are CC BY 4.0, and the
  attribution comment after `<body>` satisfies that licence. Keep the comment. To add an icon,
  copy the `<path d="...">` from the Font Awesome package rather than re-adding the CDN link.
- Every page has a `.skip-link` as the first focusable element, targeting `#main`. It is
  positioned off-screen until focused. The nav's current page carries
  `class="active" aria-current="page"`, so the active state is not conveyed by color alone.
- All `target="_blank"` links carry `rel="noopener noreferrer"`.
- Date stamps use one convention site-wide: "September 2026", in both the header institution
  line and the footer. Update all pages together.

## Heading structure

Section titles are real headings (`<h2>`, `<h3>`) carrying presentational classes. The
hierarchy is `h1` (name) → `h2` (document or section title) → `h3` (subsection), with no
skipped levels on any page.

An `h2, h3 { font: inherit; margin: 0; ... }` reset sits immediately after the global `*`
reset in every file. **Do not remove it.** Browsers apply their own font size, weight, and
vertical margins to headings; without the reset those leak through and the layout shifts. All
visual styling belongs in the classes (`.section-title`, `.stmt-section-title`, `.doc-title`,
`.subsection-title`, `.card-title`, `.blog-title`), never on the bare element.

## The blog feed

The "From the Blog" section of `index.html` pulls the three most recent posts from
*Boundary Conditions* at runtime. The inline script at the bottom of the file:

1. requests `https://public-api.wordpress.com/wp/v2/sites/rtackett1978.wordpress.com/posts`
   with `_fields=title,link,date,excerpt` (field limiting matters: the unfiltered response
   includes full post bodies and runs well over 100 KB),
2. falls back to the legacy `rest/v1.1` endpoint if that fails,
3. leaves the section `display: none` unless posts actually render.

That last point is deliberate. If WordPress changes its API or the request is blocked, the
page degrades to what it looked like before the feed existed rather than showing an empty
heading. It also means a broken feed is invisible, so check the section after any change.
No API key is involved; these endpoints are public.

## Structured data and SEO

`index.html` carries a JSON-LD `Person` block declaring name, job titles, employer, address,
`alumniOf`, ORCID as a formal `identifier`, `knowsAbout` topics, and `sameAs` links tying the
ORCID, Google Scholar, LinkedIn, and blog profiles to one individual. Validate changes with
Google's Rich Results Test before committing.

`index.html` also declares `<link rel="canonical" href="https://rtackett30.github.io/">`,
because the same page is served at both `/` and `/index.html` and search engines can otherwise
treat those as competing URLs.

`sitemap.xml` is maintained by hand. It lists the five HTML pages, using the canonical root
URL rather than `/index.html`, and omits `changefreq` and `priority` because Google ignores
both. The four PDFs are present as a commented-out block; uncomment to list them explicitly.
**Update the `lastmod` date on any page you change**, or the dates search engines use to
schedule recrawls will be wrong.

`robots.txt` allows all crawlers and points to the sitemap.

## Publication DOIs

Every published entry in `cv.html` and in the LaTeX CV carries a linked DOI except the 2005
*Phys. Rev. B* memory-effects paper, which has none in the ORCID record. DOIs came from an
ORCID BibTeX export run through Crossref; they were not constructed from citation patterns,
and none should be.

Adding a DOI to the LaTeX can push a reference past the margin. `tackettdoc.sty` loads `url`
with `\UrlBreaks` and sets `emergencystretch` to 2.5em to allow breaking inside the string.
Check the log for `Overfull` after adding references.

## Corrections applied 2026-09-04

Three publication entries were wrong in both the HTML and the PDF, and each was verified
against the publisher record before changing:

| Was | Is | Source |
|---|---|---|
| pyrochlore Bi2Ti2O4 | Bi2Ti2O**7** | Melot 2009, PRB 79, 224111 |
| La- and **Hy**-doped ... **ferro**magnetic | La- and **Dy**-doped ... **ferri**magnetic | AIP record, JAP 109, 07A510 |
| "Spin-ice state ...", PRB 77, **054408** | "**Ordered** spin-ice state ...", PRB 77, **020406** | APS record, Rapid Communication |

Note that ORCID's own record still reads "Ho-doped" for the second of these and holds a
duplicate of the Néel relaxation paper. Both need fixing in ORCID directly.

The SoFS start date reads **July 2025** throughout (`ai.html`, `admin.html`, and both PDFs).

## PDFs and their LaTeX source

The four PDFs are compiled from LaTeX, **not** exported from the HTML. The source is **not yet
committed to this repo**; it lives in `cv-latex-source.zip` alongside these files and should be
unpacked into a `latex/` folder here so the two stay together. Keeping it outside version
control is what turned a two-line CV edit into a full rebuild in September 2026.

- Engine is **XeLaTeX**, run twice so footer page numbers settle. LuaLaTeX will fail in
  environments without a populated `luaotfload` font cache.
- All four documents share `tackettdoc.sty`. **A change there reflows every one of them**, so
  recompile and visually check all four after touching it, not just the one being edited.
- The source folder must keep `tackettdoc.sty`, `headshot.jpg`, and `fonts/` as siblings of
  the `.tex` files.
- HTML and PDF versions are meant to stay in sync. Edit both, or note in the commit that one
  is pending.

## Known items

- The About-section photo on `index.html` is `Tackett_Mace.jpg`, referenced as a file. It was
  previously base64-inlined, which made the page 275 KB; it is now about 21 KB. Do not inline
  it again.
- The hero institution line (`.hero-institution`) sits on the navy hero background. It must
  stay at full opacity in KU Gold `#FFCE01`; the original `rgba(201,146,26,0.7)` at weight 300
  measured 3.42:1, below the 4.5:1 AA threshold. Do not reintroduce alpha on gold over navy.
- `.about-figure` needs `float: left` for the About text to wrap around the photo. The clearfix
  that makes the float work is `.about-body::after`. Removing either breaks the wrap.
- Two publication entries in the CV appear to have inherited typos and read identically in the
  HTML and the PDF: "pyrochlore Bi₂Ti₂O₄" (the Melot 2009 compound is Bi₂Ti₂O₇) and "La- and
  Hy-doped Co ferrite" (likely H-doped). Verify against the originals before correcting.
- The talk PDFs are LibreOffice exports of the source `.pptx` decks, which are not in this
  repo. The September deck's 6 hidden backup slides are correctly excluded from the export;
  re-exporting will keep excluding them.
- The start date for the SoFS appointment reads June 2025 in `ai.html`, `admin.html`, and both
  corresponding PDFs. Confirm whether June or July is correct; it appears in four places.

## Deploying

Commit to `main` and GitHub Pages redeploys within a minute or two. Two things that regularly
cause confusion:

- **Hard-refresh** (Ctrl+Shift+R / Cmd+Shift+R). An ordinary refresh serves the cached copy and
  a correct deployment can look like a failed one.
- `/` and `/index.html` are cached independently by some intermediaries. If one looks stale,
  check the other before concluding a file did not upload.

---

Site built with the assistance of Claude (Anthropic) via iterative conversational workflow in
Claude.ai.
