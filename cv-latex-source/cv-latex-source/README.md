# LaTeX source — Tackett professional documents

Rebuilt 2026-09-03. Keep this folder together; the documents rely on
`tackettdoc.sty`, `headshot.jpg`, and the `fonts/` directory being siblings.

## Contents

| File | Output |
|---|---|
| `Tackett_CV_Redesigned.tex` | Curriculum Vitae (8 pp.) |
| `Teaching_Philosophy_Tackett.tex` | Teaching Philosophy (3 pp.) |
| `Admin_Philosophy_Tackett.tex` | Administrative Philosophy (3 pp.) |
| `AI_Statement_Tackett.tex` | AI Personal Statement (3 pp.) |
| `tackettdoc.sty` | Shared style: palette, fonts, headings, footer |
| `fonts/` | Roboto 300/400/500/700 TTFs (referenced by `tackettdoc.sty`) |
| `headshot.jpg` | CV header photo |

## Building

XeLaTeX, run twice so the page count in the footer settles:

```
xelatex Tackett_CV_Redesigned.tex
xelatex Tackett_CV_Redesigned.tex
```

LuaLaTeX will not work in every environment — it needs a populated
luaotfload cache to find the Roboto files. XeLaTeX has no such dependency.

## Routine updates

- **Date stamp:** `\setupdated{...}` in each document preamble; the closing
  block on the statements takes its term from `\signatureblock{Fall 2026}`.
- **New publication or talk:** add an `\item` inside the relevant `reflist`.
- **New position, award, course, or service role:**
  `\cventry{title}{subtitle}{date}` — title left and bold, subtitle italic
  beneath it, date flush right.
- **Palette and rule weights:** the `\definecolor` block at the top of
  `tackettdoc.sty`. `accent` (#2E4057) drives every heading and rule.

## Conventions carried over

- American English throughout.
- No em dashes. One survives in section I of the Administrative Philosophy
  because it is present in the original text; remove it when that prose is
  next revised.
- Chemical formulas are set in math mode (`Fe$_3$O$_4$`).

## Known items to verify

Both predate this rebuild and appear identically in the previous PDF and in
`cv.html`, so they were transcribed as written:

- "pyrochlore Bi$_2$Ti$_2$O$_4$" — the Melot (2009) compound is Bi2Ti2O7.
- "La- and Hy-doped Co ferrite" — likely H-doped.
