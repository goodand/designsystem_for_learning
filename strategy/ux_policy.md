# UX Policy

## Core Rule

The user should always know what to look at, what is hidden, and why the current scene exists.

## Cognitive Principles

- One center object per scene.
- One change per animation beat.
- Use progressive disclosure.
- Keep the viewpoint stable.
- Hide or collapse irrelevant details; do not leave them faintly visible.
- Use formulas only after the visual structure is understood.
- Replay hard concepts as `example -> diagram -> formula -> example`.

## Focus Handling

Do not treat focus as a heavy analytical layer.

Use contextual focus cues:

- center placement
- sequential reveal
- thick border
- short pause
- bottom visibility state

Avoid labeling every object as focus/background.

## Bottom Visibility State

Use a small bottom bar to track:

| State | Meaning |
|---|---|
| `open` | currently expanded |
| `collapsed` | role label only |
| `hidden` | removed from body but tracked |
| `not_in_scene` | outside current scene |

The bottom bar should be quieter than the main diagram.

## Zoom Rules

Zoom only when:

- cycle exists
- hidden state exists
- matrix/vector internal calculation matters
- one block has multiple roles
- arrows may carry multiple meanings
- the user may confuse what is being calculated

Do not zoom simple linear or simple parallel pipelines.

## Canvas Density

Applies to every 16:9 animation canvas (1920×1080 reference).

- The **core object cluster** (center object + supporting objects + their connectors and labels) occupies **≥ 55% of the canvas area** at the busiest step of the scene.
- Outer padding: **≤ 5% per side** (≤ 96px at 1920×1080). Whitespace lives *between* objects, not around the composition.
- Minimum text sizes at 1080p: key values and formulas **≥ 32px**, body and labels **≥ 24px**, captions and the bottom state bar **≥ 20px**.
- Meet the floor by **scaling the cluster up** (or zooming in) — never by adding objects (the object budget in `scene_object_policy.md` still rules) or by decorative filler.

### Busiest-step check

Before shipping a scene:

1. Jump to the step with the most simultaneously visible objects.
2. Take the bounding box of the core cluster; divide by canvas area.
3. If < 55%, scale the cluster up until it passes.
4. Re-check the quietest step: a single center object should still read at ≥ 1/3 of canvas width.
