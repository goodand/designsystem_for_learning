# Visual Strategy Router

> **Entry point for the visual strategy layer.**
> This file is the router. HTML artifacts link here (via an `@visual-strategy` comment
> or a `<link rel="visual-strategy" href="…/strategy/router.md">` tag); from here you
> route to the exact policy and format spec that governs a scene.

The **visual strategy is managed in Markdown**, separate from the CSS tokens and HTML
components. CSS/HTML answer *"what does a swatch/button/canvas look like"*; these
Markdown files answer *"which visual format, layout, and motion should encode this
concept, and why."* Keep them decoupled: a scene's look is assembled from tokens +
components, but the **decision** of how to visualize is made here.

---

## How an HTML artifact connects to strategy

Every visual output (UI kit screen, animation canvas, slide) declares the strategy it
implements with a comment block placed right after the `@dsCard` line, plus a machine
-readable `<link>`:

```html
<!-- @dsCard group="Animation UI" viewport="700x400" name="…" -->
<!-- @visual-strategy
     router:   strategy/router.md
     layers:   strategy/design_system.md
     policies: strategy/ux_policy.md, strategy/scene_object_policy.md
     formats:  strategy/visual_formats/xy_coordinate.md, strategy/visual_formats/matrix.md
-->
<link rel="visual-strategy" href="../strategy/router.md">
```

- **`router`** — always this file (single entry point).
- **`layers`** — the 5-layer visual language (`design_system.md`).
- **`policies`** — the UX / scene-object / frame policies that constrain the scene.
- **`formats`** — the one main visual format (plus optional secondary) actually used.

A reader (human or agent) opens the HTML, sees which MD files govern it, and jumps
straight to them. No visual decision is hard-coded only in CSS/HTML — it always traces
back to a Markdown spec.

---

## Decision flow

```text
concept / question
  → 1. Frame it            (five_unit_frame.md)      데이터→표현→계산 대상→개념 분류→중요성
  → 2. Map the 5 layers    (design_system.md)        Topic / Relation / Process / Abstraction / Disclosure
  → 3. Route to a format   (visual_formats.md)       xy / matrix / heatmap / graph / zoom / …
  → 4. Read ONE format spec(visual_formats/<x>.md)   scene objects, tool, UX rules, avoid
  → 5. Apply UX + budget   (ux_policy.md, scene_object_policy.md)
  → 6. Assemble with tokens + components (styles.css, components/)
```

Choose the concept need first. Read **only** the matching format file. Keep **one main
format per scene**; a secondary format is allowed only for a formula lock or importance
summary.

---

## Strategy files

### Core policy layer (domain-agnostic)
| File | Governs |
|---|---|
| [`design_system.md`](design_system.md) | The 5 top-level visual layers + reusable components + secondary channels |
| [`five_unit_frame.md`](five_unit_frame.md) | The 데이터→표현→계산→분류→중요성 explanation frame + default scene objects |
| [`ux_policy.md`](ux_policy.md) | Cognitive rules, focus handling, bottom visibility state, zoom rules |
| [`scene_object_policy.md`](scene_object_policy.md) | What a scene object is + object budget per scene type |
| [`graph_policy.md`](graph_policy.md) | Which diagram structure to use before visual design; cycle/transition rules |
| [`motion_runtime.md`](motion_runtime.md) | **Motion runtime** — export-bound motion = JS timer tweens reading `tokens/animation.css`; CSS transitions for live micro-interactions only |

### Format router + specs
| File | Governs |
|---|---|
| [`visual_formats.md`](visual_formats.md) | **Format router** — concept → format → which spec to read → tool/framework |
| [`visual_formats/xy_coordinate.md`](visual_formats/xy_coordinate.md) | distance, direction, angle, cluster, KNN, cosine/Euclidean intuition |
| [`visual_formats/xy_comparison.md`](visual_formats/xy_comparison.md) | Euclidean vs cosine, before/after normalization, raw vs unit vector |
| [`visual_formats/matrix.md`](visual_formats/matrix.md) | DTM, TF-IDF, row/column/cell, pairwise similarity matrix |
| [`visual_formats/heatmap.md`](visual_formats/heatmap.md) | numeric pattern, similarity/attention/hidden-state intensity |
| [`visual_formats/quadrant.md`](visual_formats/quadrant.md) | concept positioning by two axes, strategy comparison |
| [`visual_formats/formula_comparison.md`](visual_formats/formula_comparison.md) | one formula as a transformation of another; common structure + differentia |
| [`visual_formats/zoom.md`](visual_formats/zoom.md) | global→module→internal→calculation→formula; block internals |
| [`visual_formats/one_point_animation.md`](visual_formats/one_point_animation.md) | one change is the lesson (normalization, row-pair select, query enters retriever) |
| [`visual_formats/schematic.md`](visual_formats/schematic.md) | system architecture, RAG pipeline, module responsibility |
| [`visual_formats/graph.md`](visual_formats/graph.md) | nodes, edges, cycles, hierarchy, DAGs, pipelines |
| [`visual_formats/venn.md`](visual_formats/venn.md) | set overlap, intersection/union, Jaccard — true-lens geometry rule, achromatic hatch fill |

### Domain policy layer (swappable — Text Similarity example)
These are **domain-specific** policies, not core. They show how the core layer is
specialized for one domain. Swap this folder per domain.
| File | Governs |
|---|---|
| [`domains/text-similarity/SKILL.md`](domains/text-similarity/SKILL.md) | Domain skill router — routes a concept question to the reference policies below |
| [`domains/text-similarity/design.md`](domains/text-similarity/design.md) | Full 14-section visual design system specialized for Text Similarity |
| [`domains/text-similarity/animation_policy.md`](domains/text-similarity/animation_policy.md) | Animation output contract, scene budget, graph/view/zoom/cycle/formula policy |

### Example Instances
Concrete scene plans for individual questions — the **test cases** that validate the
system. See [`../examples/`](../examples/):
- `examples/scene_plans/unit_01…05_animation_scene_plan.json` — real per-question scene-object plans
- `examples/scene-plan-unit01.html` — one plan rendered as a storyboard with the design system

---

## How strategy maps onto the token system

The Markdown layers are the **decision**; these token groups are the **implementation**.

| Strategy layer (MD) | Token / component (CSS/JSX) |
|---|---|
| Topic Mode (`design_system.md`) | Topic slots in `tokens/modes.css` + a profile in `domain-profiles/` |
| Relation Geometry | `--relation-*` tokens in `tokens/modes.css` |
| Process Flow | `--process-*` tokens |
| Abstraction Scope (incl. **zoom**) | `--abstraction-*` tokens |
| Disclosure State | `--disclosure-*` tokens |
| Representation (5-unit frame) | `--repr-*` tokens |
| Reusable components (`document_card`, `matrix_grid`, `vector_bar`, …) | `components/` primitives + canvas patterns |

> **Reminder:** `lexical / semantic / hybrid`, `supervised / unsupervised`, etc. are
> *domain profile values*, not universal categories. The provided question set and Topic
> Mode are domain-specific instances used to validate this reusable system — see
> `../README.md`.
