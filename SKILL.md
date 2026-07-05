---
name: chuk-design
description: Use this skill to generate well-branded ML/DL educational animations and interfaces for 축(Chuk), either for production or throwaway prototypes/mocks/etc. Contains essential design guidelines, colors, type, fonts, assets, structural mode system, visual-strategy (Markdown) router, and UI kit components. Built on the DaleStudy/daleui open-source foundation with Korean typography support.
user-invocable: true
---

Read the README.md file within this skill, and explore the other available files.

Key architectural principle: The design system separates **fixed structural axes** (Relation, Process, Abstraction, Disclosure, Representation modes) from **configurable domain profiles** (Topic Mode). Never hardcode domain-specific concepts (like "lexical", "semantic") as universal categories — use the Topic Mode slot system in `tokens/modes.css` and load a domain profile from `domain-profiles/`.

If creating visual artifacts (slides, mocks, throwaway prototypes, animations):
1. Copy assets out and create static HTML files
2. Link `styles.css` for tokens
3. Load a domain profile CSS if working with a specific topic
4. Use the structural modes to encode concept relationships, process stages, zoom levels, and visibility states

If working on production code:
1. Copy assets and read the token CSS files
2. Import component implementations from `components/`
3. Follow the visual foundations in README.md

If the user invokes this skill without any other guidance, ask them what they want to build or design, ask some questions, and act as an expert designer who outputs HTML artifacts _or_ production code, depending on the need.

## Key files to read first
- `README.md` — Full design system documentation
- `strategy/router.md` — **Visual strategy entry point (router)** — routes to policies + format specs
- `tokens/modes.css` — Fixed structural axes and configurable Topic Mode
- `tokens/colors.css` — Color system
- `tokens/typography.css` — Font system
- `domain-profiles/` — Example domain configurations (CSS)
- `strategy/domains/` — Domain-specific policy (Markdown)
- `examples/` — Example Instances (real scene plans + rendered storyboard)

## Visual strategy is managed in Markdown
Look/feel comes from tokens + components (CSS/JSX). The **decision of how to visualize a
concept** is made in `strategy/*.md`. Every HTML output declares its governing specs with
an `<!-- @visual-strategy -->` comment + `<link rel="visual-strategy">` pointing at
`strategy/router.md`. When creating a new animation/scene, start at the router, follow the
decision flow, and read only the one matching format spec.
