# thingsYifuMake — Content Collection Sheet
*For images: just dump raw files into each project folder. The agent will resize, rename, and wire them into the site.*

---

## How This Works

### Your job:
1. Create a folder per project inside `assets/projects/[slug]/`
2. Dump ALL raw images, screenshots, Figma exports, PDF pages, videos into that folder — any name, any size, any format
3. Fill in the text sections below per project
4. The agent (Claude Code or this chat) will: resize images, rename them, update projects.json, and build the project page

### What goes in each folder:
- Photos from your phone (any size)
- Screenshots from Figma
- Exported pages from PDFs
- Old portfolio screenshots
- Student work photos (with permission)
- Screen recordings / video clips
- Sketches, diagrams, whiteboard photos
- Literally anything visual related to the project

Name them however you want. IMG_4392.jpg is fine. The agent will sort it out.

---

## Project Page Structure (following Marco Da Re)

Each project page will have this layout:

```
HERO IMAGE (full width)

MODE TAG                           YEAR

Project Title
Subtitle / one-line pitch (italic)

Tags: Design Research, HCI, ...
Collaborators: Name, Name, ...
Awards: Award name (year), ...
Link: → View paper / View demo

OVERVIEW
2-3 paragraphs. Personal voice.
Why this project exists. What you
were trying to figure out.

  [IMAGE with caption]

SECTION: Context / Problem
What situation or gap prompted this work?

  [IMAGE]  [IMAGE]
  caption  caption

SECTION: Process / How
What you actually did. Methods,
iterations, what went wrong.

  [IMAGE or VIDEO]

SECTION: Outcome / What emerged
What it became. What you learned.

  [IMAGE] [IMAGE] [IMAGE]

← Previous project    Next project →
```

Not every project needs every section. A podcast episode might just have hero + overview + one image. A CHI paper might have all sections. Scale to what the project deserves.

---

## DESIGNED

### 1. RepairBot Interface
**slug:** `repairbot-interface`
**Folder:** `assets/projects/repairbot-interface/` — dump images here

**Metadata:**
- Year: ___
- Collaborators: ___
- Awards: ___
- Link: _[Figma? Demo?]_

**Text:**
- Subtitle (one-line italic pitch): ___
- Overview (2-3 paragraphs): ___
- Section 1 title + text: ___
- Section 2 title + text: ___
- Section 3 title + text (optional): ___

**Images to dump in folder:**
- Hero image — _[Figma screenshot? Physical prototype?]_
- Process images — _[sketches? iterations? testing?]_
- Outcome images — _[final interface?]_
- Video — _[screen recording? demo?]_

**Whisper sentence:** ___

---

### 2. Startup Product Alpha
**slug:** `startup-product`
**Folder:** `assets/projects/startup-product/`

**Metadata:**
- Year: ___
- Collaborators: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: _[What was this actually?]_
- Section 1: ___
- Section 2: ___

**Images:** _[dump whatever you have]_
**Whisper sentence:** ___

---

### 3. Tangible Interaction Device
**slug:** `tangible-device`
**Folder:** `assets/projects/tangible-device/`

**Metadata:**
- Year: ___
- Collaborators: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: _[What was the object? What did it look like?]_
- Section 1: ___
- Section 2: ___

**Images:** _[device photos, sketches, hands interacting]_
**Whisper sentence:** ___

---

### 4. Wearable Sensor Prototype
**slug:** `wearable-sensor`
**Folder:** `assets/projects/wearable-sensor/`

**Metadata:**
- Year: ___
- Collaborators: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: _[What garment? What sensing?]_
- Section 1: ___
- Section 2: ___

**Images:** _[garment, electronics, worn, EMG data]_
**Video:** _[garment in motion? signals?]_
**Whisper sentence:** ___

---

### 5. Repair Workshop Kit
**slug:** `repair-kit`
**Folder:** `assets/projects/repair-kit/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: _[What's in the kit?]_
- Section 1: ___

**Images:** _[overhead of kit, in use during workshop]_
**Whisper sentence:** ___

---

## RESEARCHED

### 6. RepairBot Framework — CHI 2026
**slug:** `repairbot-framework`
**Folder:** `assets/projects/repairbot-framework/`

**Metadata:**
- Year: 2026
- Collaborators: _[co-authors]_
- Awards: ___
- Link: _[arXiv URL]_

**Text:**
- Subtitle: ___
- Overview (what the paper argues, the framework, why it matters): ___
- Section "Context" (the ideation gap, Study 2 findings): ___
- Section "Framework" (what RBCF is, how it works): ___
- Section "Findings" (key results): ___

**Images:** _[key figures, study setup, participants, diagrams, the PDF itself]_
**Whisper sentence:** _[e.g. "What if the chatbot could feel what your hands feel?"]_

---

### 7. Affective Tools for Thought
**slug:** `affective-tools`
**Folder:** `assets/projects/affective-tools/`

**Metadata:**
- Year: 2026
- Collaborators: Raffaele Buono, Nadia Bianchi-Berthouze
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___
- Section 1: ___

**Images:** _[conceptual diagram, framework figure]_
**Whisper sentence:** _[e.g. "Feeling isn't noise. Feeling is how you think."]_

---

### 8. Material-in-the-Loop
**slug:** `material-in-the-loop`
**Folder:** `assets/projects/material-in-the-loop/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[diagrams, material + screen side by side]_
**Whisper sentence:** ___

---

### 9. Embodied Interaction & Mending (Study 3)
**slug:** `embodied-mending`
**Folder:** `assets/projects/embodied-mending/`

**Metadata:**
- Year: 2026
- Collaborators: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview (WoZ setup, sensory gap, what you're investigating): ___
- Section "Setup" (voice agent, researcher panel): ___
- Section "Mechanisms" (M1 layering, M2 attending): ___

**Images:** _[study setup, participant mending, WoZ panel screenshot, architecture diagram]_
**Video:** _[study session clip?]_
**Whisper sentence:** ___

---

### 10. Touch as Language in HCI
**slug:** `touch-language`
**Folder:** `assets/projects/touch-language/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[conceptual image, diagrams]_
**Whisper sentence:** ___

---

## BUILT

### 11. Tennis Ball Machine Mk.1
**slug:** `tennis-machine-mk1`
**Folder:** `assets/projects/tennis-machine-mk1/`

**Metadata:**
- Year: ___
- Link: _[blog? video?]_

**Text:**
- Subtitle: ___
- Overview (what went wrong, what you learned): ___
- Section "The Build" (motor, frame, mistakes): ___
- Section "What It Taught Me": ___

**Images:** _[mid-build, motor, frame, broken parts, finished machine, workspace]_
**Video:** _[machine firing balls — #1 priority for video on whole site]_
**Whisper sentence:** _[e.g. "The motor spun the wrong way for three days before I noticed."]_

---

### 12. Tennis Ball Machine Mk.2
**slug:** `tennis-machine-mk2`
**Folder:** `assets/projects/tennis-machine-mk2/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[Mk.2 build, comparison with Mk.1]_
**Video:** _[Mk.2 in action]_
**Whisper sentence:** ___

---

### 13. Sensor Array for Garments
**slug:** `sensor-array`
**Folder:** `assets/projects/sensor-array/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[soldering, PCB, sensor on fabric, working prototype]_
**Video:** _[sensor responding to touch?]_
**Whisper sentence:** _[e.g. "Broken twice. Then it worked. Then I didn't trust it."]_

---

### 14. Making Log: Vol. 1
**slug:** `making-log-v1`
**Folder:** `assets/projects/making-log-v1/`

**Metadata:**
- Year: ___
- Link: _[blog? Notion?]_

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[notebook, writing setup, sample entries]_
**Whisper sentence:** ___

---

## TAUGHT

### 15. Interaction Design Lectures
**slug:** `interaction-lectures`
**Folder:** `assets/projects/interaction-lectures/`

**Metadata:**
- Year: ___
- Module name: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview (your angle, what makes your teaching different): ___

**Images:** _[lecture hall, slides, students working]_
**Whisper sentence:** ___

---

### 16. MSc Design Mentoring 2024
**slug:** `msc-mentoring`
**Folder:** `assets/projects/msc-mentoring/`

**Metadata:**
- Year: 2024

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[whiteboard, post-its, student work with permission]_
**Whisper sentence:** ___

---

### 17. Portfolio Agency: Cohort
**slug:** `portfolio-agency`
**Folder:** `assets/projects/portfolio-agency/`

**Metadata:**
- Year: ___
- Link: _[Portfolio Agency site?]_

**Text:**
- Subtitle: ___
- Overview (how many students? What programmes? Method?): ___

**Images:** _[student portfolios with permission, before/after]_
**Whisper sentence:** ___

---

### 18. Workshop: Embodied Making
**slug:** `workshop-embodied`
**Folder:** `assets/projects/workshop-embodied/`

**Metadata:**
- Year: ___
- Where held: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[participants making, materials, outcomes]_
**Video:** _[hands making?]_
**Whisper sentence:** ___

---

### 19. Design Research Methods
**slug:** `design-research-methods`
**Folder:** `assets/projects/design-research-methods/`

**Metadata:**
- Year: ___
- Link: ___

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[lecture slide, student artifacts]_
**Whisper sentence:** ___

---

## TALKED

### 20. ABQ — Creativity Series
**slug:** `abq-creativity`
**Folder:** `assets/projects/abq-creativity/`

**Metadata:**
- Year started: ___
- Link: _[Spotify? Apple? Website?]_

**Text:**
- Subtitle: ___
- Overview (what ABQ is, why you started it): ___

**Images:** _[mic setup, logo, recording session, studio]_
**Video:** _[recording in progress?]_
**Whisper sentence:** _[e.g. "We just talked until something interesting happened."]_

---

### 21. ABQ: Making & Thinking
**slug:** `abq-making-thinking`
**Folder:** `assets/projects/abq-making-thinking/`

**Metadata:**
- Year: ___
- Guest: ___
- Link: _[episode URL]_

**Text:**
- Subtitle: ___
- Overview (guest, key insight): ___

**Images:** _[guest photo, episode artwork]_
**Whisper sentence:** ___

---

### 22. ABQ: Designers in Research
**slug:** `abq-designers-research`
**Folder:** `assets/projects/abq-designers-research/`

**Metadata:**
- Year: ___
- Guest: ___
- Link: _[episode URL]_

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[guest photo, episode artwork]_
**Whisper sentence:** ___

---

### 23. ABQ: The Joy of Getting Stuck
**slug:** `abq-getting-stuck`
**Folder:** `assets/projects/abq-getting-stuck/`

**Metadata:**
- Year: ___
- Guest: ___
- Link: _[episode URL]_

**Text:**
- Subtitle: ___
- Overview: ___

**Images:** _[guest photo, episode artwork]_
**Whisper sentence:** ___

---

## Projects to Add?

| Project name | Mode | Year | What exists? | Include? |
|---|---|---|---|---|
| Tact Monster (basketball robot) | Designed / Built | 2019-2021 | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |

---

## Existing Assets — Where Is Everything?

**Old portfolio site:**
- URL: ___
- Projects covered: ___

**Figma files:**
- URL(s): ___
- Projects: ___

**Paper PDFs:**
- RepairBot Framework: ___
- Affective Tools for Thought: ___
- Others: ___

**Photos already taken:**
| Subject | Have it? | Where? |
|---|---|---|
| Tennis ball machine | | |
| Sensor array | | |
| Mending / repair | | |
| Workshop moments | | |
| ABQ podcast setup | | |
| Lectures / teaching | | |
| Student work | | |
| Physical prototypes | | |

---

## Whisper Sentences (batch-write, then batch-generate)

| # | Project | Whisper | Done? |
|---|---|---|---|
| 1 | RepairBot Interface | | ☐ |
| 2 | Startup Product Alpha | | ☐ |
| 3 | Tangible Interaction Device | | ☐ |
| 4 | Wearable Sensor Prototype | | ☐ |
| 5 | Repair Workshop Kit | | ☐ |
| 6 | RepairBot Framework | | ☐ |
| 7 | Affective Tools for Thought | | ☐ |
| 8 | Material-in-the-Loop | | ☐ |
| 9 | Embodied Interaction & Mending | | ☐ |
| 10 | Touch as Language in HCI | | ☐ |
| 11 | Tennis Ball Machine Mk.1 | | ☐ |
| 12 | Tennis Ball Machine Mk.2 | | ☐ |
| 13 | Sensor Array for Garments | | ☐ |
| 14 | Making Log: Vol. 1 | | ☐ |
| 15 | Interaction Design Lectures | | ☐ |
| 16 | MSc Design Mentoring 2024 | | ☐ |
| 17 | Portfolio Agency: Cohort | | ☐ |
| 18 | Workshop: Embodied Making | | ☐ |
| 19 | Design Research Methods | | ☐ |
| 20 | ABQ — Creativity Series | | ☐ |
| 21 | ABQ: Making & Thinking | | ☐ |
| 22 | ABQ: Designers in Research | | ☐ |
| 23 | ABQ: The Joy of Getting Stuck | | ☐ |

---

## ElevenLabs Voice Assignments

| Mode | Voice | Character |
|---|---|---|
| Designed | _[pick]_ | |
| Researched | _[pick]_ | |
| Built | _[pick]_ | |
| Taught | _[pick]_ | |
| Talked | _[pick]_ | |

---

## Ambient Music

- Generated? ___
- Tool: ___
- File: `assets/audio/ambient.mp3`
