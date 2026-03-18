# thingsYifuMake — Design Plan v4 (Orbital)
*Updated March 2026. Source of truth for all design decisions.*

---

## 1. Overview

**Name:** `thingsYifuMake` — camelCase, direct. Domain: `thingsyifumake.com`
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

### Progression

1. **Land** — Dark canvas. Blob breathes. Dots orbit silently. Ambient music fades in. Only wordmark visible. Let people *watch*.
2. **Hover dot** — Dot blooms (elastic overshoot). Thin dotted leader line extends outward. Title fades in at end of line. ElevenLabs audio whisper speaks the title. That's it — no card.
3. **Click dot** — Preview expands. B&W / pixelated / halftone image treatment. Minimal info: image + title + mode color accent. Still light.
4. **Enter project** — Full page. Color returns. Detail lives here.

### Sound design

- **Music:** Ambient layer, starts on entry (with autoplay gate). Barely-there volume — you notice when it stops. Single continuous tone or generative texture, not a track.
- **Whispers:** ElevenLabs-generated voice speaking each project title. Quiet, like overhearing. Potentially spatial (pan based on dot position: left dot = left ear).
- **Interaction sounds:** Optional subtle tones on hover/click. Very restrained.

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

### Preview (second level — on click)

| Decision | Direction |
|---|---|
| Image treatment | B&W, or pixelated / halftone / dot-matrix |
| Image reveal | Progressive — starts degraded, sharpens |
| Card style | Minimal — no heavy border, floating, dark bg |
| Information shown | Image + title + mode color accent only |
| Card animation | TBD — scale from dot center vs materialize |

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

### Phase 2 — Sound + vibe
- [ ] Ambient music layer with autoplay gate ("click to enter" or first interaction unlocks)
- [ ] ElevenLabs whisper generation for all 23 project titles
- [ ] Whisper playback on hover with spatial panning
- [ ] Interaction sound design (optional subtle tones)

### Phase 3 — Preview + project pages
- [ ] B&W / halftone image treatment for preview cards
- [ ] Progressive image reveal (degraded → sharp)
- [ ] Project page ambient background (not static void)
- [ ] Year + link display on project pages
- [ ] Related projects section

### Phase 4 — Polish + deploy
- [ ] Mode filter transition (dots re-orbit)
- [ ] Mobile layout (vertical list + decorative header)
- [ ] Real photography session (minimum 5 images, one per mode)
- [ ] Deploy to Netlify + connect domain
- [ ] Making Log as live chronological section

---

## 8. Design References

| Reference | Lesson |
|---|---|
| Pentagram satellite orbital | Dots on rings, constant motion, legible |
| Yugo Nakamura / tha.jp | Typography as personality |
| Robin Mastromarino | Cursor-reactive physics, cinematic transitions |
| Neal.fun | Lightness, one sentence per project |
| David Whyte / beesandbombs | One obsession deeply expressed |
| Bruno Simon | The site IS the work |
| Lusion | R&D/lab section = Making Log |
| harm.work | Flat archive, URL as design decision |

---

## 9. Shelved Directions

**Workbench concept** — Overhead studio desk, objects with weight/shadow. Needs real photography to work. Return to this when photo assets exist.

**Flat constellation (v3)** — Built and working. Good foundation but movement felt ambient/random rather than purposeful. Orbital model gives movement meaning.
