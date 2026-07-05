# XY Comparison Format

## Use When

- comparing Euclidean vs cosine
- before/after normalization
- raw vector vs unit vector

## Layout

Use left/right or top/bottom contrast:

```text
Before / Euclidean / raw space
After  / Cosine    / normalized space
```

## Tool Preference

- SVG/HTML for precise paired diagrams
- presentation slide with two panels for static teaching
- Canvas only if many animated points are needed

## UX Rules

- Use identical axes layout in both panels.
- Move only one visual variable between panels.
- Keep the same vector colors across panels.

## Formula Lock

Use after visual:

```text
||A - B||^2 = 2 - 2cos(theta)  when ||A|| = ||B|| = 1
```
