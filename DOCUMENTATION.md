# thingsYifuMake — Complete Project Documentation
*Last updated: March 2026. For Yifu or any future agent continuing this work.*

---

## 1. What This Is

A personal portfolio website for Yifu — final-year PhD researcher at UCL Interaction Centre (UCLIC), product designer, maker, podcast host, based in London. The site is live at **thingsyifumake.uk**.

The site is NOT a CV. It's a space where a CHI paper and a tennis ball machine diary sit at the same level. The first impression should be: playful, surprising, alive. Like walking into someone's studio.

**Domain:** thingsyifumake.uk (registered on Cloudflare, DNS pointing to Netlify)
**Hosting:** Netlify (auto-deploys from GitHub on every push)
**Repo:** GitHub — `thingsYifuMake`
**Tech:** Pure HTML + CSS + JS. No framework. No build step. Single-file engine (`index.html`) + external data (`projects.json`).

---

## 2. How the Deployment Pipeline Works

```
Edit files on laptop (or via Claude Code)
        ↓
Preview locally: python3 -m http.server 8000 → localhost:8000
        ↓
git add . && git commit -m "description" && git push
        ↓
GitHub receives push → Netlify auto-detects → deploys in ~15 seconds
        ↓
Live at thingsyifumake.uk
```

No manual steps on Netlify. No build command. Just push.

---

## 3. File Structure

```
thingsYifuMake/
├── index.html              ← Site engine (HTML + CSS + JS, single file)
├── projects.json           ← All project content (edit this to change content)
├── CLAUDE.md               ← Claude Code setup guide (read-this-first for agents)
├── DESIGN.md               ← All design decisions + build priorities
├── README.md               ← Deployment guide
├── DOCUMENTATION.md        ← This file
├── .gitignore
└── assets/
    ├── audio/
    │   ├── ambient.mp3     ← Background music loop (60-120s, seamless)
    │   └── whispers/       ← Per-project audio whispers
    │       ├── repairbot-framework.mp3
    │       ├── tennis-machine-mk1.mp3
    │       └── ...         ← One MP3 per project slug
    └── projects/
        ├── repairbot-framework/
        │   ├── preview.jpg     ← 880×520 (displays at 440×260, 2x retina)
        │   ├── cover.jpg       ← 2800×1200 (displays at 1400×600, 2x retina)
        │   └── loop.mp4        ← Optional 5-10s silent video loop
        ├── tennis-machine-mk1/
        │   └── ...
        └── ...                 ← One folder per project slug
```

### Which file does what

| File | Purpose | When to edit |
|---|---|---|
| `projects.json` | All project content — titles, descriptions, tags, years, links, whisper sentences, image paths | Adding/editing/removing projects |
| `index.html` | The site engine — layout, animation, interaction logic | Changing how the site works or looks |
| `DESIGN.md` | Design decisions, visual direction, interaction specs, build phases | Planning new features or revisiting design intent |
| `CLAUDE.md` | Quick-start guide for Claude Code or any AI agent | When starting a new agent session |
| `README.md` | Deployment, git, domain, image prep instructions | Setting up on a new machine |

---

## 4. The Design Vision

### Two views

**Constellation (default):** Dark canvas. Project dots orbit a reactive center blob on elliptical rings. Ambient music plays. Cursor is a large invert-lens (~80-100px, `mix-blend-mode: difference`) that fills with a B&W halftone image when hovering a project dot. A whispered sentence plays. Clicking enters the project page.

**List (backup):** Flat text list, Formafantasma `/works` style. System fonts (Times New Roman + Arial). One row per project. Toggle between views via button in top-right. URL hash: `#constellation` vs `#list`.

### Interaction progression (low → high detail)

1. **Land** — Dark canvas, blob breathes, dots orbit, music fades in. Just watch.
2. **Hover dot** — Dot blooms, cursor fills with B&W image, leader line extends, title appears, whisper plays.
3. **Click dot** — Preview expands. Minimal: image + title + mode color.
4. **Enter project** — Full page. Color returns. All detail lives here.

### Mobile

- **Primary:** Gyroscope exploration — tilt phone to pan across constellation (larger than viewport). Tap to reveal, tap to enter.
- **Backup:** List view — vertical scroll, one tap away from gyroscope.

### Sound

- **Ambient music:** Warm drone, NIN Ghosts V: Together vibe. 60-120s seamless loop. Barely-there volume.
- **Whispers:** One evocative sentence per project, spoken by one of five voices (one per mode). Spatial panning based on dot position.

### Typography

| Context | Font |
|---|---|
| Constellation view — display/titles | Cormorant Garamond, weight 300 |
| Constellation view — UI/labels | DM Mono, weight 300-400 |
| Constellation view — body | Cormorant Garamond, 13.5px, line-height 2.05 |
| List view — titles/body | Times New Roman (system) |
| List view — UI/labels | Arial (system) |

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

### Design references

| Reference | What to steal |
|---|---|
| Pentagram satellite orbital | Dots on rings, constant motion |
| Shinoda / Leon Brown | Invert-lens cursor, word-by-word entrance pacing |
| Formafantasma | Image-in-cursor, list view layout, system fonts |
| Marco Da Re | Project page layout — text/pic/video structure |
| NIN Ghosts V: Together | Music vibe — warm drones, spacious, barely there |
| Robin Mastromarino | Cursor-reactive physics, cinematic transitions |
| Neal.fun | Tone of lightness, no ego |
| Bruno Simon | The site IS the work |

---

## 5. Build Phases + Status

| Phase | Description | Status |
|---|---|---|
| 0 | Project structure, data separation, deployment | ✅ Done |
| 1 | Orbital prototype (rings, blob, dot bloom, leader lines) | 🔲 Not started |
| 2 | Cursor-lens + sound (invert lens, image-in-cursor, music, whispers) | 🔲 Not started |
| 3 | Project pages (Marco Da Re layout, image treatment, ambient bg) | 🔲 Not started |
| 4 | Mobile (gyroscope exploration, tap-to-reveal, fallback) | 🔲 Not started |
| 5 | List view (Formafantasma style, system fonts, view toggle) | 🔲 Not started |
| 6 | Polish (entrance choreography, filter transitions, Making Log) | 🔲 Not started |

See `DESIGN.md` for detailed task lists per phase.

---

## 6. How to Populate Content

### Step 1 — Edit projects.json

Every project is one object in the JSON array. Here's the full format with every field explained:

```json
{
  "mode": "Built",
  "slug": "tennis-machine-mk1",
  "title": "Tennis Ball Machine Mk.1",
  "desc": "A self-commissioned engineering project. A motor that spun wrong, a frame that vibrated itself apart — the slow realisation that building teaches you what you didn't know you didn't know.",
  "tags": ["Making", "Engineering", "Log"],
  "year": 2024,
  "link": "https://example.com/optional-external-link",
  "whisper": "The motor spun the wrong way for three days before I noticed.",
  "previewImage": "assets/projects/tennis-machine-mk1/preview.jpg",
  "coverImage": "assets/projects/tennis-machine-mk1/cover.jpg",
  "previewVideo": null
}
```

| Field | What it is | Required | Example |
|---|---|---|---|
| `mode` | One of: `Designed`, `Researched`, `Built`, `Taught`, `Talked` | Yes | `"Built"` |
| `slug` | URL-safe name, matches the asset folder name | Yes | `"tennis-machine-mk1"` |
| `title` | Display title | Yes | `"Tennis Ball Machine Mk.1"` |
| `desc` | 1-3 sentences. Honest, specific, in your voice. Not a pitch. | Yes | See below for writing guide |
| `tags` | 2-4 short labels for the project page | Yes | `["Making", "Engineering"]` |
| `year` | Year the project was made or published | Yes | `2024` |
| `link` | External URL (arXiv, podcast episode, etc). `null` if none. | No | `"https://arxiv.org/abs/..."` |
| `whisper` | One evocative sentence for the audio whisper. Diary-entry tone. | No | `"What if the chatbot could feel what your hands feel?"` |
| `previewImage` | Path to card thumbnail. `null` = generated gradient. | No | `"assets/projects/slug/preview.jpg"` |
| `coverImage` | Path to project page hero. `null` = generated gradient. | No | `"assets/projects/slug/cover.jpg"` |
| `previewVideo` | Path to silent video loop. `null` = no video. | No | `"assets/projects/slug/loop.mp4"` |

### Step 2 — Prepare images

**Source photos** from phone/camera are 5-10MB. They need to be resized for web:

| Asset | Export dimensions (2x retina) | Target file size | Format |
|---|---|---|---|
| Preview thumbnail | 880 × 520 px | 80-100 KB | JPG, 80% quality |
| Cover hero | 2800 × 1200 px | 300-400 KB | JPG, 85% quality |
| Video loop | Any (16:9 ideal) | < 3 MB | MP4, H.264, silent |

**Resize on Mac:**
```bash
# Using sips (built into macOS)
sips -z 520 880 input.jpg --out assets/projects/slug/preview.jpg

# Or with ImageMagick (brew install imagemagick)
convert input.jpg -resize 880x520^ -gravity center -extent 880x520 -quality 80 preview.jpg
convert input.jpg -resize 2800x1200^ -gravity center -extent 2800x1200 -quality 85 cover.jpg
```

**Photo ideas per mode:**

| Mode | What to shoot |
|---|---|
| Designed | Overhead shot of physical prototype on white/wood surface |
| Researched | Printed paper with annotations, diagram close-up, screen with code |
| Built | Process photo — mid-build, wires visible, hands in frame |
| Taught | Student sketch, whiteboard, workshop moment |
| Talked | Podcast mic setup, guest moment, recording environment |

Keep originals on iCloud/cloud storage. Only the resized copies go in the project folder.

### Step 3 — Prepare audio whispers

1. Write one evocative sentence per project (the `whisper` field in JSON)
2. Open ElevenLabs
3. Pick 5 voices — one per mode. Aim for: overhearing someone, not being addressed.
4. Settings: stability ~75%, clarity ~80%, style exaggeration low
5. Generate each sentence, export as MP3
6. Name files by slug: `repairbot-framework.mp3`, `tennis-machine-mk1.mp3`
7. Save to `assets/audio/whispers/`

### Step 4 — Prepare ambient music

Use Suno, Udio, or similar with this prompt:

```
Ambient drone, 90 seconds, seamless loop. Warm analog synthesizer 
pads that evolve very slowly. Gentle buzzing and humming undertones. 
Occasional soft piano note, single keys, widely spaced. No melody, 
no beat, no rhythm. Breathy exhaling textures. Slight dissonance 
that resolves into consonance. Spacious and meditative, like an 
empty room with good acoustics. Inspired by Brian Eno, Trent Reznor 
film scores, Angelo Badalamenti. Low energy, intimate, barely there.
```

Save as `assets/audio/ambient.mp3`. Keep under 2MB.

### Step 5 — Push

```bash
git add .
git commit -m "added tennis machine photos + whisper audio"
git push
```

Live in 15 seconds.

---

## 7. Writing Guide for Project Descriptions

The `desc` field is what people read on the project page. It should sound like you talking about the project to someone interested, not like a grant application.

**Good pattern:** What it is + what made it interesting/difficult + what it revealed.

**Examples:**

✅ "A self-commissioned engineering project. A motor that spun wrong, a frame that vibrated itself apart — the slow realisation that building teaches you what you didn't know you didn't know."

✅ "A framework for human-touch-aware conversational agents in textile repair. Introduces the concept of material-sensitive dialogue and the Ideation Gap."

❌ "This project explores the intersection of embodied cognition and computational design through a novel framework for..." (too academic)

❌ "Built a tennis ball machine." (too empty)

**Aim for:** 1-3 sentences. Specific. Honest. Something only you would say about it.

### Writing guide for whisper sentences

The `whisper` is not a summary. It's the one thought you'd have about the project at 2am. A fragment from a diary, not a pitch.

**Examples:**

| Project | Whisper |
|---|---|
| RepairBot Framework | "What if the chatbot could feel what your hands feel?" |
| Tennis Ball Machine Mk.1 | "The motor spun the wrong way for three days before I noticed." |
| ABQ Podcast | "We just talked until something interesting happened." |
| Affective Tools for Thought | "Feeling isn't noise. Feeling is how you think." |
| Sensor Array | "Broken twice. Then it worked. Then I didn't trust it." |

---

## 8. How to Add a New Project (Complete Checklist)

1. **Create asset folder:** `mkdir assets/projects/your-slug`
2. **Take/find photos**, resize to 880×520 (preview) and 2800×1200 (cover)
3. **Save images** to `assets/projects/your-slug/preview.jpg` and `cover.jpg`
4. **Write the whisper sentence**, generate audio in ElevenLabs, save to `assets/audio/whispers/your-slug.mp3`
5. **Add entry to projects.json:**
```json
{
  "mode": "Built",
  "slug": "your-slug",
  "title": "Your Project Title",
  "desc": "1-3 sentences in your voice.",
  "tags": ["Tag1", "Tag2"],
  "year": 2026,
  "link": null,
  "whisper": "Your evocative one-liner.",
  "previewImage": "assets/projects/your-slug/preview.jpg",
  "coverImage": "assets/projects/your-slug/cover.jpg",
  "previewVideo": null
}
```
6. **Preview locally:** `python3 -m http.server 8000`
7. **Push:** `git add . && git commit -m "added your-slug" && git push`
8. **Check** thingsyifumake.uk

---

## 9. How to Continue Building with an AI Agent

Open the project folder in Claude Code (or paste into a new Claude chat) and say:

> "Read CLAUDE.md and DESIGN.md. The site is live at thingsyifumake.uk. Current state: [describe what's been built so far]. I want to work on [Phase X / specific feature]. Here's the current index.html: [paste if needed]."

The agent needs:
- `CLAUDE.md` — tech stack, architecture, current state
- `DESIGN.md` — design decisions, interaction specs, build phases
- `projects.json` — content data
- `index.html` — current code (paste or reference)

If starting from scratch in a new session, also share:
- This file (`DOCUMENTATION.md`) for full context
- The Pentagram orbital reference image (if discussing constellation layout)
- Any new mood board pins or reference URLs

---

## 10. Current Content Inventory

23 projects across 5 modes. All currently have generated gradient placeholders — no real images yet.

| Mode | Count | Projects |
|---|---|---|
| Designed | 5 | RepairBot Interface, Startup Product Alpha, Tangible Interaction Device, Wearable Sensor Prototype, Repair Workshop Kit |
| Researched | 5 | RepairBot Framework (CHI 2026), Affective Tools for Thought (CHI 2026), Material-in-the-Loop, Embodied Interaction & Mending, Touch as Language in HCI |
| Built | 4 | Tennis Ball Machine Mk.1, Tennis Ball Machine Mk.2, Sensor Array for Garments, Making Log: Vol. 1 |
| Taught | 5 | Interaction Design Lectures, MSc Design Mentoring 2024, Portfolio Agency: Cohort, Workshop: Embodied Making, Design Research Methods |
| Talked | 4 | ABQ — Creativity Series, ABQ: Making & Thinking, ABQ: Designers in Research, ABQ: The Joy of Getting Stuck |

### What needs populating per project

| Field | Status |
|---|---|
| mode, slug, title, desc, tags | ✅ All 23 done |
| year | ✅ All 23 done |
| link | 🔲 Needs real URLs (arXiv, podcast links, etc.) |
| whisper | 🔲 Needs writing (23 sentences) |
| previewImage | 🔲 Needs photography + resize |
| coverImage | 🔲 Needs photography + resize |
| previewVideo | 🔲 Optional — prioritize for Built mode projects |
| whisper audio | 🔲 Needs ElevenLabs generation (23 MP3s) |
| ambient music | 🔲 Needs generation (1 MP3) |

---

## 11. Minimum Viable Populated Site

You don't need all 23 projects fully populated to make the site feel real. Here's the minimum that transforms it from placeholder to portfolio:

**5 photos (one per mode):**
- RepairBot Framework → printed paper with annotations
- RepairBot Interface → overhead of prototype
- Tennis Ball Machine Mk.1 → mid-build process shot
- Interaction Design Lectures → whiteboard or workshop moment
- ABQ Creativity Series → mic/podcast setup

**5 whisper sentences + audio (one per mode):**
- Generate one clip per mode to test the interaction

**1 ambient music loop:**
- One 90-second drone

**Real links for published work:**
- RepairBot Framework arXiv URL
- Affective Tools for Thought URL (if available)
- ABQ podcast link

That's maybe 2-3 hours of work total, and the site goes from "prototype with placeholders" to "portfolio with character."
