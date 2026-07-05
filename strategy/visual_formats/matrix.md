# Matrix Format

## Use When

- DTM, TF-IDF, document-term matrix
- row vector selection
- pairwise similarity matrix shape

## Scene Objects

- matrix grid
- row highlight
- column highlight
- selected cell or selected row pair
- row/column labels

## Tool Preference

| Need | Tool |
|---|---|
| small explanatory matrix | Markdown table |
| styled matrix with highlights | HTML/CSS or SVG |
| animated row/cell selection | HTML/SVG |

## UX Rules

- Start with a tiny matrix, not the real full size.
- Explain row, column, value before any calculation.
- For cosine over TF-IDF, highlight row_i and row_j as one `comparison_pair_object`.
- Use the real shape as a label, e.g. `(20000, 47487)`, not as a full drawn matrix.

## Avoid

- Do not show large dense matrices unless converted to a heatmap.
