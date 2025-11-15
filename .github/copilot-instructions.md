<!-- Copilot / AI agent instructions for the Halaji-Menu repo -->

# Copilot Instructions — Halaji-Menu

Purpose: give an AI coding agent the minimal, actionable knowledge to be productive in this static flipbook menu project.

1. Big picture

- This is a static website (no backend) that implements a magazine/flipbook UI for restaurant menus.
- Key areas:
  - Root HTML pages: `index.html`, `restaurant.html`, `cafe.html` — entry points used in the site.
  - Flipbook assets: `flipbook/` — contains `css/`, `js/`, `lib/`, `extras/`, and `files/` (images/backgrounds).
  - Content folders: `Cafe/`, `Homepage/`, `NewData/`, `Restaurant/` — likely contain page-specific assets and content.

2. How the pieces fit

- `index.html` (and other top-level HTML files) load CSS from `flipbook/css/` and JS from `flipbook/js/`.
- Core flipbook logic lives in `flipbook/js/*` (e.g. `magazine.js`, `core*.js`, `magazineSINGLE.js`).
- Third-party libraries and fallbacks are kept under `flipbook/lib/` and `flipbook/extras/` (e.g. `turn.js`, `zoom.js`, jQuery builds).
- Styling variants: multiple `magazine*.css` files indicate theme/variant styles — choose the matching JS (`core*.js`) when changing behavior.

3. Developer workflows (what works locally)

- No build scripts found — serve files with a static server to test pages. Examples:
  - With Python: `python -m http.server 8000` (run in repo root) then open `http://localhost:8000/index.html`.
  - With VS Code: use Live Server extension and open `index.html`.
- There are no automated tests or bundlers; changes to `.js`/`.css` are reflected on reload.

4. Conventions & patterns to follow

- Naming pattern: `core.js`, `core1.js` ... `core5.js` and `magazine*.js`/`magazine*_single.js` indicate parallel variants. When editing behavior, update the corresponding pair (JS + CSS) for that magazine variant.
- `*_single.js` and `*_single.css` are used for single-page or single-magazine views — prefer editing both paired files.
- Minified libs live alongside sources (`turn.min.js`, `zoom.min.js`). Prefer editing the non-minified versions if present (`turn.js`, `zoom.js`) and keep minified files in sync when committing.

5. Integration points & external dependencies

- jQuery is a dependency (multiple copies/version variants under `flipbook/extras/`), so be careful when changing how scripts are loaded — use the versions the HTML pages reference.
- `flipbook/lib/turn*.js` and `zoom*.js` provide flip/zoom behaviors: changes to flip logic often involve these files and `flipbook/js/magazine.js`.
- `flipbook/files/backgrounds/` and `flipbook/pics/` contain image assets referenced by HTML/CSS.

6. Files to inspect for context when you edit

- `index.html` — example entry point and script ordering.
- `flipbook/js/magazine.js` and `flipbook/js/core.js` (and other `core*.js`) — main flipbook logic and variant behaviors.
- `flipbook/css/magazine.css` and `flipbook/css/style.css` — primary styles; variants live in `magazine1.css` ...
- `flipbook/lib/turn.js` (and `turn.min.js`) — flipbook engine; edit with caution.

7. Safe edit checklist for JS/CSS changes

- Confirm which HTML entry page (`index.html` or `restaurant.html`) is used by the change.
- Update paired files for a variant (both `core*.js` and `magazine*.css` when relevant).
- Test locally via a static server and verify the flip/zoom behaviors and responsive layout.
- If you modify a library file, keep a backup copy and prefer adding changes in a new custom file instead of editing third-party code in-place when possible.

8. If you need to add build tooling

- Prefer minimal additions (e.g., a simple `package.json` with dev server) and document commands in the repo root README.

9. What not to assume

- There is no Node.js build system or tests present — do not add changes that depend on an unlisted toolchain without confirming.

If anything is missing or you'd like more detail about a specific area (for example: where menu content is authored, or which HTML pages are canonical), tell me which files you want linked and I'll expand this file.
