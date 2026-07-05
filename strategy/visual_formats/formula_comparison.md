# Formula Comparison Format

## Use When

- one formula is a transformation of another
- user needs common structure and differentia
- concept is easier through symbolic compression

## Pattern

```text
Base formula
Transformed formula
What changed
What stayed the same
```

## Examples

```text
Spearman(X, Y) = Pearson(rank(X), rank(Y))
cosine(A, B) = dot(A, B) / (||A|| ||B||)
```

## Tool Preference

- Markdown + KaTeX for most cases
- side-by-side table for comparison
- SVG only if formula parts need animated highlighting

## UX Rules

- Show formula after visual explanation.
- Highlight only the changed sub-expression.
- Pair every formula with a one-line verbal reading.
