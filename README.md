# APEX Lab Website

Accessibility and Privacy Enhancing EXperience (APEX) Lab — University of Texas at San Antonio.

Static site (no build step). Built with HTML + Bootstrap 5 (loaded from a CDN) + one custom
stylesheet. Edit a file, push to GitHub, done.

## Tech stack

| Layer          | Technology                                   | Notes                                                        |
|----------------|----------------------------------------------|--------------------------------------------------------------|
| Markup         | HTML5 (semantic)                             | Plain .html files, one per page — no templates, no build step |
| CSS framework  | [Bootstrap 5.3](https://getbootstrap.com)    | Grid, carousel, responsive utilities; loaded from CDN         |
| Custom styles  | `css/style.css`                              | Single stylesheet; all settings are CSS variables in `:root`  |
| JavaScript     | Vanilla JS (`js/main.js`)                    | ~50 lines: footer year, lightbox init, sidebar scroll-highlight |
| Lightbox       | [GLightbox 3.3](https://biati-digital.github.io/glightbox/) | Gallery full-size image viewer; no jQuery required |
| Fonts          | [Inter](https://fonts.google.com/specimen/Inter) + [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) | Body + headings, via Google Fonts |

There is intentionally **no** build tooling (no npm, no bundler, no preprocessor): open any
HTML file in a browser to preview, edit with any text editor, push to deploy.

## Project structure

```
index.html          Home (banner, carousel, intro, recent news)
people.html         Team members (with section sidebar)
research.html       Research areas (with section sidebar)
publications.html   Publication lists
gallery.html        Photo gallery with lightbox
css/style.css       ALL custom styles — settings at the top
js/main.js          Tiny script (footer year, lightbox, sidebar highlight)
images/             All photos, figures, and the banner
favicons/           Per-page browser tab icons
```

## Site-wide controls (top of css/style.css)

All in the `:root { ... }` block:

| Variable            | Controls                                              |
|---------------------|-------------------------------------------------------|
| `--brand-*` colors  | Theme colors (see accessibility note below)           |
| `--page-max-width`  | How wide the site can grow (raise to widen)           |
| `--page-padding`    | Space at the left/right screen edges                  |
| `--space`           | Master vertical spacing — lower = more compact        |
| `--carousel-height` | Homepage banner carousel height                       |
| `--thumb-height`    | Gallery thumbnail height                              |
| `--headshot-size`   | People page photo size                                |

## Common updates (each takes ~2 minutes)

Every editable spot is marked with a `<!-- ============ -->` comment in the HTML.

**Add a news item** → `index.html`, find `RECENT NEWS`. Copy one
`<div class="col-lg-4 col-md-6">` block, paste it as the FIRST card (newest first), edit the
date, title, link, image, and text. If the image is a screenshot or figure with text on it,
add `class="fit-contain"` to the `<img>` so it isn't cropped.

**Add a person** → `people.html`. Copy one `<div class="person">` block into the right
section. Roughly square photos work best (they display at 220×220, cropped from the top).
If the photo links to the person's website, wrap the `<img>` in an `<a>` — both forms are
already styled.

**Add a publication** → `publications.html`. Copy one `<li>` block, paste it at the TOP of
the right list (newest first).

**Add a research project** → `research.html`. Copy one
`<section class="research-block">`, give it a unique `id`, then add a matching link in the
sidebar list (`class="sub"` for project-level links). The sidebar highlight follows scrolling
automatically — no extra setup.

**Add a gallery photo** → put the image in `images/`, then in `gallery.html` copy one
`<figure>` block and update `href`, `src`, `alt`, and the caption.

**Add a carousel slide** → `index.html`, copy one `<div class="carousel-item">` block.
Use landscape (wider-than-tall) photos; portrait photos get heavily cropped.

**Add a new section to a sidebar page** → add the `<h2 class="section-title" id="...">`
in the content column and a matching `<a href="#...">` in that page's sidebar list.

**Change the banner** → replace `images/cover-1.png` (keep it wide, roughly 3.5:1).

**Add a new page** → copy `publications.html` (simplest layout), update the `<title>`,
favicon link, and content. Add the nav link to the navbar `<ul>` on EVERY page, and move
`class="active"` + `aria-current="page"` to the new page's own link in its file.

## Accessibility checklist (please keep this — it's our lab's own site)

The site currently meets these standards. When adding content, keep them true:

**Every image gets real alt text.** Describe what's in the photo ("Abhinaya Guduru
presenting a poster"), not "image" or "photo1". For purely decorative images use `alt=""`
so screen readers skip them — but on this site almost nothing is decorative.

**Never write "click here" links.** Screen reader users browse pages as a list of links,
out of context. Put the meaning in the link text:
- Bad: `Find the paper <a href="...">here</a>`
- Good: `<a href="...">Read the paper: Beyond Accessibility (ASSETS 2025)</a>`

**Don't use justified text** (`text-align: justify`). It creates uneven word spacing that
hurts readers with dyslexia and low vision. Left-aligned is the accessible default.


**Keep the heading order.** One `<h1>` per page (the banner), `<h2>` for sections,
`<h3>` for items inside sections. Don't skip levels or pick headings for their size —
screen reader users navigate by heading structure.

**Keep the built-in features intact when copying blocks:** the skip link at the top of
`<body>`, `aria-label` on the two navs, `aria-current` on the active nav link, and the
`alt`/`figcaption` pairs in the gallery.

## Notes

- Keep photos under ~1920px on the long edge before uploading (large phone photos slow
  the site down).
- Bootstrap and the lightbox load from cdn.jsdelivr.net — no local copies to update.
- The footer is duplicated in each page; if contact info changes, update all five files
  (search for "Contact Information").