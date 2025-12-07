Purpose
-------
This file gives focused, actionable guidance for AI coding agents (Copilot-style) to be productive in this repository: a small static website composed of hand-written HTML pages, images, videos, and JSON configuration files.

Key points (big picture)
- The site is a static collection of HTML files in the repo root and `webpages/` with topical subfolders (`bjj/`, `striking/`, `takedowns/`, `test_pages/`). No build toolchain is present—edits are plain HTML/CSS/JS.
- Navigation and relationships rely on relative links (e.g. `index.html` → `webpages/map.html` uses `../` paths). Preserve relative paths when moving files.
- `webpages/map.html` uses an image (`images/map.png`) with `<map>` / `<area>` coordinates to link to many topic pages. Coordinates are critical and must match the image dimensions.
- `json/VisibilitySettings.json` and other `json/*.json` files are used as data/config — `VisibilitySettings.json` lists `HiddenElements` and an `Overrides` map keyed by numeric IDs.

Where to look (representative files)
- `index.html` — root entry and link structure.
- `webpages/map.html` — image map, area coordinates, and many examples of relative linking.
- `webpages/*.html` and folders like `webpages/bjj/`, `webpages/striking/`, `webpages/takedowns/` — content pages; many filenames contain spaces.
- `images/` and `videos/` — media referenced by pages.
- `json/VisibilitySettings.json` — configuration mapping (IDs → overrides).

Project-specific conventions and gotchas
- Filenames often contain spaces (e.g. `1 guard retention basics.html`). When editing or renaming, update every referring `href` (relative links will break otherwise).
- `<area>` coordinates: the correct format for an `<area shape="rect">` is `coords="x1,y1,x2,y2"` (left, top, right, bottom). There are inline comments in `webpages/map.html` that mix the notion of width/height vs. right/bottom — trust browser semantics (x2 = right coordinate, not width). Use an image editor or browser devtools to recompute coordinates.
- Many pages use inline styles and simple vanilla JS (no frameworks). Keep changes small and consistent with existing patterns unless you refactor across many files.
- Relative paths are the norm (e.g. `../images/`, `../index.html`). Use path resolution from the file being edited.

Local preview & quick commands
- Using Python's simple server (works in PowerShell):
```powershell
cd "c:\Users\arq-a\OneDrive\Obsidian Vault\projects\12_github_website\adfgx.github.io"
python -m http.server 8000
# then open http://localhost:8000 in a browser
```
- If Node is available, `npx serve` or `npx http-server` also work:
```powershell
npx serve . -l 8000
```

Editing guidelines (what to do and examples)
- To add/edit a map hotspot: open `webpages/map.html`, update the `<area>` tag coords and confirm visually against `images/map.png`.
  Example:
  ```html
  <area shape="rect" coords="455,200,725,260" href="../webpages/takedowns/1 wrestling basics made easy.html">
  ```
- To change visibility/config: edit `json/VisibilitySettings.json`. The file uses numeric string keys under `Overrides` — preserve the key format.
- When adding content pages, follow the folder pattern: put topic pages in `webpages/<topic>/` and link from `webpages/map.html` using `href="../webpages/<topic>/...html"`.

No automated tests / CI notes
- No test suite or build system found—treat changes as manual edits. If you add a build tool, document how to run it in this file.

PR and review suggestions for AI-generated patches
- Keep PRs small and focused: change a single page or a coherent set (e.g. update map areas only). Large refactors require human review of many relative links.
- When updating filenames, include an automated pass to update all `href`/`src` occurrences across the repo.
- Before proposing coordinate changes, include a screenshot or list of modified coords and the file(s) changed.

If unsure
- Ask the repo owner whether the site is published via GitHub Pages and which branch to push to. Default to opening a draft PR against `main`.
- When a change affects many files (bulk renames, move of `images/`), request confirmation first.

Feedback
- After reviewing these instructions, tell me which areas you want expanded (deploy, automated checks, or rename scripts) and I'll iterate.
