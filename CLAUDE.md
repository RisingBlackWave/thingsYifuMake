# CLAUDE.md — Claude Code Setup Guide

## Project

thingsYifuMake — personal portfolio website for Yifu, a PhD researcher / designer / maker at UCL.

A dark-canvas orbital constellation where project dots orbit a reactive center blob. Ambient music plays on entry. Interaction follows a low-to-high detail progression: watch → hover (whisper) → click (preview) → enter (full page).

## Key Files

- `DESIGN.md` — **Read this first.** All design decisions, visual direction, build priorities, and interaction specs live here. This is the source of truth.
- `projects.json` — All project content. 23 entries across 5 modes (Designed, Researched, Built, Taught, Talked). Edit content here, not in HTML.
- `index.html` — The site engine. HTML + CSS + JS in a single file. Loads `projects.json` via fetch. Currently implements v3 (flat constellation). Needs to be rebuilt for v4 (orbital).
- `README.md` — Deployment guide (GitHub, Netlify, domain, image prep).
- `assets/projects/[slug]/` — Per-project image/video folders. Empty until real photography is added. Each can hold `preview.jpg` (440×260), `cover.jpg` (1400×600), `loop.mp4`.
- `assets/audio/` — Will hold `ambient.mp3` and `whispers/[slug].mp3`. Not yet created.

## Tech Stack

Pure HTML + CSS + JS. No framework, no build step, no dependencies. Canvas 2D for background rendering (stars, rings, blob). DOM elements for dots, preview cards, project pages. Google Fonts loaded via CDN (Cormorant Garamond, DM Mono).

Static site — runs from any web server or `python3 -m http.server`. Deploys to Netlify or GitHub Pages.

## Architecture Patterns

- **Data-driven:** All project content in `projects.json`. The JS reads this, generates gradients, builds DOM nodes. To add a project: add a JSON entry + create an asset folder.
- **Single-file engine:** All CSS and JS are inline in `index.html`. This is intentional — keeps deployment dead simple (no bundler). Don't split unless there's a strong reason.
- **Null-fallback assets:** Every project has `previewImage`, `coverImage`, `previewVideo` fields. `null` = generated gradient. Set a path = real asset loads with the gradient as fallback behind it.
- **Animation loop:** `requestAnimationFrame` drives dot positions, canvas redraw, and breathing effects. Everything time-dependent uses a single `animT` counter incremented per frame.

## Colour Palette

```
--designed:   #E8C17A  (warm amber)
--researched: #7AB8E8  (cool blue)
--built:      #7AE8C1  (teal/mint)
--taught:     #E87A7A  (coral red)
--talked:     #C17AE8  (violet)
--bg:         #07070A  (near-black)
--text:       #EDE9E2  (warm white)
```

These are defined as CSS custom properties in `:root` and also in the JS `COLORS` object.

## Current State (v3 — flat constellation)

What works: 23 dots with sinusoidal drift, canvas constellation lines between mode groups, auto-surfacing preview cards with pulse ring, mode filter with scatter/regroup, hover preview cards with viewport-edge flip, full project page with back navigation, custom cursor, grain overlay, staggered entrance animation.

What's next: Rebuild to v4 orbital model (see DESIGN.md Phase 1). The v3 code is a working reference for DOM structure, preview card building, project page rendering, and filter logic — these parts carry forward. The positioning math (BASE_POS, sinusoidal drift, constellation line drawing) gets replaced by orbital ring math.

## Build Priorities (from DESIGN.md)

**Phase 1 — Orbital prototype:**
Elliptical ring paths (2–3 rings, different speeds/tilts), dots riding rings, center blob with perlin-noise displacement + cursor reactivity, elastic dot bloom on hover, dotted leader line extending to whispered title.

**Phase 2 — Cursor-lens + sound:**
Large (~80-100px) `mix-blend-mode: difference` invert-lens cursor. On dot hover, the cursor fills with B&W halftone preview image (clipped to circle, moves with mouse). Ambient music with autoplay gate (NIN Ghosts V: Together vibe — warm drones). ElevenLabs whisper audio — one evocative sentence per project, 5 voices (one per mode), spatial panning via Web Audio API.

**Phase 3 — Preview + pages:**
Project page layout inspired by Marco Da Re (text/pic/video structure). B&W halftone image treatment. Progressive reveal. Project page ambient background.

**Phase 4 — Mobile (gyroscope exploration):**
`DeviceOrientationEvent` to pan across constellation by tilting phone. Constellation renders larger than viewport. Tap-to-reveal circle animation with image + title + whisper. Fallback: touch-drag panning. iOS permission prompt for motion access.

**Phase 5 — List view (backup):**
Flat text list referencing Formafantasma `/works`. System fonts only (Times New Roman + Arial). Row per project: index, title, mode color tag, year. Click expands description. View toggle (constellation ↔ list) in top-right, no page reload, URL hash (`#list` / `#constellation`). On mobile, list is always one tap from gyroscope view.

**Phase 6 — Polish:**
Entrance choreography (Shinoda-style word-by-word pacing), filter transitions, Making Log section. ~~Deploy~~ ✅ Live at thingsyifumake.uk.

## Commands

```bash
# Preview locally
python3 -m http.server 8000
# or
npx serve .

# Deploy (git + Netlify already connected)
git add . && git commit -m "description" && git push
# Netlify auto-deploys in ~15 seconds
```

## Style Notes

- **Cursor-lens (desktop):** Hidden native cursor. A ~80-100px div follows mouse with `mix-blend-mode: difference` — acts as invert-lens. On project dot hover, lens fills with B&W halftone image clipped to circle. Inspired by Formafantasma (image-in-cursor) + Shinoda (invert blend mode).
- **Mobile:** Gyroscope-driven panning via `DeviceOrientationEvent`. Constellation is larger than viewport, phone tilt explores it. Tap to reveal, tap to enter. Fallback: touch-drag.
- Grain: SVG noise filter as `body::after` pseudo-element at 2.5% opacity
- Motion: all animations via `requestAnimationFrame`, CSS transitions for UI state changes
- Typography: Cormorant Garamond for display/body, DM Mono for UI/labels
- The site should feel like a living space, not a document. Prioritise feel over information density.
