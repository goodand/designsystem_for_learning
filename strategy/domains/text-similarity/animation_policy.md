# Text Similarity Animation Policy

## Purpose

이 문서는 Text Similarity 개념 설명을 위한 애니메이션 산출 정책이다.

`design.md`가 색상, 도형, 화살표, 컴포넌트 같은 작은 조각의 일관된 체계라면, 이 문서는 사용자의 질문을 받아 실제 장면, 그래프 도식, 줌, 애니메이션 흐름으로 변환하는 실행 정책이다.

핵심 목표는 다음과 같다.

- 지시와 산출이 1:1로 대응되게 한다.
- 그래프 도식화 정책을 애니메이션 정책 안에 포함한다.
- 한 화면에 너무 많은 객체를 노출하지 않는다.
- 단순 구조는 1 view로 처리하고, 복잡한 구조만 zoom한다.

## Input Contract

애니메이션 산출 지시는 아래 중 하나 이상의 입력을 받는다.

| Input | Meaning |
|---|---|
| `question` | 설명해야 할 질문 |
| `concepts` | 등장 개념 목록 |
| `process` | 입력, 변환, 계산, 출력 흐름 |
| `relation` | 개념 간 관계 |
| `formula` | 필요할 때 고정할 수식 |
| `importance` | 용도, 필요성, 차이점, 강점 |

## Output Contract

각 질문은 아래 구조로 산출한다.

```json
{
  "question": "...",
  "scene_type": "...",
  "view_count": 1,
  "scene_objects": [],
  "graph_diagram_policy": {},
  "animation_steps": [],
  "zoom_policy": {},
  "formula_lock": "...",
  "importance_frame": "..."
}
```

## Five-Unit Explanation Frame

질문 1개는 기본적으로 아래 5단위로 설명한다.

```text
데이터 -> 표현 -> 계산 대상 -> 개념 분류 -> 중요성
```

기본 scene object는 4개를 목표로 한다.

| Object | Role |
|---|---|
| `data_to_representation_object` | 원본 데이터가 표현으로 바뀌는 장면 |
| `calculation_or_comparison_object` | 계산 대상 또는 비교 대상 쌍 |
| `classification_object` | lexical/semantic/ML 등 개념 위치 |
| `importance_object` | 용도, 필요성, 차이점, 강점 |

비교 대상 A/B는 별도 객체 2개가 아니라 `comparison_pair_object` 하나로 묶는다.

## Scene Object Budget

| Case | Recommended Object Count |
|---|---:|
| 단순 입력 -> 출력 | 1-3 |
| 기본 질문 설명 | 4 |
| 계산/비교 포함 | 5-6 |
| zoom 포함 | 8-12 |
| cycle/hidden state 포함 | 10+ 가능 |

한 화면에 노출되는 주요 객체는 3-5개 이하로 유지한다.

## Graph Diagram Policy

그래프 도식화는 애니메이션 정책 안에서 결정한다.

| Structure | Diagram Type | View Policy |
|---|---|---|
| 단순 순차 절차 | `linear_pipeline` | 1 view |
| 두 절차 순차 처리 | `two_step_linear_pipeline` | 1 view |
| 병렬 처리 후 결합 | `fork_join_parallel_pipeline` | 1 view |
| 포함관계 | `nested_box` 또는 `tree` | 깊이 3 이상이면 zoom |
| 상호 비교 | `pairwise_relation` 또는 `similarity_matrix` | 계산 대상만 zoom |
| 변환 과정 | `before_after_transform` | 1 view 또는 단계 reveal |
| cycle | `cycle_block` + zoom | cycle마다 별도 zoom |
| RNN/hidden state | `recurrent_timestep_zoom` | timestep 단위 zoom |

## View Decision Rules

1 view로 충분한 경우:

- 입력과 출력이 명확하다.
- 방향이 하나다.
- cycle이 없다.
- 내부 상태 변화가 없다.
- 비교 대상이 1쌍 이하이다.
- 각 절차가 역할명만으로 이해된다.

zoom이 필요한 경우:

- cycle이 있다.
- hidden state가 있다.
- 행렬/벡터 내부 계산이 있다.
- 한 블록이 2개 이상 역할을 한다.
- 같은 화살표가 여러 의미로 보일 수 있다.
- 사용자가 무엇끼리 계산하는지 헷갈릴 수 있다.
- 도면형 도식에서 블록 내부의 변환, 계산, 비교가 질문의 답이다.

도면형 도식에서 zoom하지 않는 경우:

- 블록 이름과 한 줄 역할 설명만으로 답이 된다.
- 단순 `Input -> Process -> Output` 구조이다.
- 단순 linear pipeline 또는 fork-join parallel pipeline이다.
- 내부를 열면 한 화면 객체 수가 불필요하게 증가한다.

## Transition Count Rule

선형 구조에서는 루트에서 마지막 노드까지 노드 수를 `N`이라고 할 때:

```text
transition_count = N - 1
```

cycle이 `M`개 있으면:

```text
transition_count = (N - 1) + M
```

단, 이 값은 scene object 수가 아니라 설명 전환 수이다.

## Cycle Policy

cycle은 전체 도식 안에서 모두 설명하지 않는다.

```text
전체 구조에서 cycle 존재 표시
-> cycle block만 zoom
-> 반복 1회만 애니메이션
-> 동일 구조가 반복됨을 표시
-> 전체 구조로 복귀
```

## Process Flow Policy

SW/ML 절차는 `Process Flow`로 별도 처리한다.

```text
Input -> Transform -> Calculation -> Output
```

입력과 출력은 시간차 reveal로 표현한다.

- input: 먼저 등장
- transform: 입력을 받아 형태를 바꿈
- calculation: 현재 계산 대상 한 쌍만 연결
- output: 마지막에 결과 리스트나 score로 등장

## Relation Geometry Policy

정적 관계는 수학/기하학식 relation family로 처리한다.

| Family | Visual |
|---|---|
| identical/equivalent | `=`, `≡`, 같은 위치 |
| similar/near | `≈`, 가까운 배치, 평행성 |
| contains/overlaps | nested box, Venn, `⊂`, `∩` |
| different/orthogonal | `≠`, `⟂`, 분리 lane |

변환이나 절차는 Relation Geometry가 아니라 Process Flow로 넘긴다.

## Disclosure Policy

화면에서 보이지 않는 정보는 삭제된 것이 아니라 다음 상태 중 하나로 표시한다.

| State | Meaning |
|---|---|
| `open` | 현재 열림 |
| `collapsed` | 역할명만 남기고 접힘 |
| `hidden` | 본문에서 제거되고 하단 상태바에만 표시 |
| `not_in_scene` | 현재 장면 밖 |

하단 상태바는 항상 본문 도식보다 작고 낮은 대비로 유지한다.

## Formula Lock Policy

수식은 처음부터 제시하지 않는다.

```text
예시 -> 도식 -> 애니메이션 -> 수식
```

수식은 이미 본 시각 구조를 압축하는 용도로만 쓴다.

예:

```text
Spearman(X, Y) = Pearson(rank(X), rank(Y))
cosine(A, B) = dot(A, B) / (||A|| ||B||)
```

## Final Check

산출 전에 아래를 확인한다.

- 한 장면에 중심 객체가 하나인가?
- zoom이 꼭 필요한가?
- 단순 pipeline을 불필요하게 쪼개지 않았는가?
- cycle은 별도 zoom으로 분리했는가?
- 비교 대상 A/B를 pair object로 묶었는가?
- 사라진 객체의 상태가 하단에 표시되는가?
- 수식은 시각화 뒤에 제시되는가?
