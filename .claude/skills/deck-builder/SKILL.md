---
name: deck-builder
description: Build Salesforce-branded HTML presentation decks for Kiana Parker — executive briefs, GIS survey results, global data storytelling, and cross-team presentations.
trigger: explicit — only build a deck when the user explicitly asks (e.g. "build me a deck", "create slides for...", "make a presentation on...")
---

# Deck Builder Skill

Kiana is a Sr. Executive Assistant supporting REWS Workplace Services leadership at Salesforce. She builds decks for executives and cross-functional partners. These presentations typically cover:

- **GIS / survey results** — global workplace data, utilization trends, employee sentiment
- **Global data storytelling** — synthesizing numbers across regions (AMER, EMEA, JAPAC, India) into a coherent narrative
- **Executive briefs** — concise, data-forward decks for SVP/VP audiences
- **Cross-team presentations** — REWS info sessions, leadership onsites, BOLDforce SF programs
- **Program recaps** — post-event summaries with attendance, highlights, and recommendations

---

## Output format

Produce a **native `.pptx` file** using Python and the `python-pptx` library.

- Save the file to the project root as `deck-[topic].pptx`
- Generate it by writing a Python script (`build-deck-[topic].py`) and running it with `python3`
- The resulting `.pptx` opens directly in PowerPoint, Keynote, or Google Slides
- Install the library if needed: `pip3 install python-pptx`
- Delete the build script after the `.pptx` is successfully generated — only keep the deck file

---

## Salesforce brand guidelines (apply to every deck)

**Colors:**
- Primary blue: `#0070D2` (Salesforce Cloud Blue)
- Dark navy: `#032D60` (Salesforce Navy)
- White: `#FFFFFF`
- Light gray background: `#F3F3F3`
- Accent / highlight: `#00A1E0` (lighter blue)
- Success green: `#4BBF6B`
- Warning amber: `#FFB75D`
- Text primary: `#181818`
- Text secondary: `#54698D`

**Typography:**
- Headlines: `Salesforce Sans`, falling back to `'Inter', sans-serif`
- Body: `Inter`, `-apple-system`, `sans-serif`
- Load Inter from Google Fonts

**Logo:**
- Represent the Salesforce brand with a simple SVG cloud mark inline — do not fetch external logo assets
- Place in top-left corner of title slide and bottom-left footer of all other slides

**Slide feel:**
- Clean, generous whitespace
- Data presented in styled stat cards, bar charts (CSS-only), or comparison tables — not raw bullet dumps
- Regional data shown in a grid layout (AMER / EMEA / JAPAC / India)
- Pull quotes from survey data styled as large callout blocks

---

## Slide structure to follow

Unless the user specifies otherwise, use this structure:

1. **Title slide** — deck title, subtitle, presenter name (ask if not provided), date
2. **Agenda / What we'll cover** — 3–5 bullets
3. **Context / Background** — why this data matters, framing the story
4. **Key findings** — 3–4 big stat cards with headlines (e.g. "87% of employees...")
5. **Regional breakdown** — 2×2 grid: AMER / EMEA / JAPAC / India (or whatever regions apply)
6. **Deep dive** — one or two slides on the most important trend or finding
7. **What we heard** — pull quotes or verbatim highlights from survey responses
8. **Recommendations / Next steps** — bulleted, owned, dated where possible
9. **Thank you / Q&A** — closing slide with Kiana's contact info

Adapt this structure based on the content. If the user says "this is a recap" or "this is a roadmap" adjust accordingly.

---

## How to gather inputs

When the user asks to build a deck, ask for:

1. **Topic / title** — what is this deck about?
2. **Audience** — who is presenting to whom? (e.g. "Sean presenting to Relina and the REWS LT")
3. **Key data or findings** — paste in the numbers, survey results, or bullet points to work from
4. **Any specific asks** — e.g. "emphasize the India data", "include a slide on next steps", "keep it to 8 slides"
5. **Presenter name and date** (for the title slide)

If the user provides raw data (CSV snippets, bullet points, survey percentages), synthesize them into the narrative — don't just reformat the input.

---

## python-pptx patterns to use

**Slide dimensions:** Widescreen 16:9 — `prs.slide_width = Inches(13.33)`, `prs.slide_height = Inches(7.5)`

**Title slide layout:** Dark navy (`#032D60`) full-bleed background, white title text (Salesforce Sans / Inter, 44pt bold), white subtitle (24pt), date bottom-right in light blue.

**Content slides:** White background, navy top bar (0.6" tall) with slide title in white. Body content below. Page number bottom-right in gray.

**Stat cards:** Use colored rectangles with large bold numbers (48pt, Salesforce Blue `#0070D2`) and a smaller label below (14pt, gray). Arrange 3–4 across a slide.

**Bar charts:** Use `pptx.util` and `pptx.chart` — prefer `BAR_CLUSTERED` chart type with Salesforce blue as the series fill. Always include data labels.

**Regional grid:** Four equal rectangles in a 2×2 grid. Each cell: region name (bold, navy, 16pt), big stat (blue, 36pt), one insight line (gray, 12pt).

**Pull quote:** Light blue (`#E8F4FD`) rectangle, italic text (18pt, navy), source attribution right-aligned below (12pt, gray).

**Footer on all slides:** Thin navy line at bottom. Left: "Salesforce Confidential" in gray 9pt. Right: slide number.

---

## Naming convention

Save the file as `deck-[short-topic].pptx` — e.g.:
- `deck-gis-q2-2026.pptx`
- `deck-rews-info-session.pptx`
- `deck-boldforce-recap-june.pptx`

After generating, tell the user the full path so they can open it directly.

---

## Tone and writing style

- Lead with the insight, not the methodology
- Use active voice: "Utilization increased" not "An increase in utilization was observed"
- Numbers first: "81% of respondents..." not "Most respondents (81%)..."
- Regional comparisons should highlight contrast, not just repeat data
- Recommendations should be specific and owned — "REWS to review Chicago staffing model by Q3" not "consider reviewing staffing"
