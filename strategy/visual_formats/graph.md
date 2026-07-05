# Graph Diagram Format

## Use When

- nodes, edges, cycles, hierarchy, DAGs, pipelines
- tree structure or recurrent structure

## Topology Axes

Use only when needed:

- Edge presence
- Directionality
- Cycle presence

## Tool Preference

| Need | Tool |
|---|---|
| simple DAG/tree/pipeline | Mermaid |
| custom geometry or visual consistency | SVG/HTML |
| interactive graph | D3 or Cytoscape-style graph library |
| graph animation | SVG/Canvas |

## Diagram Choices

| Structure | Diagram |
|---|---|
| sequence | linear pipeline |
| parallel branches | fork-join pipeline |
| containment | tree or nested boxes |
| pairwise relation | edge between two nodes or matrix |
| cycle | cycle block + zoom |

## UX Rules

- Use graph only when relationships matter.
- If cycle exists, mark it in full view, then zoom into the cycle.
- Do not explain cycle internals inside the full graph.
- Keep horizontal nodes to 5 or fewer.
