# Python-pptx Template for Consulting Slides

```python
import pptx
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.enum.text import PP_ALIGN
from pptx.dml.color import RGBColor

def create_consulting_slide():
    # 1. Create Presentation
    prs = Presentation()

    # 2. Define Layout (Title Only)
    slide_layout = prs.slide_layouts[5]
    slide = prs.slides.add_slide(slide_layout)

    # 3. Add Title (Lead Message)
    title = slide.shapes.title
    title.text = "Market Share Growth Strategy: Expanding into SEA Region"
    title.text_frame.paragraphs[0].font.size = Pt(24)
    title.text_frame.paragraphs[0].font.bold = True

    # 4. Add Subtitle / Kicker
    subtitle_box = slide.shapes.add_textbox(Inches(0.5), Inches(0.5), Inches(9), Inches(0.5))
    subtitle_p = subtitle_box.text_frame.add_paragraph()
    subtitle_p.text = "Targeting Vietnam & Indonesia as primary entry points due to high digital adoption."
    subtitle_p.font.size = Pt(14)
    subtitle_p.font.color.rgb = RGBColor(100, 100, 100) # Gray

    # 5. Add Content (e.g., Column Chart)
    # Note: Requires chart data
    from pptx.chart.data import CategoryChartData
    from pptx.enum.chart import XL_CHART_TYPE

    chart_data = CategoryChartData()
    chart_data.categories = ['2023', '2024', '2025(E)']
    chart_data.add_series('Revenue ($M)', (10.5, 15.2, 22.8))

    x, y, cx, cy = Inches(2), Inches(2), Inches(6), Inches(4.5)
    slide.shapes.add_chart(
        XL_CHART_TYPE.COLUMN_CLUSTERED, x, y, cx, cy, chart_data
    )

    # 6. Save
    output_path = "Strategy_Deck_v1.pptx"
    prs.save(output_path)
    print(f"Presentation saved to {output_path}")

if __name__ == "__main__":
    create_consulting_slide()
```

## Key Elements

1.  **Lead Message First**: Title serves as the main takeaway.
2.  **Clean Layout**: Use `Inches` to position elements precisely.
3.  **Data Visualization**: Use `CategoryChartData` for native charts (editable).
