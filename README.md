# TJ Adebayo — Personal Site

A single-page, single-file personal website. Pixel-art TJ dribbles a football
left/right across a stadium pitch; each stop along the way reveals a section
of the CV (Kickoff → Match Experience → Training Ground → Highlight Reel →
Full Time). No build step, no dependencies — everything lives in `index.html`.

## Files

- `index.html` — the entire site (HTML + CSS + JS, self-contained). Fonts are
  loaded from Google Fonts via CDN (`Press Start 2P`, `Space Grotesk`,
  `JetBrains Mono`); everything else is inline.
- `profile.jpg` — graduation photo shown in the Classic View hero.

## Classic View

A "Classic View" button in the top bar switches to a standard scrollable
portfolio page (circular photo, name, links, then the CV sections stacked
vertically). Content is cloned at runtime from the game-view cards, so
there is a single source of truth — edit the zone cards and both views
update. The chosen view is remembered in localStorage.

## How it works

- `#world` is an absolutely-positioned layer 5000px wide holding the ground,
  floodlights, footprints, and the five content `.zone` sections. Pressing
  ←/→ (or A/D) scrolls `#world` via `translate3d`; the player sprite stays
  fixed on screen at ~32% viewport width.
- The player and ball are drawn on `<canvas>` elements from small pixel
  bitmaps (`FRAME_A` / `FRAME_B` string arrays near the top of the `<script>`
  block) — no image assets, so there's nothing to break if you move the file.
- Each `.zone` becomes `.active` (fades/slides in) when the player's world-X
  position enters its range; the corresponding floodlight lights up
  permanently once visited, and the bottom dot-track updates to match.
- Touch devices (`@media (pointer:coarse)`) get on-screen ◀ ▶ buttons
  automatically.

## Links

GitHub profile and project links are filled in (top bar, contact section,
and the three Highlight Reel cards).

Your phone number was intentionally left off the public page for privacy —
add it to the Kickoff card's `.row` list if you want it visible.

## Customizing

- **Colors** — all in the `:root { ... }` CSS variable block at the top of
  `<style>` (`--bg-night`, `--pitch`, `--amber`, etc.).
- **Copy/content** — each `<section class="zone" id="zone-N">` is plain HTML;
  edit the text directly.
- **Zone order/spacing** — the `ZONES` array near the top of the `<script>`
  block defines each zone's `x` position and width; the matching
  `.zone` element's inline `left` style and the `.floodlight` element's
  inline `left` style must be moved together if you change these.
- **Character look** — `FRAME_A` / `FRAME_B` are 10×14 character grids
  (`.` = transparent, other letters map to colors in the `PALETTE` object
  just above them). Edit characters to redesign the sprite; keep every row
  exactly 10 characters or the art will skew.
- **Move speed** — `SPEED` constant in the `<script>` block.

## Running locally

No build step needed. Either:

```bash
open index.html          # macOS, opens directly in default browser
# or
python3 -m http.server    # then visit http://localhost:8000
```

## Deploying

**GitHub Pages**
1. Create a repo, add `index.html` at the root.
2. Repo Settings → Pages → Deploy from branch → `main` / `root`.
3. Site is live at `https://<username>.github.io/<repo>/`.

**Netlify / Vercel**
- Drag-and-drop the folder containing `index.html` onto the Netlify deploy
  UI, or `vercel deploy` from this folder — both need zero configuration
  since there's no build step.

## Known placeholders / TODO

- [ ] Decide whether to add phone number back in
- [ ] Optional: add a "Download CV" button linking to an actual PDF
- [ ] THERMAL repo link is currently a private repo (404s publicly)
