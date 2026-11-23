# Presentation & Diagram Architect

A production-grade AI Agent Skill synthesized via **Meta-Skill Synthesizer** for creating Canva-ready presentations (`.pptx`), native Draw.io diagrams (`.drawio` + `.png`), and curated royalty-free visual decor.

---

## Directory Structure

```text
presentation-diagram-architect/
├── SKILL.md                                   # Core agent instructions & stage-gate pipeline
├── README.md                                  # Overview, synthesis provenance & usage guide
├── references/
│   └── drawio-xml-and-pptx-patterns.md        # Draw.io mxGraph & python-pptx code recipes
└── checklists/
    └── pre-flight-deck-audit.md               # Pre-delivery verification rubric
```

---

## Synthesis Provenance Matrix

| Source Skill / Repository | Strengths Extracted | Limitations Identified | Mitigations Engineered |
| :--- | :--- | :--- | :--- |
| `bahayonghang/drawio-skills@drawio` | Structured diagram specs, clean layout discipline | Heavy YAML intermediate boilerplate for quick decks | Direct Python `mxGraph` XML builder with deterministic grid coordinates |
| `jgraph/drawio-mcp@drawio` | Native `.drawio` XML & `drawio` CLI export workflow | Assumes MCP server availability; Windows path quoting gaps | Local `draw.io.exe` CLI invocation with explicit quoted path handling |
| `ailabs-393/ai-labs-claude-skills@pitch-deck` | Strong narrative arc & investor/demo slide pacing | No automated `.pptx` generation or diagram embedding | `python-pptx` 16:9 card engine with proportional image fitting |
| `tfriedel/claude-office-skills@pptx` | Programmatic `.pptx` styling and shape primitives | Lacks Canva portability guidance and stock image checks | Standard font tokens (`Segoe UI`), Canva upload workflow, Pillow validation |
| `peter-duffy95/open-images-for-free-use-skill` | Royalty-free stock sourcing from open repositories | Susceptible to Wikimedia HTTP 429 rate limits | Unsplash/local asset fallback & automated Pillow integrity check |

---

## Prerequisites & Dependencies

- **Python 3.10+** with `python-pptx` and `Pillow` (MIT/HPND open-source licenses)
- **Draw.io Desktop** (`draw.io.exe`, Apache-2.0) for headless PNG/SVG export
- *(Optional)* **Canva CLI** (`@canva/cli`, requires Node.js v24 & npm v11) for direct Canva Connect API workflows

---

## Usage Guide

1. Invoke this skill when asked to build a project presentation, pitch deck, or system architecture diagrams.
2. Follow the 4-stage pipeline in `SKILL.md` (`Audit` -> `Draw.io` -> `Decor` -> `.pptx` Assembly).
3. Upload the generated `.pptx` file directly to **Canva** (`Upload` -> `.pptx`) to edit slides or apply Canva templates seamlessly.
