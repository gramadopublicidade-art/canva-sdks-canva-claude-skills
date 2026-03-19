---
name: canva-create-carousel
description: Create a multi-slide Instagram/social media carousel in a Twitter/X dark-quote style — black background, white text, circular profile photo, verified badge, and handle. Use when the user asks to "create a carousel", "make a quote carousel", "create slides in Twitter style", "make a dark quote post", or "create a carousel in this style" (especially when showing a screenshot of a dark-background tweet-style post).
---

# Canva Quote Carousel Creator

Generate a polished multi-slide carousel in the viral Twitter/X dark-quote style: black background, large white quote text, and a profile header with avatar, name, verified badge, and handle — optimised for Instagram, LinkedIn, and other social platforms.

## Visual Style Reference

Each slide follows this layout (1080 × 1080 px):

```
┌─────────────────────────────────────┐
│  [avatar]  Name ✓        · · ·      │  ← profile header
│            @handle                   │
│                                     │
│   "Quote or key point               │  ← main content
│    spanning two or                  │
│    three lines."                    │
│                                     │
│                                     │ 
└─────────────────────────────────────┘
```

- **Background**: solid black (#000000)
- **Name**: bold white, ~18–20 px
- **Verified badge**: blue checkmark (✓) next to the name
- **Handle**: light gray (#8B98A5), ~15–16 px, below the name
- **Quote text**: white, large (36–48 px), left-aligned, upper portion of the slide
- **Three-dot menu**: top-right corner, gray
- **Avatar**: circular, top-left

---

## Workflow

### Step 1: Gather Content

Ask the user for the following (or extract from what they already provided):

1. **Profile name** — e.g., "Pedro Zanatta"
2. **Handle** — e.g., "@pedrozanatta1"
3. **Profile photo** — a Canva image URL, upload, or description; use a professional headshot placeholder if not provided
4. **Carousel content** — one of:
   - A list of quotes/points (one per slide)
   - A topic or theme — generate 5–8 punchy, standalone quotes on that topic
   - A long-form text to break into bite-sized slides

If the user provides a topic instead of ready-made quotes, generate them yourself using these rules:
- Each quote must stand alone — no slide should depend on reading another
- Keep quotes to 2–4 lines of text max
- Use assertive, first-person or universal language ("Success is…", "The people who…")
- Mix statement, contrast, and question formats for variety
- Aim for 5–8 slides by default (ask the user if they want more or fewer)

### Step 2: Plan the Carousel

Before generating, present the slide plan to the user:

```
Here's the plan for your carousel (8 slides):

Slide 1 — Cover
"O sucesso não é construído nos dias fáceis, mas na consistência dos dias difíceis."

Slide 2
"Disciplina é escolher entre o que você quer agora e o que você quer mais."

Slide 3
"A maioria desiste quando o processo fica difícil. Essa é exatamente a hora de continuar."

...

Slide 8 — CTA
"Salva esse carrossel e compartilha com quem precisa ouvir isso. 👇"

Profile: Pedro Zanatta (@pedrozanatta1)
Style: Twitter/X dark quote
Format: 1080 × 1080 px (Instagram Post)
```

Wait for the user to approve or adjust the slide content. This is the **only approval step**.

### Step 3: Generate the Carousel Design

Call `generate-design` with a detailed prompt following the format below. After calling it, immediately call `get-design-generation-job` with the returned job ID to poll for completion (retry every 3–5 seconds until status is `"success"`).

#### Generation Query Format

```
Create a multi-slide Instagram carousel in a Twitter/X dark-quote style.

VISUAL STYLE:
- Black (#000000) background on every slide
- Profile header top-left: circular avatar, bold white name "[NAME]", blue verified checkmark ✓, gray handle "[HANDLE]"
- Three-dot menu icon (···) in the top-right corner of every slide
- Main quote text: white, large (40–48 px), left-aligned, positioned in the upper-center area
- Clean, minimal layout — no gradients, no patterns, no extra decorations
- Optional: small muted-speaker icon (🔇) bottom-right corner

SLIDES:
[List each slide with its quote/content]

Slide 1 (Cover): "[quote]"
Slide 2: "[quote]"
Slide 3: "[quote]"
...
Slide N (CTA): "[CTA text]"

PROFILE DETAILS:
- Name: [NAME]
- Handle: [HANDLE]
- Avatar: [description or URL]

Generate 3 visual style variations (different typography weight, quote placement, or subtle accent colors) so the user can choose their preferred look.
```

### Step 4: Finalize

- Poll `get-design-generation-job` until the job completes
- Show the generated candidates to the user
- Ask which candidate they prefer (or if they want adjustments)
- Once approved, use `export-design` to export the final design or provide the Canva edit link returned by the job so the user can fine-tune avatar, fonts, or any slide

---

## Slide Content Guidelines

### Cover Slide (Slide 1)
Use the most impactful quote of the set — this is what appears in the feed preview and determines whether someone swipes.

### Body Slides (Slides 2 – N-1)
- One idea per slide
- Short enough to read in 3 seconds
- Avoid bullet lists — transform them into individual slide quotes

### CTA Slide (Last Slide)
Always include a call-to-action slide. Examples:
- "Salva esse carrossel para não esquecer. 👇"
- "Segue para mais conteúdos como esse."
- "Compartilha com alguém que precisa ouvir isso."
- "Me conta nos comentários qual slide te tocou mais."

---

## Notes

- Default to **8 slides** unless the user specifies otherwise
- If the user provides a photo URL, pass it to the generation query as the avatar source
- The Twitter/X style works equally well for Portuguese, Spanish, and English content — match the quote language to the user's language
- After generating, remind the user they can use the `resize-for-social-media` skill to export the carousel to Facebook, LinkedIn, and other platforms
- This skill requires Claude Desktop with the native Canva connector configured. Required tools: `generate-design` and `get-design-generation-job`. If these are not available, ask the user to connect the Canva integration in Claude Desktop settings.
