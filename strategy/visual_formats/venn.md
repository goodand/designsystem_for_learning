# Venn / Set Diagram Format

## Use When

- set membership, overlap, disjoint, containment
- Jaccard: intersection vs union
- shared vs unique tokens between two documents
- lexical set comparison before matrix/vector representations

## Scene Objects

- set circles (2 default, max 3)
- intersection lens
- element chips (tokens, documents) placed inside regions
- region labels + counts (`|A ∩ B|`, `|A ∪ B|`)

## Geometry Rule (non-negotiable)

**The intersection is never approximated with a separate shape** (ellipse, rounded
rect, blob). Render the *true* overlap region: one circle clipped by the other — the
lens IS the geometry. If the circles move, the lens follows automatically.

SVG recipe:

```svg
<defs>
  <clipPath id="clipB"><circle cx="(B)" cy="(B)" r="(B)"/></clipPath>
  <pattern id="hatch" width="8" height="8" patternTransform="rotate(45)"
           patternUnits="userSpaceOnUse">
    <!-- 8 = --relation-venn-hatch-gap, rotate(45) = --relation-venn-hatch-angle -->
    <line x1="0" y1="0" x2="0" y2="8"
          style="stroke: var(--relation-venn-hatch-stroke);
                 stroke-width: var(--relation-venn-hatch-width)"/>
  </pattern>
</defs>
<!-- circle A redrawn, clipped by circle B = exact lens -->
<circle cx="(A)" cy="(A)" r="(A)" clip-path="url(#clipB)" fill="url(#hatch)"/>
```

## Fill

The intersection fill is **achromatic** — Relation owns no color (token ownership).

- **Primary: hatch** — `--relation-venn-hatch-angle` (45deg), `--relation-venn-hatch-gap`
  (8px), `--relation-venn-hatch-width` (1.5px), `--relation-venn-hatch-stroke` (slate)
- Alternative: flat `--relation-venn-fill` at `--relation-venn-opacity`
- Circle rings: `--relation-venn-ring`

Set circles may carry topic color on their **ring or label** when the sets themselves
are topic-classified (doc A vs doc B) — the lens never does.

## UX Rules

- Two sets by default; three only when three-way overlap is the question.
- Animate elements *moving into* regions before filling the lens (JS tween — see
  `strategy/motion_runtime.md`).
- Label the lens with the operation (`∩`), not an interpretation.
- Pair with `formula_comparison` only to lock Jaccard as a formula.

## Avoid

- approximated intersection shapes (the original sin this spec exists to prevent)
- topic color inside the lens
- more than 3 sets
- using Venn for process/flow — that is `schematic` / `graph`
