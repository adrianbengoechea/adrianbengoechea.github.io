# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Adrian Beng, built as a single-page application with section-based navigation and custom animations.

## Tech Stack

- **Astro 5.x** — static site generator (no integrations configured)
- **TypeScript** — strict mode (`astro/tsconfigs/strict`)
- **Vanilla CSS** — custom properties for design tokens, no preprocessor or framework
- **Vanilla JS** — client-side interactions (no frontend framework)
- **Fonts**: Inter (body), Montserrat (headings), SN Pro (buttons) via Google Fonts

## Commands

```
npm run dev        # Dev server at localhost:4321
npm run build      # Production build to ./dist/
npm run preview    # Preview production build
```

No test suite is configured.

## Architecture

Single page (`src/pages/index.astro`) using `BaseLayout.astro` with section components:

```
BaseLayout.astro
├── Intro.astro          # Intro/loading screen (fixed, z-index: 3)
├── FloatingShapes.astro # Animated background shapes (z-index: -1)
├── Header.astro         # Floating magnetic menu button (fixed, z-index: 20)
└── <main>
    ├── Hero.astro
    ├── About.astro
    ├── Projects.astro
    └── Contact.astro
```

## Key Conventions

- **Design tokens** live in `src/styles/global.css` as CSS custom properties (`--bg`, `--fg`, `--accent`, `--light`, `--font-primary`, etc.)
- **Sections default to hidden** (`opacity: 0; visibility: hidden`) for reveal animations
- **Scoped styles** in each `.astro` component's `<style>` block; inline styles used for one-off adjustments
- **Client JS** wrapped in `DOMContentLoaded` listeners; animations use `requestAnimationFrame`
- **Z-index layering**: background effects (-1), main content (default), intro (3), header/nav (20)
- **Git commits**: lowercase, feature-descriptive messages
