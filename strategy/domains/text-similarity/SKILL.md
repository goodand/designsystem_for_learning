---
name: text-similarity-animation
description: Use this skill when creating animation storyboards, graph diagrams, scene-object plans, or visual explanation flows for Text Similarity, RAG, KNN, NNS/ANN, TF-IDF, Jaccard, cosine similarity, lexical/semantic comparison, and related ML concepts. It routes the task to focused reference policies for UX, design system, five-unit explanation, visual formats, graph policy, and scene-object planning.
---

# Text Similarity Animation Skill

## Role

Convert a concept question into an animation-ready plan.

This main skill is a router and common policy. Load only the reference files needed for the request.

## Common Output Contract

For each question, produce:

```json
{
  "question": "...",
  "five_unit_frame": {},
  "visual_format": "...",
  "graph_policy": {},
  "scene_objects": [],
  "animation_steps": [],
  "zoom_policy": {},
  "formula_lock": "...",
  "importance_frame": "..."
}
```

## Common UX Policy

Always follow these rules:

- One center object per scene.
- Show 3-5 visible objects at most.
- Hide or collapse irrelevant objects instead of fading them.
- Use bottom visibility state for `open`, `collapsed`, `hidden`, and `not_in_scene`.
- Use zoom only when needed: cycle, hidden state, matrix/vector internal calculation, multi-role block, or ambiguous calculation target.
- Show formulas after the visual flow, not before it.
- Use relation geometry for static relationships; use process flow for dynamic transformations.

For full UX rules, read [references/ux_policy.md](references/ux_policy.md).

## Design System Routing

Use the visual design system for recurring shapes, colors, arrows, state bars, and relation symbols.

Read [references/design_system.md](references/design_system.md) when:

- choosing colors, shapes, arrows, lines, or state markers
- mapping visual channels to classification layers
- defining the legend before drawing
- distinguishing Topic Mode, Relation Geometry, Process Flow, Abstraction Scope, and Disclosure State

## Five-Unit Explanation Routing

Every concept explanation should be organized by:

```text
데이터 -> 표현 -> 계산 대상 -> 개념 분류 -> 중요성
```

Read [references/five_unit_frame.md](references/five_unit_frame.md) when:

- chunking a question into explanation units
- deciding the minimum scene objects
- writing the explanation table for a question
- attaching usage, necessity, difference, and strength

## Visual Format Routing

Read [references/visual_formats.md](references/visual_formats.md) when choosing among:

- XY 좌표계
- XY 좌표계 대조
- 행렬
- 히트맵
- 2분면/4분면 대조표
- 유사 수식 비교
- 줌
- 원 포인트 애니메이션
- 도면형 도식
- graph형 도식

## Graph Policy Routing

Read [references/graph_policy.md](references/graph_policy.md) when:

- drawing pipelines, trees, DAGs, cycles, fork-join structures, or pairwise comparisons
- deciding whether one view is enough
- applying `N - 1` transition logic
- handling cycle zooms

## Scene Object Routing

Read [references/scene_object_policy.md](references/scene_object_policy.md) when:

- estimating scene object count
- grouping comparison target A/B as one `comparison_pair_object`
- deciding zoom object budget
- planning bottom visibility states

## Minimal Workflow

1. Identify the question type.
2. Fill the five-unit frame.
3. Choose the visual format.
4. Choose graph policy only if graph structure matters.
5. Estimate scene objects.
6. Apply UX and design system rules.
7. Produce the animation plan.

## Final Checks

- Did the output map one user instruction to one scene decision?
- Did it avoid unnecessary zoom?
- Did it keep simple linear/parallel pipelines in one view?
- Did it separate graph policy from design system?
- Did it link the needed reference policy?
