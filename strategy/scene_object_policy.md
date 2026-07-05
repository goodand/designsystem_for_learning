# Scene Object Policy

## Scene Object Definition

A `scene_object` is a visible or tracked unit in an animation scene.

Examples:

- document card
- matrix
- vector
- comparison pair
- calculation node
- classification badge
- importance card
- collapsed block
- bottom state chip

## Object Budget

| Case | Object Budget |
|---|---:|
| simple input/output | 1-3 |
| default question | 4 |
| calculation/comparison | 5-6 |
| zoom needed | 8-12 |
| cycle/hidden state | 10+ allowed |

Visible objects per screen should stay at 3-5 or fewer.

## Pair Grouping

Treat comparison target A and B as one object:

```text
comparison_pair_object
```

This object includes:

- target A
- target B
- comparison relation line
- optional score/result marker

## Zoom Object Rule

Zoom can create more scene objects, but the current view should still expose only the active subset.

Use zoom for:

- cycle
- hidden state
- internal vector/matrix calculation
- multi-role block
- ambiguous calculation target

Avoid zoom for:

- simple linear pipeline
- simple parallel pipeline
- role-labeled two-step process
