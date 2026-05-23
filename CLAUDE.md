# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```sh
npm run dev      # dev server at localhost:4321
npm run build    # production build to ./dist/
npm run preview  # preview production build locally
```

No test runner or linter is configured.

## Architecture

Personal website for Carlos Miguel Guevara, built with Astro 5. Content is in Spanish.

**Page pattern** — every page follows the same structure:
1. Import `Layout` and `Menu`
2. Wrap content in `<Layout>`
3. Render `<Menu currentPath="/route" />` — the `currentPath` prop drives the active nav state

**`src/layouts/Layout.astro`** — the HTML shell. Loads Bootstrap 5 via CDN (not the npm package), Roboto from Google Fonts, and includes the Google Analytics snippet (G-SD2QESDRRX). Global styles (body font, `.bold`, `.title`, `.content`, `.entry`) live here.

**`src/components/Menu.astro`** — shared header with profile photo (`src/assets/carlos.jpg`) and horizontal nav. Nav items are defined as a static array inside the component; add new top-level pages there.

**`src/pages/`** — file-based routing. One `.astro` file per route. Pages with no dynamic data are pure static HTML with inline content.

**`public/tools/`** — standalone static tools (e.g. `screensize`) served as-is, outside the Astro component system.

## Notes

- Bootstrap is loaded from CDN in the layout, but `bootstrap` is also listed as an npm dependency — it is not currently imported anywhere in the JS/CSS pipeline.
- The `src/pages/blog.astro` page has a commented-out entry block — the blog section is not yet implemented.
- Some pages (`proyectos.astro`, `blog.astro`) import a `Welcome` component that does not exist; remove those imports if editing those files to avoid build warnings.
