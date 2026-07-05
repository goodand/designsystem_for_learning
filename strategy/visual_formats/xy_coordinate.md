# XY Coordinate Format

## Use When

- distance, direction, angle, boundary, cluster, nearest neighbor
- KNN, Euclidean distance, cosine direction intuition

## Scene Objects

- coordinate plane
- point/vector A
- point/vector B
- optional distance line or angle arc
- calculation label

## Tool Preference

| Need | Tool |
|---|---|
| simple static explanation | SVG or Mermaid-like schematic |
| precise axes and coordinates | SVG/HTML |
| interactive sliders or animation | HTML + SVG/Canvas |

## UX Rules

- Keep visible points under 5 unless showing clusters.
- Show either distance line or angle arc first, not both at once.
- For cosine, emphasize direction/angle.
- For Euclidean, emphasize endpoint-to-endpoint diagonal.

## Avoid

- Do not use XY when the data is actually high-dimensional unless it is clearly labeled as a simplified projection.
