# Zoom Format

## Use When

- global-to-local explanation
- block internals matter
- cycle, hidden state, matrix/vector calculation
- a schematic block's internal role is the answer to the question

## Zoom Levels

```text
global -> module -> internal -> calculation -> formula
```

## Tool Preference

- presentation slides for step zoom
- HTML/SVG for interactive map-like zoom
- animation storyboard for planning

## UX Rules

- Start with 3-5 collapsed role blocks.
- Open only the selected block.
- Keep a breadcrumb or bottom state.
- Return to global after explaining the zoomed part.
- Treat zoom as a question-answering tool, not a default decoration.
- If the global block label answers the question, do not zoom.
- If the user needs to know what happens inside the block, zoom into only that block.

## Avoid

- Do not zoom simple linear or simple parallel pipelines.
- Do not zoom every block in a schematic. Zoom the minimum block whose internals are necessary.
