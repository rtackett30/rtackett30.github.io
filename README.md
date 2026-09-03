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
| `Tackett_Longway_Dec2024_Semiconductors.pdf` | Slides, Longway Planetarium, Dec 2024 (4.9 MB) |
| `Tackett_Longway_2023_Microscopy.pdf` | Slides, Longway Planetarium, 2023 (4.9 MB, recompressed) |
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
  `--accent` (#0D1F4C), `--orange` (#C9921A), `--ku-blue` (#27A9E1).
- Fonts are Roboto and Roboto Slab, loaded from Google Fonts. Font Awesome 6.5.0 supplies the
  contact icons, including `fa-google-scholar` and `fa-orcid`, both of which require 6.5.0 or
  later.

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

## PDFs and their LaTeX source

The four PDFs are compiled from LaTeX, **not** exported from the HTML. Source lives outside
this repo (see `cv-latex-source/`, which should be committed here so the two stay together).

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
- The 2023 microscopy PDF was 16 MB as exported. Embedded images were downsampled to 1400 px
  and re-encoded as JPEG at quality 72, bringing it to 4.9 MB with text left as vectors. Redo
  that step after any re-export. Its image sources are credited on-slide, several of them
  public domain or Creative Commons.
- The Longway semiconductors deck contains roughly 20 images, several of them sourced from
  third-party sites (Intel, CircuitDigest, and others) and appropriate for live classroom or
  public display. Publishing it as a permanent download is a different use. Review the image
  sourcing, or remove the `deck-link` line from that entry in `talks.html` to keep the
  description without the file. The PDF is also 4.9 MB, by far the largest file in the repo;
  the images resist further lossless compression.
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
