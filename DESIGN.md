# thingsYifuMake — Design Plan v4 (Orbital)
*Updated March 2026. Source of truth for all design decisions.*

---

## 1. Overview

**Name:** `thingsYifuMake` — camelCase, direct. Domain: `thingsyifumake.uk`
**Owner:** Yifu — final-year PhD at UCL (UCLIC), product design background, maker, podcast host.
**Audience:** Future employers / fellowships + curious people.
**First impression goal:** Playful, surprising, alive. Not a CV.

**Tagline:** `PhD · Designer · Maker · London`

---

## 2. Direction: Orbital Constellation

**Previous:** Flat constellation with sinusoidal drift (v3, built).
**New direction:** Orbital model inspired by Pentagram satellite visualization.

### Composition

```
                    ·  ·
                 ·        ·        ← outer ring (slowest)
              ·    ·  ·     ·
           ·    ·       ·     ·    ← middle ring
          ·   ·  [BLOB]  ·    ·
           ·    ·       ·     ·    ← inner ring
              ·    ·  ·     ·
                 ·        ·
                    ·  ·
```

- **Center:** Hand-drawn wobbly blob. Reactive to cursor. Breathes softly at rest.
- **Rings:** 2–3 elliptical orbits at different speeds + tilts. Each dot rides a ring.
- **Dots:** Color-coded by mode. Constantly orbiting. Varied sizes possible.
- **Interaction:** Hover a dot → thin leader line extends outward → title whispers in.

### Why this over flat constellation

- Movement has *purpose* (orbital paths) not just ambient drift
- Center blob gives the site a heart — something alive to discover
- Orbital rings create natural visual hierarchy (inner = closer, outer = further)
- Simpler math (angle + radius + angular velocity per dot)
- The Pentagram reference validates this as legible and elegant

---

## 3. Landing Experience — Low → High Detail

The site should feel like arriving in a space, not loading a page. Music sets the tone immediately. Information is earned through exploration.

### Progression (Desktop)

1. **Land** — Dark canvas. Blob breathes. Dots orbit silently. Ambient music fades in. Only wordmark visible. Cursor is a large circle (~80-100px) with `mix-blend-mode: difference` — acts as an invert-lens, making you want to sweep across the canvas.
2. **Hover dot** — Dot blooms (elastic overshoot). The cursor-lens fills with a B&W halftone preview image of the project (image lives *inside* the cursor, moves with it). Thin dotted leader line extends outward. Title fades in at end of line. ElevenLabs audio whisper plays — a short evocative sentence, not just the title.
3. **Click dot** — Preview expands from cursor position. Minimal info: image + title + mode color accent. Still light.
4. **Enter project** — Full page (Marco Da Re-style layout). Color returns. Detail lives here.

### Progression (Mobile — Gyroscope Exploration)

Phone tilt/orientation pans the viewport across the constellation. The orbital system renders larger than the screen — tilting explores it like looking through a window into a room. Tilting toward a dot cluster brings them closer/larger. Tapping a dot triggers: circle expands from tap point revealing B&W image + title + whisper audio, then contracts. Tap again to enter project page.

Uses `DeviceOrientationEvent` API. Needs permission prompt on iOS ("Allow motion access?"). Fallback: touch-drag panning if gyroscope unavailable or denied.

### Cursor-Lens (Desktop)

- **Default state:** ~80-100px circle, no fill, `mix-blend-mode: difference`. Inverts whatever it passes over — bright on dark bg, dark on light text.
- **Hover project dot:** Circle fills with the project's preview image (B&W halftone treatment). Image is clipped to the circle shape. Smooth fade-in (~300ms). Image moves with cursor.
- **Leave dot:** Image fades out, circle returns to invert-lens.
- **Hover blob:** TBD — could distort the lens shape itself.
- **Implementation:** A div following cursor position via `mousemove`, with CSS `clip-path: circle()` and `mix-blend-mode`. Image swapped via JS on dot mouseenter/mouseleave. Use `will-change: transform` for performance.

Inspired by: Formafantasma (image-in-cursor preview), Shinoda/Leon Brown (mix-blend-mode invert lens).

### Sound design

- **Music:** Ambient layer inspired by Nine Inch Nails — Ghosts V: Together (warm drones, evolving pads, no melody). Starts on entry with autoplay gate. Barely-there volume — you notice when it stops. 60-120s seamless loop.
- **Whispers:** ElevenLabs-generated voice speaking a short evocative sentence per project (not just the title). One sentence, diary-entry tone. E.g. "What if the chatbot could feel what your hands feel?" not "RepairBot Framework." Five different voices, one per mode — each mode has its own vocal character. Spatial panning based on dot position (left dot = left ear).
- **Interaction sounds:** Optional subtle tones on hover/click. Very restrained.

#### Music generation prompt (for Suno / Udio / similar)

```
Ambient drone, 90 seconds, seamless loop. Warm analog synthesizer pads 
that evolve very slowly. Gentle buzzing and humming undertones. Occasional 
soft piano note, single keys, widely spaced. No melody, no beat, no rhythm. 
Breathy exhaling textures. Slight dissonance that resolves into consonance. 
Spacious and meditative, like an empty room with good acoustics. Inspired 
by Brian Eno, Trent Reznor film scores, Angelo Badalamenti. Low energy, 
intimate, barely there. Should feel like air in a room — you notice it 
when it stops.
```

---

## 3.5. List View (Backup — Desktop + Mobile)

A flat, text-first project list accessible as an alternative view. References Formafantasma `/works` directly — same information architecture, adapted to thingsYifuMake's five modes.

### Why

The constellation is the *experience*. The list is the *reference*. Some visitors (employers, academics, people on slow connections) want to scan all 23 projects quickly. The list view gives them that without losing the site's identity. It also solves mobile accessibility — the gyroscope is the wow, the list is the safety net.

### Typography (list view only)

System fonts, following Formafantasma's approach — zero HTTP requests, instant load.

```
Titles:       Times New Roman, serif — 16px
UI / labels:  Arial, sans-serif — 11px, uppercase, letter-spacing .12em
Body / desc:  Times New Roman, serif — 14px, line-height 1.7
Year / tags:  Arial, sans-serif — 10px
```

The constellation view keeps Cormorant Garamond + DM Mono. The list view switches to system fonts. This creates a deliberate contrast: the constellation is rich and atmospheric; the list is lean and functional.

### Layout

Each project is a single row:

```
[index]  [title]                              [mode tag]  [year]
         Short description visible on expand / hover
```

- **Index:** Sequential number in DM Mono or Arial, dimmed
- **Title:** Times New Roman, left-aligned, full width
- **Mode tag:** Colored pill or text in mode color (Designed, Researched, etc.)
- **Year:** Right-aligned, dimmed
- **Description:** Appears below the row on click/hover, in dimmed serif
- **Explore link:** Below description, minimal ("→ open project")

### Mode filter

Same five filters as constellation view (All / Designed / Researched / Built / Taught / Talked), displayed as text toggles at the top. Active filter underlined or colored.

### Switching between views

A small toggle in the top-right corner: `constellation` / `list`. Clicking switches without page reload. The URL could reflect the view: `thingsyifumake.uk/#list` vs `thingsyifumake.uk/#constellation` (or default).

### Mobile behavior

On mobile, the list view is always available via a toggle or swipe. The gyroscope constellation is the default landing, but the list is one tap away. This means mobile has two modes:
1. **Gyroscope constellation** — tilt to explore, tap to reveal (the wow)
2. **List view** — vertical scroll, Formafantasma-style (the safety net)

---

## 4. Design Details — Pin Reference Checklist

### Dots

| Decision | Direction |
|---|---|
| Shape at rest | TBD — perfect circle vs slightly organic |
| Size variation | TBD — uniform vs scaled by recency |
| Bloom animation | Elastic overshoot + settle |
| Bloom halo | TBD — soft glow vs radial blur dissolve |
| Opacity at rest | Slightly translucent (embedded in sky) |
| Idle breathing | Barely perceptible scale oscillation |
| Entrance on load | Settle into orbit positions (not instant) |

### Lines and connections

| Decision | Direction |
|---|---|
| Constellation lines | **Replaced by orbital rings** — thin elliptical paths, always visible |
| Ring style | Thin, low opacity, possibly dashed or dotted |
| Ring breathing | Gentle opacity pulse |
| Leader lines (on hover) | Thin dotted line extending from dot outward to title |
| Leader line animation | Draws outward from dot on hover, retracts on leave |
| Line cap | Round |

### Center Blob

| Decision | Direction |
|---|---|
| Visual style | Hand-drawn / wobbly / organic — NOT a clean sphere |
| Rendering | Canvas 2D with perlin-noise displacement on a base circle |
| At rest | Soft breathing (slow shape oscillation) |
| Cursor reaction | Distorts toward cursor (attraction / soft-body feel) |
| Color | TBD — monochrome, or subtly tinted? |
| Click behavior | TBD — could be an easter egg, or do nothing |
| Size | ~15–20% of viewport width |

### Preview (hover — lives inside cursor-lens)

| Decision | Direction |
|---|---|
| Image treatment | B&W halftone — clipped to cursor circle |
| Image reveal | Fade in (~300ms) when cursor enters dot zone |
| Container | The cursor itself — no separate card |
| Information shown | Image only in cursor; title on leader line outside |
| On mobile | Circle expands from tap point, B&W image fills it |

### Background

| Decision | Direction |
|---|---|
| Star field | Keep, but potentially reduce density |
| Depth layers | TBD — single plane vs 2–3 parallax |
| Nebula / fog | TBD — faint color clouds behind ring groups? |
| Grain | Keep (SVG noise at 2.5% opacity) |
| Base color | `#07070A` near-black (keep) |

### Typography

| Use | Font |
|---|---|
| Display / titles | Cormorant Garamond, weight 300 |
| Wordmark `Yifu` | Cormorant Garamond, italic |
| UI / labels | DM Mono, weight 300–400 |
| Body (project pages) | Cormorant Garamond 300, 13.5px, line-height 2.05 |
| Whisper titles (hover) | TBD — could be DM Mono at small size |

### Colour palette

```
Designed:   #E8C17A  (warm amber)
Researched: #7AB8E8  (cool blue)
Built:      #7AE8C1  (teal/mint)
Taught:     #E87A7A  (coral red)
Talked:     #C17AE8  (violet)
Background: #07070A  (near-black)
Text:       #EDE9E2  (warm white)
```

---

## 5. Content — Five Modes

All content tagged by mode. One unified world, filterable.

| Mode | Content |
|---|---|
| **Designed** | Product design, startup products, tangible interfaces, wearables, repair kit |
| **Researched** | CHI papers, Material-in-the-Loop, PhD Study 3, embodied interaction |
| **Built** | Tennis ball machines, sensor array, Making Log |
| **Taught** | UCL lectures, MSc mentoring, portfolio cohort, workshops |
| **Talked** | ABQ podcast episodes, guests, show identity |

Content lives in `projects.json`. 23 projects currently. See `README.md` for editing instructions.

---

## 6. Technical Architecture

```
thingsYifuMake/
├── index.html           ← Engine (HTML + CSS + JS)
├── projects.json        ← Content data (edit here)
├── .gitignore
├── DESIGN.md            ← This file
├── CLAUDE.md            ← Claude Code setup guide
├── README.md            ← Deployment guide
└── assets/
    ├── audio/
    │   ├── ambient.mp3  ← Background music loop
    │   └── whispers/    ← Per-project title whispers
    │       ├── repairbot-interface.mp3
    │       └── ...
    └── projects/
        ├── repairbot-interface/
        │   ├── preview.jpg   ← 440×260
        │   ├── cover.jpg     ← 1400×600
        │   └── loop.mp4      ← optional
        └── ...
```

### Data format (projects.json)

```json
{
  "mode": "Built",
  "slug": "tennis-machine-mk1",
  "title": "Tennis Ball Machine Mk.1",
  "desc": "...",
  "tags": ["Making", "Engineering"],
  "year": 2024,
  "link": null,
  "whisper": "The motor spun the wrong way for three days before I noticed.",
  "previewImage": null,
  "coverImage": null,
  "previewVideo": null
}
```

Set image/video paths to enable real assets. `null` = generated gradient fallback.

---

## 7. Build Priorities

### Phase 1 — Orbital prototype
- [ ] Orbital ring math (elliptical paths, 2–3 rings, varied speed)
- [ ] Dots riding rings with correct angular velocity
- [ ] Center blob (canvas, perlin displacement, cursor reactivity)
- [ ] Dot bloom animation (elastic overshoot)
- [ ] Leader line hover (dotted, extends outward, title at end)

### Phase 2 — Cursor-lens + sound
- [ ] Large invert-lens cursor (`mix-blend-mode: difference`, ~80-100px)
- [ ] Image-in-cursor on dot hover (B&W halftone, clipped to circle, moves with mouse)
- [ ] Smooth image swap between dots (fade out → fade in)
- [ ] Ambient music layer with autoplay gate (NIN Ghosts V: Together vibe)
- [ ] ElevenLabs whisper sentences — 23 clips, 5 voices (one per mode)
- [ ] Whisper playback on hover with spatial panning (Web Audio API panNode)

### Phase 3 — Preview + project pages
- [ ] Project page layout (Marco Da Re-style: text, pic, video structure)
- [ ] B&W / halftone image treatment for hover previews
- [ ] Progressive image reveal on project page (degraded → sharp)
- [ ] Project page ambient background (not static void)
- [ ] Year + link display on project pages
- [ ] Related projects section

### Phase 4 — Mobile (gyroscope exploration)
- [ ] `DeviceOrientationEvent` API integration + iOS permission prompt
- [ ] Constellation renders larger than viewport, tilt pans the view
- [ ] Dot proximity scaling (closer to center = larger)
- [ ] Tap-to-reveal: circle expands from tap, shows B&W image + title + whisper
- [ ] Tap-to-enter: second tap opens project page
- [ ] Fallback: touch-drag panning if gyroscope unavailable
- [ ] Mobile project page layout (responsive typography + image sizing)

### Phase 5 — List view (backup)
- [ ] Flat text list, Formafantasma `/works` style
- [ ] System fonts: Times New Roman (titles/body) + Arial (UI/labels)
- [ ] Row per project: index, title, mode tag (colored), year
- [ ] Click/hover expands description + "→ open project" link
- [ ] Mode filter (same five toggles, text-only)
- [ ] View toggle: constellation ↔ list (top-right, no page reload)
- [ ] URL hash: `#constellation` (default) vs `#list`
- [ ] Mobile: list always one tap away from gyroscope view

### Phase 6 — Polish
- [ ] Mode filter transition (dots re-orbit)
- [ ] Entrance choreography (Shinoda-style pacing: dots appear one-by-one, wordmark types itself)
- [ ] Real photography session (minimum 5 images, one per mode)
- [ ] ~~Deploy to Netlify + connect domain~~ ✅ DONE (thingsyifumake.uk)
- [ ] Making Log as live chronological section

---

## 8. Design References

| Reference | Lesson |
|---|---|
| **Pentagram satellite orbital** | Dots on rings, constant motion, legible |
| **Shinoda / Leon Brown** | mix-blend-mode invert cursor as exploration lens; word-by-word entrance pacing |
| **Formafantasma** | Image preview in cursor; list view layout + system font typography; energy-conscious design |
| **Marco Da Re** | Project page layout — text, pic, video structure; honest research writing |
| **NIN Ghosts V: Together** | Music reference — warm drones, evolving pads, spacious, barely-there |
| **Yugo Nakamura / tha.jp** | Typography as personality |
| **Robin Mastromarino** | Cursor-reactive physics, cinematic transitions |
| **Neal.fun** | Lightness, one sentence per project |
| **David Whyte / beesandbombs** | One obsession deeply expressed |
| **Bruno Simon** | The site IS the work |
| **Lusion** | R&D/lab section = Making Log |
| **harm.work** | Flat archive, URL as design decision |

---

## 9. Shelved Directions

**Workbench concept** — Overhead studio desk, objects with weight/shadow. Needs real photography to work. Return to this when photo assets exist.

**Flat constellation (v3)** — Built and working. Good foundation but movement felt ambient/random rather than purposeful. Orbital model gives movement meaning.
