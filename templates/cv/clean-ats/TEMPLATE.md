# Template: clean-ats

- **Type:** CV
- **Engine:** lualatex (also compiles cleanly with pdflatex/xelatex - no fontspec or icon-font dependency)
- **Page limit:** 2 page(s)
- **Fonts:** TeX Gyre Heros (Helvetica-alike sans-serif) - bundled with any standard TeX Live install via the `tgheros` package, no font files to manage
- **Class/packages:** `article` base class + `titlesec`, `enumitem`, `xcolor`, `ifthen`, `tabularx`, `parskip`, `microtype`, `hyperref` (all standard TeX Live packages)

## Compile command

    cd cv && lualatex -interaction=nonstopmode main_<company>_<role>.tex

## Style rules

- Single-column, no sidebars - reading order in the PDF text layer always matches visual order (good for ATS).
- Name centered, large bold, at the top; contact line centered directly below it, pipe-separated (`Address | Email | Phone | LinkedIn`).
- No icon fonts anywhere (this is the whole point of this template - see Known pitfalls). Contact details are plain text/hyperlinks only.
- Section headings (`\section{...}`): bold, accent-colored, underlined with a colored rule via `\titleformat`. Unnumbered (`\setcounter{secnumdepth}{-1}`).
- Accent color is one line to change: `\definecolor{accent}{HTML}{1F5C99}` near the top of the preamble.
- Experience/education entries use `\cventry{Title/Degree}{Date range}{Organization}{Location}` - title bold on the left, date right-aligned on the same line (via a borderless `tabularx`), organization (and location, if given) in italics on the line below. Pass `{}` as the 4th argument to omit location (used for Education entries, which don't carry a location in this profile).
- Bullets use `itemize` with tight spacing (`itemsep=1pt, topsep=2pt`) - do not add manual `\vspace` between bullets (same pitfall as the stock moderncv template: it produces uneven gaps).
- `\vspace{4pt}` after each `\cventry` block (inside the macro itself) gives breathing room between roles/degrees; this is baked into the `\cventry` macro, not something to add manually per entry.
- Core Competencies section: `itemize` list, one bullet per category, `\textbf{Category}: comma-separated items` - same authoring rules as the stock template (see `05-cv-templates.md`'s "Core Competencies / Skills Section" guidance, which still applies).
- Page budget and relevance-weighted cutting rules from `05-cv-templates.md` are unchanged - this template only changes the container, not the content-fitting strategy.

## Known pitfalls

- This template exists specifically to avoid a real bug in the stock moderncv "banking" style: under lualatex, `moderncviconsawesome.sty`'s `\faMobile*`/`\faEnvelope[regular]` icons sometimes render as literal fallback text (`MOBILE-ALT`, `Envelope`) instead of glyphs. This template has zero icon-font dependency, so that failure mode cannot occur here - contact details are plain text and hyperlinks only.
- `\cventry`'s 4th argument (location) must be passed as an empty group `{}`, not omitted, or LaTeX will complain about a missing argument. Education entries in this profile have no location, so they're always called as `\cventry{...}{...}{...}{}`.
- `tabularx` requires the `X` column to be the first column for the flexible-width/right-aligned-date layout to behave (`@{}X r@{}`) - don't reorder the columns in `\cventry`.
