# Visual Format Router

## Purpose

Route the concept to the right visual expression format. Do not load every format reference by default.

## Routing Table

| User Need | Format | Read |
|---|---|---|
| distance, direction, cluster, boundary | XY coordinate | `visual_formats/xy_coordinate.md` |
| compare two coordinate interpretations | XY comparison | `visual_formats/xy_comparison.md` |
| DTM, TF-IDF, row/column/cell | matrix | `visual_formats/matrix.md` |
| numeric pattern or similarity scores | heatmap | `visual_formats/heatmap.md` |
| set overlap, intersection/union, Jaccard | Venn / set diagram | `visual_formats/venn.md` |
| concept position by two axes | quadrant/table | `visual_formats/quadrant.md` |
| formulas share a structure | formula comparison | `visual_formats/formula_comparison.md` |
| global-to-local explanation | zoom | `visual_formats/zoom.md` |
| one change should be emphasized | one-point animation | `visual_formats/one_point_animation.md` |
| system architecture or block layout | schematic diagram | `visual_formats/schematic.md` |
| nodes, edges, hierarchy, cycle, pipeline | graph diagram | `visual_formats/graph.md` |

## Tool/Framework Routing

| Output Need | Prefer |
|---|---|
| simple static relationship diagram | Mermaid |
| precise custom diagram | SVG or HTML/CSS |
| interactive coordinate/matrix/heatmap | HTML + SVG/Canvas, Plotly, D3 |
| formula-heavy comparison | Markdown table + KaTeX |
| animation storyboard | structured JSON or slide-by-slide markdown |
| production animation | SVG/HTML/CSS animation, Canvas, or presentation tool |

## Selection Rule

1. Choose the concept need first.
2. Read only the matching format file.
3. Choose the tool/framework after deciding the format.
4. Keep one main format per scene. Use a secondary format only for formula lock or importance summary.
