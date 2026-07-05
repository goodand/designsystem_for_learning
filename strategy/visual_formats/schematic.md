# Schematic Diagram Format

## Use When

- system architecture
- block-based process
- RAG pipeline
- module responsibility

## Scene Objects

- role blocks
- ports
- flow arrows
- collapsed internals
- output list

## Tool Preference

- Mermaid for simple block flow
- SVG/HTML for consistent design-system components
- presentation tool for lecture slides

## UX Rules

- Use 3-5 blocks in global view.
- Put role labels inside blocks.
- Hide internals until zoom.
- Use Process Flow for dynamic transformations.
- Use zoom only when the selected block's internal transformation, calculation, or comparison is the answer to the question.
- If the block's role label is enough to answer the question, keep the schematic as one view.
- For RAG-style diagrams, show the global pipeline first, then zoom only into the block that the question is actually about, such as `Retriever`, `Embedding`, or `ANN Search`.

## Schematic Zoom Decision

Use zoom when:

- one block has multiple internal roles
- input/output changes inside the block
- the calculation target is inside the block
- the user may confuse where a transformation happens
- showing internals in the global diagram would exceed 3-5 visible objects

Do not zoom when:

- the diagram is a simple `Input -> Process -> Output`
- the process is a simple linear pipeline
- the process is a simple fork-join pipeline
- the block name and one-line role label are enough

## Avoid

- Do not show all internals in the global architecture view.
- Do not create a zoom scene just because the block has internals. Zoom only if those internals are necessary for the question.
