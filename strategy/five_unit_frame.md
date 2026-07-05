# Five-Unit Explanation Frame

## Frame

Every question should be explainable through:

```text
데이터 -> 표현 -> 계산 대상 -> 개념 분류 -> 중요성
```

## Units

| Unit | Question | Output |
|---|---|---|
| 데이터 | 원래 무엇을 다루는가? | source data card |
| 표현 | 어떤 형식으로 바꾸는가? | set, matrix, vector, coordinate |
| 계산 대상 | 무엇과 무엇을 계산하는가? | pair object or selected row/cell |
| 개념 분류 | 어떤 범주에 속하는가? | topic/classification marker |
| 중요성 | 왜 필요한가? | usage, necessity, difference, strength |

## Default Scene Objects

Use 4 default objects:

1. `data_to_representation_object`
2. `calculation_or_comparison_object`
3. `classification_object`
4. `importance_object`

When there are two comparison targets, group them as one:

```text
comparison_pair_object = target A + target B + relation/comparison marker
```

## Importance Subfields

Always include:

- `usage`: where it is used
- `necessity`: why it is needed
- `difference`: what it differs from
- `strength`: where it is strong
