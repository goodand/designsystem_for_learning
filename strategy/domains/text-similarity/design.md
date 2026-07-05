# Text Similarity Visual Design System

## 1. Purpose

이 문서는 Text Similarity, RAG, KNN, NNS/ANN, TF-IDF, Jaccard, Cosine Similarity 같은 개념을 설명하기 위한 시각화 디자인 시스템이다.

핵심 목표는 다음과 같다.

- 개념을 한 번에 많이 보여주지 않고, 사용자의 시점 흐름을 안정화한다.
- 같은 역할의 화살표, 도형, 색상, 선 스타일을 반복적으로 사용한다.
- 데이터 -> 표현 -> 계산 대상 -> 개념 분류 -> 중요성 순서로 이해를 유도한다.
- 거시 구조에서 시작해 미시 계산으로 줌인하고, 다시 전체 구조로 복귀한다.

## 2. Understanding Frame

모든 단원은 아래 5칸 이해 프레임을 따른다.

| Frame | Guiding Question | Visual Strategy |
|---|---|---|
| 데이터 | 원래 무엇을 다루는가? | 원문 텍스트 카드, 문서 chunk, 실제 예시 |
| 표현 | 어떤 형식으로 바꾸는가? | 집합, 행렬, 벡터, 좌표계 |
| 계산 대상 | 무엇과 무엇을 비교하는가? | 한 쌍만 강조: row_i vs row_j, query vs document |
| 개념 분류 | lexical/semantic/ML 중 어디인가? | 2축 맵, 포함관계, 비교표 |
| 중요성 | 왜 필요한가? 무엇이 강점인가? | Before/After, 기술 비교표, 사용 시나리오 |

## 3. Top-Level Visual Layers

최상위 직접 매핑은 5개 레이어로 제한한다.

| Layer | Question | Primary Channel |
|---|---|---|
| Topic Mode | lexical / semantic / hybrid 중 무엇인가? | 3색 컬러 |
| Relation Geometry | 두 대상은 어떤 수학적/기하학적 관계인가? | 공간 배치, 포함/겹침, 기호 |
| Process Flow | SW 절차에서 입력/변환/계산/출력 중 무엇인가? | 방향 화살표, 포트, 시간차 reveal |
| Abstraction Scope | 지금 거시/중간/미시/계산/수식 중 어디인가? | 슬라이드 순서, 줌, breadcrumb |
| Disclosure State | 정보가 열림/접힘/숨김 중 어디에 있는가? | 하단 상태바, 접힌 블록 |

`Attention`은 독립 의미축으로 두지 않는다. 초점은 중앙 배치, 순차 공개, 굵은 테두리, 짧은 정지 시간, 하단 상태바로 맥락적으로 후킹한다.

## 4. Topic Mode

색상은 Text Similarity의 핵심 topic 구분에 우선 배정한다.

| Value | Meaning | Color Role |
|---|---|---|
| lexical | 단어, 토큰, 빈도, 집합 기반 | Primary |
| semantic | 의미, 개념, 임베딩 기반 | Secondary |
| hybrid | lexical과 semantic 연결/혼합 | Tertiary |
| neutral | 구조, 상태, 보조 설명 | Neutral |

색상을 초점/배경, 정확/근사, 입력/출력 같은 다른 의미에 중복 배정하지 않는다.

## 5. Relation Geometry

Relation은 수학/기하학식 family로 먼저 나눈 뒤 시각화한다.

| Family | Relations | Visual Rule |
|---|---|---|
| Identity / Equivalence | same, equivalent | 같은 위치, 같은 형태, `=`, `≡` |
| Similarity / Proximity | similar, analogous, near | 가까운 배치, 부분 겹침, `≈`, 평행성 |
| Set / Topology | contains, contained_by, overlap, disjoint | nested box, Venn overlap, `⊂`, `∩`, `∅` |
| Difference / Separation | different, independent, orthogonal | 분리 lane, 수직 축, `≠`, `⟂` |

변환이나 절차가 핵심이면 Relation Geometry가 아니라 Process Flow에서 다룬다.

## 6. Process Flow

SW/ML 문맥에서는 절차를 별도 레이어로 유지한다.

| Role | Visual Rule |
|---|---|
| input | 왼쪽 또는 상단 입력 포트에서 먼저 등장 |
| transform | 굵은 변환 화살표 또는 변환 블록 |
| calculation | 원형 계산 노드, 현재 계산 대상 한 쌍만 연결 |
| output | 오른쪽 또는 하단 결과 리스트/스코어 카드로 시간차 등장 |

입력, 중간값, 출력이 한 화면에 동시에 전부 열리지 않게 한다.

## 7. Abstraction Scope

추상화 정도는 색/도형보다 슬라이드 순서와 줌 레벨로 표현한다.

| Scope | Visual Rule |
|---|---|
| global | 역할 블록 3-5개로 전체 윤곽만 표시 |
| module | 선택한 블록 하나를 중앙 확대 |
| internal | 블록 내부의 입력, 표현, 계산, 출력 순차 공개 |
| calculation | 비교 대상 한 쌍 또는 matrix cell 하나만 표시 |
| formula | 이미 본 도식을 수식 하나로 압축 |

객체 크기를 중요도와 섞지 않는다. 크기 변화는 줌인/줌아웃 인터랙션에만 제한한다.

## 8. Disclosure State

하단 상태바로 현재 정보의 공개 상태를 표시한다.

| State | Meaning | Visual Marker |
|---|---|---|
| open | 현재 내부가 공개된 블록 | 열린 칩 |
| collapsed | 역할명만 남긴 접힌 블록 | 회색 칩 |
| hidden | 본문에서 제거된 객체 | 작은 점 또는 생략 표시 |
| not_in_scene | 현재 장면과 무관한 객체 | 상태바에서만 필요 시 표시 |

하단 상태바는 본문 도식보다 작고 낮은 대비로 유지한다.

## 9. Diagram Components

반복 컴포넌트는 실제 도식 전에 범례로 먼저 설명한다.

| Component | Meaning |
|---|---|
| document_card | 원본 데이터 또는 문서 chunk |
| matrix_grid | DTM, TF-IDF, 유사도 행렬 |
| vector_bar | 문서 벡터, query vector, embedding |
| calculation_node | cosine, dot product, distance 같은 계산 |
| algorithm_block | KNN, HNSW, ANN index, RAG retriever |
| collapsed_block | 내부를 설명하지 않는 기능 블록 |
| focus_border | 현재 사용자가 봐야 할 대상 |
| warning_marker | 헷갈리기 쉬운 차이점 |
| transform_arrow | 표현 변환 |
| comparison_arrow | 두 대상 비교 |
| flow_arrow | 처리 순서 |
| output_list | Top-k 결과, 추천 결과, 예측 결과 |

## 10. Visual Topology Axes

그래프/도식 형태를 고를 때만 제한적으로 사용한다.

| Axis | Meaning | Use When |
|---|---|---|
| Edge 유무 | 객체들이 관계로 연결되는가? | 포함관계, 처리 흐름, 계산 대상 연결 |
| 방향성 유무 | 관계가 상호적인가, 처리 방향이 있는가? | similarity 비교 vs input -> output |
| Cycle 유무 | 한 번 흐르는가, 반복되는가? | RNN, feedback, 반복 갱신 |

한 장면에서는 topology 축을 최대 1-2개만 드러낸다.

## 11. Secondary Channels

| Channel | Recommended Use | Status |
|---|---|---|
| 곡률 | 원본/인간 친화는 둥글게, 구조화/기계 표현은 직선적으로 | useful |
| 실선/점선 | 직접/명시/정확은 실선, 근사/접힘/생략은 점선 | core |
| 명도/채도 | 비활성, 보조 상태 | support only |
| 폰트 타입 | 일반 설명 vs 코드/수식 구분 | minimal |
| 다각형/각도 | 복잡도/성능 단계 암시 | optional |
| 애니메이션 속도 | exact vs approximate처럼 느림/빠름이 핵심일 때 | optional |
| 크기 변화 | zoom-in/zoom-out 인터랙션 | restricted |

## 12. Slide Pattern

기본 슬라이드 흐름은 아래 순서를 따른다.

1. 최상위 5개 시각 레이어 제시
2. 주요 개념 축과 이분법 제시
3. 도식 디자인 시스템 범례 제시
4. 전체 구조를 역할 블록 3-5개로 제시
5. 현재 설명할 블록 선택
6. 선택 블록 중앙 확대
7. 블록 내부를 입력 -> 표현 -> 계산 대상 -> 출력 순서로 순차 공개
8. 필요할 때 수식 하나 또는 비교표 하나로 고정
9. 블록을 다시 접고 전체 구조 속 역할 재표시
10. 중요성을 Before/After 또는 기술 비교표로 정리

## 13. Cognitive UX Rules

- 한 장면의 중심 객체는 하나만 둔다.
- 보조 객체는 최대 2-4개로 제한한다.
- 설명하지 않는 객체는 흐리게 남기지 말고 숨기거나 접는다.
- 같은 모양은 같은 의미를 갖게 한다.
- 한 애니메이션 장면에서는 하나의 변화만 일어나게 한다.
- 수식은 시각화 뒤에 제시한다.
- 어려운 개념은 예시 -> 도식 -> 수식 -> 다시 예시 순서로 반복한다.
- Relation은 수학/기하학식 family로 먼저 정리한다.
- Focus는 라벨링하지 말고 맥락적으로 유도한다.

## 14. Example Application

TF-IDF + Cosine 장면:

1. 데이터: 영화 overview 카드
2. 표현: TF-IDF matrix
3. 계산 대상: row_i vs row_j
4. 개념 분류: lexical topic color
5. 계산: cosine node
6. Relation: 두 row vector의 similarity
7. Scope: matrix 전체 -> row pair -> cosine formula
8. Disclosure: 나머지 row는 collapsed 또는 hidden
9. 중요성: 비슷한 단어 중요도 패턴의 영화 추천

RAG embedding search 장면:

1. 데이터: user query와 document chunk
2. 표현: embedding vector
3. 계산 대상: query vector vs document vector
4. 개념 분류: semantic topic color
5. Process: query -> embedding -> ANN search -> Top-k chunks
6. Relation: vector proximity
7. Scope: RAG 전체 -> retriever -> vector comparison
8. Disclosure: LLM generation은 접힌 블록으로 유지
9. 중요성: 의미상 가까운 근거 문서를 찾아 답변 품질 개선

## 15. Terminology Policy

라벨과 캡션의 용어는 발명하지 않고 이 표에서 가져온다. 색상과 마찬가지로 언어도 채널이다: 한 개념에 하나의 라벨만 배정한다. (unit_01의 "가중치 → 중요도 점수 → 희소성 보정 빈도" 수정 사이클에서 확립.)

### Principles

1. **타 분야 예약어와 충돌 금지.** ML에서 다른 뜻으로 굳어진 단어는 라벨로 쓰지 않는다. `가중치(weight)`는 모델 파라미터 전용 — TF-IDF 값을 "가중치"라 부르면 학습되는 파라미터로 오해된다.
2. **해석어보다 계산 메커니즘 기술어.** "중요도 점수"처럼 결과의 해석을 담은 말 대신, 무엇을 어떻게 계산했는지를 기술한다. 예: "희소성 보정 빈도".
3. **한 개념 = 한 라벨.** 같은 unit 안에서 동의어를 돌려 쓰지 않는다. 장면이 바뀌어도 라벨은 유지된다.
4. **원어 병기는 첫 등장 1회.** 예: "희소성 보정 빈도(TF-IDF)" → 이후 "희소성 보정 빈도". (README Copy style의 라벨 적용판.)
5. **표에 없는 라벨은 발명 금지.** 새 개념은 이 표에 먼저 등록(권장·금지·이유)한 뒤 사용한다 — token ownership의 언어판.

### Confirmed — TF-IDF 계열 (unit_01에서 검증)

| 개념 | 권장 라벨 | 금지 라벨 | 이유 |
|---|---|---|---|
| TF-IDF 값 | 희소성 보정 빈도(TF-IDF) | 가중치, 중요도 점수 | weight는 ML 파라미터 예약어; "중요도"는 해석어 |
| TF | 단어 빈도(TF) | 단어 가중치 | 계산 그대로 기술 |
| IDF | 역문서 빈도(IDF) | 희소성 점수, 희귀도 | 표준 역어 + 메커니즘 기술 |
| DTM | 문서-단어 행렬(DTM) | 빈도표 | 행렬 형식을 라벨에 명시 |
| DTM 셀 값 | 등장 횟수 | 점수 | 원시 count임을 유지 |

### Candidates — unit_02~05 대비 (사용 전 확정할 것)

| 개념 | 후보 라벨 | 금지 라벨 | 비고 |
|---|---|---|---|
| Cosine Similarity | 코사인 유사도(Cosine Similarity) | 방향 점수, 각도 점수 | 표준 역어 유지; 메커니즘 캡션 "두 벡터 사이 각도의 코사인" |
| Embedding | 임베딩 벡터(Embedding) | 의미 좌표 | "의미 공간의 좌표"는 캡션에서만 |
| Similarity score | 유사도 | 매칭률 | |
| KNN | k-최근접 이웃(KNN) | 주변 탐색 | |
| NNS / ANN | 최근접 탐색(NNS) / 근사 최근접 탐색(ANN) | 빠른 검색 | "근사"를 라벨에 유지 — exact/approx 구분이 핵심 개념 |
| Jaccard | 자카드 유사도(Jaccard) | 겹침 점수 | 메커니즘 캡션 "교집합 ÷ 합집합" |

확정된 라벨은 Confirmed 표로 옮기고 금지 사유를 남긴다.
