# Design System Policy

## Purpose

Use a small reusable visual language. The design system defines the smallest repeated pieces: colors, shapes, arrows, state markers, and components.

## Top-Level Visual Layers

Directly map only 5 layers:

| Layer | Question | Main Channel |
|---|---|---|
| Topic Mode | lexical / semantic / hybrid? | 3-color palette |
| Relation Geometry | what static relation? | spatial layout, set/geometry notation |
| Process Flow | input / transform / calculation / output? | arrows, ports, timed reveal |
| Abstraction Scope | global / module / internal / calculation / formula? | slide order, zoom, breadcrumb |
| Disclosure State | open / collapsed / hidden? | bottom state bar, collapsed block |

Focus is not a top-level semantic mapping. Treat it as contextual UX.

## Topic Mode

| Value | Visual |
|---|---|
| lexical | primary color family |
| semantic | secondary color family |
| hybrid | tertiary color family |
| neutral | neutral color family |

Do not reuse color for focus, exactness, or input/output.

## Relation Geometry

| Family | Visual |
|---|---|
| identity/equivalence | same position, `=`, `≡` |
| similarity/proximity | nearby placement, partial overlap, `≈`, parallel direction |
| set/topology | nested box, Venn, `⊂`, `∩`, `∅` |
| difference/separation | separated lane, `≠`, `⟂` |

Use Relation Geometry for static relations only. Use Process Flow for transformations.

## Reusable Components

| Component | Meaning |
|---|---|
| `document_card` | original data or document chunk |
| `matrix_grid` | DTM, TF-IDF, similarity matrix |
| `vector_bar` | document vector, query vector, embedding |
| `calculation_node` | cosine, dot product, distance |
| `algorithm_block` | KNN, HNSW, ANN, RAG retriever |
| `collapsed_block` | role-only hidden block |
| `transform_arrow` | representation transformation |
| `comparison_arrow` | comparison between two targets |
| `flow_arrow` | process order |
| `output_list` | Top-k, recommendation, prediction |

## Secondary Channels

| Channel | Use |
|---|---|
| curvature | rounded for raw/human data, straight for structured/machine representation |
| solid/dotted | solid for direct/explicit, dotted for approximate/collapsed/shortcut |
| brightness/saturation | support or inactive state only |
| font type | ordinary explanation vs code/formula only |
| polygon angle count | optional complexity/performance hint |
| animation speed | optional exact vs approximate search contrast |
| size change | zoom interaction only, not importance |
