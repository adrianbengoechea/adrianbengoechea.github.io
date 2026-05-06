# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Adrian Beng, built as a single-page application with section-based navigation and custom animations.

## Tech Stack

- **Astro 5.x** — static site generator (no integrations configured)
- **TypeScript** — strict mode (`astro/tsconfigs/strict`)
- **Vanilla CSS** — custom properties for design tokens, no preprocessor or framework
- **Vanilla JS** — client-side interactions (no frontend framework)
- **Icons**: Font Awesome Free (`@fortawesome/fontawesome-free`, imported in `global.css`)
- **Fonts**: Inter (body), Space Grotesk (headings), SN Pro (buttons) via Google Fonts

## Commands

```
npm run dev        # Dev server at localhost:4321
npm run build      # Production build to ./dist/
npm run preview    # Preview production build
```

No test suite is configured.

## Architecture

Single page (`src/pages/index.astro`) composing:

```
BaseLayout.astro
├── IntroAnimation.astro      # Intro/loading screen (fixed, z-index: 3)
├── FloatingShapes.astro      # Animated background shapes (z-index: -1)
└── MainFlow.astro            # Two-column layout container (max-width: 1300px)
    ├── Aside.astro           # Sticky sidebar (48% width, height: 100vh)
    │   ├── aside/MainTitle.astro
    │   ├── aside/Navigation.astro
    │   └── aside/Socials.astro
    └── Content.astro         # Scrollable right column
        ├── content/About.astro
        ├── content/Experience.astro
        ├── content/Projects.astro
        ├── content/Contact.astro
        └── content/Footer.astro
```

`Aside` becomes `position: relative` (stacked) on viewports ≤ 991px.

## Key Conventions

- **Design tokens** live in `src/styles/global.css` as CSS custom properties (`--bg`, `--fg`, `--accent`, `--light`, `--text`, `--font-primary`, etc.)
- **Section reveal**: all `<section>` elements are hidden (`opacity: 0; visibility: hidden`) until `body.intro-finished` is added by `IntroAnimation.astro` after the typing animation completes
- **Navigation anchors**: each content section contains `<a name="sectionName" class="anchor">` (offset −100px); nav `<li>` elements use `data-section="sectionName"` for scroll-spy
- **Scoped styles** in each `.astro` component's `<style>` block; inline styles used for one-off adjustments
- **Client JS** wrapped in `DOMContentLoaded` listeners; scroll-spy uses `requestAnimationFrame` throttle
- **Z-index layering**: background effects (−1), main content (default), intro (3), nav (20)
- **Git commits**: lowercase, feature-descriptive messages

## Adding Content

**Projects**: Add entries to the `projects.list` array in `src/components/content/Projects.astro`. Thumbnails go in `src/assets/projects/` and are imported at the top of that file (Astro processes them for optimized output).

**Experience**: Edit the `<ol>` in `src/components/content/Experience.astro` directly — no data abstraction layer.
