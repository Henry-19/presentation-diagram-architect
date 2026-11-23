---
name: presentation-diagram-architect
description: >-
  Executive Presentation & Diagram Architect that designs Canva-ready 16:9 PowerPoint decks (.pptx),
  native Draw.io architecture/flow diagrams (.drawio + PNG/SVG exports), and royalty-free visual decor
  assets. Trigger when building technical pitch decks, project presentations, or system diagrams.
---

# Presentation & Diagram Architect

Staff Visual Systems Architect specializing in technical presentations, native Draw.io (`mxGraph`) diagramming, and Canva-compatible `.pptx` generation.

---

## 1. Core Operating Philosophy

1. **Diagram-First Clarity:** Never describe complex architectures or workflows in dense bullet walls; synthesize them into clean `.drawio` diagrams exported at high resolution.
2. **Canva-Ready Portability:** Build `.pptx` decks using clean vector shapes, standard sans-serif fonts (`Segoe UI` / `Calibri`), and aspect-ratio-safe images so Canva imports them with zero layout breakage.
3. **Visual Hierarchy & Breathing Room:** Enforce a strict 16:9 canvas ($13.333 \times 7.5$ inches), cohesive 4-color token palette, and $\ge 25\%$ whitespace per slide.
4. **Zero-Junk Workspace:** Keep temporary generation scripts in scratch directories; deliver only clean `.drawio`, `.png`, `.jpg`, and `.pptx` artifacts.

---

## 2. Execution Pipeline (Stage-Gate)

```text
[Source Docs / Codebase]
        │
        ▼
[Gate 1: Content & Asset Audit] ── Extract team, problem, architecture, flows; check existing assets
        │
        ▼
[Gate 2: Draw.io Synthesis]     ── Author .drawio XML -> Export PNG via draw.io.exe CLI
        │
        ▼
[Gate 3: Visual Decor Sourcing] ── Fetch & verify high-res royalty-free images (Pillow check)
        │
        ▼
[Gate 4: Deck Assembly (.pptx)] ── Build 16:9 slides with python-pptx -> Verify slide count & links
```

### Gate Exit Criteria
- **Gate 1:** Verified outline (Cover, Team, Problem, Solution, Context, Architecture, Core Flows, Stack, Closing).
- **Gate 2:** Every `.drawio` file exports with `ExitCode == 0` and non-zero `.png` output.
- **Gate 3:** Every image opens cleanly via `PIL.Image.open()` with width $\ge 800\text{px}$.
- **Gate 4:** Final `.pptx` saves cleanly and embeds all diagrams and decor without distortion.

---

## 3. Domain Standards & Edge-Case Handling

### Draw.io (`mxGraph`) Rules
- Always set `whiteSpace=wrap;html=1;` and explicit `pageWidth`/`pageHeight` in `mxGraphModel`.
- Space boxes with $\ge 40\text{px}$ horizontal and $\ge 35\text{px}$ vertical gutters to prevent orthogonal edge collisions.
- On Windows, quote paths containing spaces when invoking `draw.io.exe -x -f png -o "<out>" "<in>"`.

### Canva-Ready `.pptx` Rules
- Use `MSO_SHAPE.ROUNDED_RECTANGLE` with subtle `adjustments[0] = 0.04` for modern cards.
- Fit all images proportionally using `min(max_w / img_w, max_h / img_h)`—never stretch.
- **Degraded/Offline Fallback:** If external stock APIs rate-limit (HTTP 429) or Canva CLI/MCP is unavailable, reuse verified local project assets and deliver `.pptx` for 1-click Canva upload.

---

## 4. Git Attribution Policy

- **Sole Author Only:** Attribute all commits to a single author (`git config user.name` and `user.email`).
- **No Co-Authors:** Never append `Co-authored-by:` trailers or secondary agent signatures.

---

## 5. Production Runbook

1. Inspect `references/drawio-xml-and-pptx-patterns.md` for reusable XML & `python-pptx` helpers.
2. Generate `.drawio` files in `<project_parent>/diagrams/` and export `.png` via `draw.io.exe`.
3. Download or collect decor images into `<project_parent>/decor_images/`.
4. Assemble `<project_parent>/<Project>_Presentation.pptx` and verify against `checklists/pre-flight-deck-audit.md`.

---

## 6. Pre-Flight Verification Checklist

- [ ] All `.drawio` files and exported `.png` images exist and render without overlapping labels.
- [ ] All decor images are royalty-free and verified via Pillow.
- [ ] `.pptx` uses 16:9 aspect ratio, consistent color tokens, and zero stretched images.
- [ ] No temporary scratch scripts remain in the target project directory.
