# Copilot Instructions — Moneytor

**Project type:** Single-file static marketing/site (SPA-like) — `Moneytor.html`

## Quick summary
- Single HTML file containing markup, styles, and client-side JS. No build system, no server code, no tests. ✅
- Uses CDN-hosted assets (FontAwesome, Google Fonts). CSS variables for colors and theme live in `:root` in the head.

## How to run locally 🔧
- Open `Moneytor.html` directly in a browser for quick checks (some features require an HTTP context).
- Recommended local dev servers:
  - `python -m http.server 8000` (serve repo root, then open http://localhost:8000/Moneytor.html)
  - `npx http-server -p 8080` or use VS Code Live Server extension

## What to change and where (concise examples) ✏️
- The single source of truth is `Moneytor.html`:
  - Layout & theme: large inline `<style>` near top. Keep color palette in `:root` (e.g., `--primary`, `--accent-blue`).
  - Animations: classes `.animate-in`, `.animate-left`, `.animate-right` — IntersectionObserver adds `.active` to trigger transitions.
  - Mobile navigation: `#mobileMenuBtn` toggles `#navLinks.active` via `navLinks.classList.toggle('active')`.
  - Dashboard mockup: bar heights are set inline on `.chart-bar` elements (e.g., `<div class="chart-bar" style="height: 70%"></div>`). If converting to dynamic data, update styles or use JS to animate heights.
  - Contact form is static: `<form>` has no `action` or backend hookup. Any integration should add a POST endpoint and update the form to `fetch()` or `action` accordingly.

## Conventions & patterns to preserve
- Theme variables: Use `:root` variables for colors and radii. When adding styles, prefer reusing `--primary`, `--text-dark` etc.
- Responsive breakpoints are established at 992px, 768px, and 576px — follow those when adding layout changes.
- Small, semantic class names (e.g., `.hero`, `.kpi-item`, `.contact-form`) — keep names descriptive and flat rather than introducing a complex BEM hierarchy.
- JS is small and imperative, manipulating the DOM directly at bottom of file — when refactoring to multiple files, preserve the initialization order (menu listeners, IntersectionObserver, onload animations).

## Tests, builds, and CI
- No existing test or build commands found. If adding automation:
  - Add a lightweight `npm` setup (eslint, stylelint, and a test runner) and a simple `package.json` script for `start` that runs a static server.
  - For visual checks, rely on browser DevTools; for accessibility, consider adding an a11y tool (axe) as a dev-only check.

## Integration & external dependencies
- External dependencies are CDN references in the head:
  - Font Awesome (icons)
  - Google Fonts (`Inter`)
- There are no API keys or backend integrations present. Any new integration should include a README snippet describing environment variables and endpoints.

## Notable limitations & gotchas ⚠️
- The contact form is client-side only; _do not_ assume it submits anywhere.
- Accessibility: interactive elements (mobile menu button, links) lack ARIA attributes—be explicit about adding `aria-expanded`, `aria-label` when introducing behavior changes.
- Single-file approach: when splitting into modules, keep script load order and IntersectionObserver registration consistent to avoid race conditions.

## PR guidance for AI authors
- Keep changes small and focused. When editing styles, update `:root` first if introducing new colors.
- When adding JS features, place initialization at the bottom and keep observers and event registration deterministic (guard selectors with `if` checks).
- For new assets, prefer adding a top-level `assets/` folder and reference it from `Moneytor.html`.

---
If anything important is missing or you want sections expanded (for example, an example `package.json`, CI steps, or an automated visual test plan), tell me which part to expand and I’ll update this file. ✅
