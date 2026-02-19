# Copilot Instructions for this Repository

## Big picture
- This repo is a static showcase of AI-generated experiments; there is no build step, backend, or package manager.
- `index.html` is the catalog entrypoint and the only cross-page integration point.
- Each experiment is a standalone HTML document (for example `motherload-copilot.html`, `stickrpg-opus-4-6.html`, `minecraft-opus-4.6.html`) with inline CSS and inline JS.
- Architecture is intentionally “many independent pages + one index table”, so keep pages loosely coupled and avoid introducing shared runtime dependencies.

## Source of truth and data flow
- `index.html` table rows are the source of discoverability; adding/removing an experiment requires updating the `<tbody>` row list.
- Filtering reads `row.cells[0]` and `data-project`/`data-prompt`; keep these attributes populated on every row.
- Sorting by Created Date uses `td[data-date]` ISO values (`YYYY-MM-DD`), not the human-readable text.
- Theme state is persisted in `localStorage` key `theme`; preserve `light`/`dark` values if changing theme behavior.

## File and naming conventions
- Root-level experiment files follow descriptive, model/version-oriented names such as `cef-sonnet-4.6.html` or `fun-game-opus-4.6.html`.
- Keep new experiments as single self-contained `.html` files unless the user explicitly asks for multi-file refactors.
- In experiment pages, common structure is: full-screen layout, `<canvas>` or app container, mobile-friendly controls, and a `requestAnimationFrame` game/render loop.
- Preserve touch + mouse + keyboard support patterns seen in `stickrpg-opus-4-6.html` and `motherload-copilot.html`.

## External integrations
- Some pages depend on browser-loaded CDNs (not npm), e.g. import maps for Three.js in `minecraft-opus-4.6.html` and `transporter-bridge-opus-4.6.html`.
- When editing those files, keep `type="module"` and import-map URLs consistent; do not add build tooling just to manage dependencies.
- Optional chat provenance links are stored in `index.html` "Chat Link" column and may be blank (`—`) for some entries.

## Developer workflow
- Local run: open `index.html` directly, or serve statically (example: `python3 -m http.server` from repo root).
- Manual verification is primary: check index filtering, sorting, theme toggle, and links after edits.
- For experiment page edits, validate in browser at desktop and narrow/mobile viewport because many pages use `100dvh`, touch handlers, and fixed overlays.

## Change guidelines for agents
- Make focused edits in the specific page requested; avoid broad restyling across unrelated experiment files.
- Treat one-shot experiment HTML files as immutable snapshots; do not edit them except to add a provenance comment on the first line when explicitly requested.
- If adding an experiment page, also add its row in `index.html` with consistent `data-*` metadata and date format.
- When adding a new experiment HTML file, add a first-line provenance comment in the format `<!-- Made with AI: <chat-link> -->` if a chat link is available.
- Do not convert this repo into a framework app or add lint/test infrastructure unless explicitly requested.
- Respect that `robots.txt` currently disallows crawling (`Disallow: /`); do not change crawler behavior unless asked.
