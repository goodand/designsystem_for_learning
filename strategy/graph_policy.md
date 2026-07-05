# Graph Diagram Policy

## Purpose

Graph policy belongs inside animation policy. It decides what diagram structure to use before applying visual design.

## Diagram Selection

| Structure | Diagram | View Rule |
|---|---|---|
| simple sequence | `linear_pipeline` | 1 view |
| two sequential steps | `two_step_linear_pipeline` | 1 view |
| parallel branches then merge | `fork_join_parallel_pipeline` | 1 view |
| containment | `nested_box` or `tree` | zoom if depth >= 3 |
| pairwise comparison | `pairwise_relation` or `similarity_matrix` | zoom target pair/cell |
| transformation | `before_after_transform` | 1 view or staged reveal |
| cycle | `cycle_block` | zoom each cycle |
| hidden state / RNN | `recurrent_timestep_zoom` | zoom one timestep |

## One-View Conditions

Use one view when:

- input and output are clear
- direction is one-way
- no cycle
- no hidden state
- one comparison pair or less
- each procedure is understandable by role label

## Transition Count

For a linear root-to-leaf path with `N` nodes:

```text
transition_count = N - 1
```

If there are `M` cycles:

```text
transition_count = (N - 1) + M
```

This counts explanation transitions, not scene objects.

## Cycle Rule

Do not explain a cycle inside the full graph.

Use:

```text
show full graph
-> mark cycle
-> zoom cycle block
-> animate one iteration
-> return to full graph
```
