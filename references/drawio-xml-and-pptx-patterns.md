# Draw.io XML & python-pptx Reference Patterns

## 1. Native Draw.io (`mxGraph`) XML Primitives

Use a deterministic coordinate grid with $\ge 40\text{px}$ horizontal and $\ge 35\text{px}$ vertical spacing:

```python
from xml.sax.saxutils import escape

def make_mxfile(name: str, cells_xml: str, width: int = 1100, height: int = 650) -> str:
    return f"""<mxfile host="app.diagrams.net" agent="Diagram-Architect" version="24.7.17">
  <diagram id="{name}" name="{name}">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="{width}" pageHeight="{height}" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
{cells_xml}
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>"""
```

### Windows CLI Export (`draw.io.exe`)
Always quote paths containing spaces when invoking `draw.io.exe` via PowerShell `Start-Process`:

```powershell
$in  = "`"C:\path\with spaces\diagram.drawio`""
$out = "`"C:\path\with spaces\diagram.png`""
Start-Process -FilePath "C:\Program Files\draw.io\draw.io.exe" -ArgumentList '-x', '-f', 'png', '-o', $out, $in -Wait -PassThru
```

---

## 2. Proportional Image Fitting (`python-pptx`)

Never pass arbitrary `width` and `height` together without preserving aspect ratio:

```python
from PIL import Image
from pptx.util import Inches

def add_pic_fit(slide, path: str, x: float, y: float, max_w: float, max_h: float) -> None:
    with Image.open(path) as im:
        iw, ih = im.size
    ratio = min(max_w / iw, max_h / ih)
    w, h = iw * ratio, ih * ratio
    px = x + (max_w - w) / 2
    py = y + (max_h - h) / 2
    slide.shapes.add_picture(path, Inches(px), Inches(py), width=Inches(w), height=Inches(h))
```

---

## 3. Canva `.pptx` Import Best Practices

- Keep slide dimensions at standard widescreen `13.333 x 7.5` inches (16:9).
- Avoid complex PowerPoint animations or SmartArt; use native `ROUNDED_RECTANGLE`, `TEXT_BOX`, and embedded `.png`/`.jpg` assets so Canva converts every element into editable layers.
- Limit body copy to $\le 35$ words per card to prevent text overflow when Canva substitutes web fonts.
