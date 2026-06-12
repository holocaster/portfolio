# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static personal portfolio (one page) for Paulo Roberto Sousa Pereira, in Portuguese (pt-BR). No framework, no build step. Plain HTML/CSS/JS served as static files by nginx on the owner's VPS. Keep it simple by design.

## Commands

- Preview locally: `python3 -m http.server 8000` then open `http://localhost:8000`
- No build, lint, or test step exists. Do not add one without being asked.
- Deploy: static files served by nginx on the owner's VPS (rsync to `/var/www/portfolio`). Deploy steps are managed outside this repo.

## Architecture

Three files do everything:
- `index.html` - all content: hero, project grid, footer/contact.
- `assets/css/styles.css` - the entire design. Tokens (colors, fonts, layout) live in `:root` at the top.
- `assets/js/main.js` - intentionally tiny (just the footer year). Resist adding JS.

Screenshots and the favicon live in `assets/img/`.

## Key conventions

- **Portuguese with correct accents** in all visible text (aplicações, Sênior, currículo). The "no emojis" rule does NOT mean stripping diacritics — missing accents read as sloppy to recruiters.
- **Adding a project**: copy a whole `<li class="card">...</li>` block in `index.html` and edit `data-accent` (`amber` | `teal` | `slate`), the index number, title, description, tags, and `href`. The `data-accent` value selects the thumbnail gradient defined in CSS.
- **Project thumbnails**: default to a gradient + monogram. A real screenshot is opt-in via an inline `style="background-image:url('assets/img/x.jpg')"` on `.card__thumb` (see README).
- **Cache-busting on every CSS/JS edit (MANDATORY)**: nginx serves assets with `Cache-Control: immutable, expires 1y`, so browsers will NOT refetch a changed file unless its URL changes. The filenames are NOT hashed. Therefore, whenever you edit `assets/css/styles.css` or `assets/js/main.js`, you MUST bump the `?v=N` query param on its `<link>`/`<script>` tag in `index.html` (e.g. `styles.css?v=1` -> `?v=2`). Bump each file independently (only change the version of the file you edited). Forgetting this means users stay on the stale version for up to a year.
- **No public email**: contact routes through the LinkedIn link only. Do not add a plaintext `mailto:` (spam scraping) unless explicitly asked.
- Design direction is deliberate editorial minimalism (warm paper, ink, single terracotta accent; Fraunces + DM Sans + JetBrains Mono). Keep changes within this aesthetic.

See `CONTEXT.md` for the project glossary (Projeto, Currículo, etc.).
