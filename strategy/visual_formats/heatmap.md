# Heatmap Format

## Use When

- numeric pattern matters more than exact values
- similarity matrix, attention matrix, hidden-state intensity

## Scene Objects

- heatmap grid
- color legend
- selected row/column/cell
- optional value tooltip

## Tool Preference

| Need | Tool |
|---|---|
| static heatmap | image, SVG, or table with color fills |
| interactive hover/filter | Plotly or D3 |
| animation over time | Canvas or SVG frames |

## UX Rules

- Provide a legend before interpretation.
- Use one highlighted row/cell when explaining calculation target.
- Use intensity only for value magnitude, not topic category.

## Avoid

- Do not combine topic colors with heatmap colors in the same grid.
