# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static personal portfolio website for Ryan A. Diaz (ryanadiaz.com). No build system, package manager, or server-side code — everything is vanilla HTML/CSS/JS served as static files.

## Architecture

### Single-page layout (`index.html`)
One HTML file with anchor-linked sections: `#about`, `#experience`, `#portfolio`, `#social`, `#contact`. The fixed navbar uses `js-scroll-trigger` class for smooth scrolling and Bootstrap scrollspy for active state highlighting.

### CSS
- `scss/creative.scss` — main SCSS entry point that imports all partials (`_variables`, `_mixins`, `_global`, `_navbar`, `_masthead`, `_services`, `_portfolio`, `_bootstrap-overrides`)
- `css/creative.css` / `css/creative.min.css` — compiled output (committed to repo)
- `css/main.css` — small hand-written overrides added on top of creative.css

**Primary brand color:** `#F05F40` (defined as `$primary` in `scss/_variables.scss`)

### JavaScript
- `js/creative.js` — source JS handling smooth scroll, navbar collapse, scrollspy, ScrollReveal animations, and Magnific Popup initialization
- `js/creative.min.js` — minified version; this is what `index.html` loads

### Vendor libraries (all local copies in `vendor/`)
- Bootstrap 4.1 (also loaded via CDN for CSS)
- jQuery + jQuery Easing
- ScrollReveal — used for `.sr-icons`, `.sr-button`, `.sr-contact` entrance animations
- Magnific Popup — configured but portfolio links open directly in new tabs (`target="_blank"`), not as lightbox popups

### Analytics (in `<head>` of `index.html`)
- Google Analytics (UA-147235487-1)
- Inspectlet (wid: 853360445)
- Hubalz

## Making Changes

### Styles
Edit SCSS partials in `scss/`, then compile to regenerate `css/creative.css`. There is no build script in the repo — compile manually with the Sass CLI:
```
sass scss/creative.scss css/creative.css
sass --style=compressed scss/creative.scss css/creative.min.css
```
For minor tweaks, editing `css/creative.css` directly (and keeping it in sync with SCSS) is also acceptable.

### Content
All content is inline in `index.html`. Portfolio items are `<div class="col-lg-4 col-sm-6 gray-border">` blocks inside `.popup-gallery`. Each item has a `.portfolio-box-caption` overlay with `.project-category`, `.project-name`, and `.project-description`.

### Images
Portfolio thumbnails live in `img/` (flat, named by project). There is also an `img/portfolio/` directory with `fullsize/` and `thumbnails/` subdirectories that appear unused by the current `index.html`.

## Deployment
Static files — deploy by pushing to GitHub and syncing to a web host. DNS configuration screenshots are stored as `aws-dns-backup.png` and `aws-dns-backup_2.png` at the repo root for reference.
