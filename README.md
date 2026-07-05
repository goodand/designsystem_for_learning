# ML Animations Design System

**브랜드: 축(Chuk)** — "축(axis)"은 이 시스템의 핵심인 구조적 축(Relation / Process / Abstraction / Disclosure / Representation)에서 따온 임시 브랜드명입니다.

딥러닝 및 머신러닝 개념 설명용 애니메이션 제작을 위한 디자인 시스템입니다.\
한글 타이포그래피·색상 체계·UI 컴포넌트는 DaleStudy의 [daleui](https://github.com/DaleStudy/daleui) 오픈소스 디자인 시스템을 \*\*기술적 기반(foundation)\*\*으로 삼되, 브랜드 정체성은 daleui와 무관한 축(Chuk)입니다.

> **The provided question set and Topic Mode are not the universal taxonomy. They are domain-specific instances used to validate the reusable design system.**

---

## Source References

- **DaleUI**: https://github.com/DaleStudy/daleui — 한국어 환경에 맞는 오픈소스 디자인 시스템. Pretendard 폰트 시스템, 색상 토큰(Violet/Teal/Slate), 컴포넌트 체계의 원본.
- **Animation Content**: Text Similarity, RAG, NNS, ANN, KNN 관련 질문셋과 scene plan — 디자인 시스템의 검증용 test case로만 사용.

---

## Architecture: Core / Domain Profile / Example Instance

### Core Design System

도메인과 무관하게 재사용되는 규칙:

- **Fixed Structural Axes**: Relation, Process, Abstraction, Disclosure, Representation modes
- **Visual Strategy (Markdown)**: `strategy/` — 시각 전략은 CSS/HTML이 아니라 MD로 관리. `strategy/router.md`가 단일 진입점(라우터)
- **Color scales**: Violet, Teal, Slate, Sage + semantic (Red, Green, Amber, Blue)
- **Typography**: Pretendard Variable (sans), JetBrains Mono (mono)
- **Spacing, radii, borders, shadows, animation timing**
- **UI Components**: Button, Tag, Badge, Card, Text, Heading, TextInput, Checkbox, Select, Stack, FrameBar, ScenePlayer

### Domain Profile (가변 축)

특정 주제에 맞춰 교체되는 값. `domain-profiles/` 디렉토리에 CSS 파일로 관리:

- **Topic Mode** = configurable domain profile
- 예: Text Similarity profile (`lexical / semantic / hybrid`)
- 예: ML profile (`supervised / unsupervised / reinforcement / evaluation`)
- 예: Geometry profile (`vector / distance / angle / projection`)

사용법: `<div data-domain="text-similarity">` 또는 `class="domain-text-similarity"`

### Example Instance

특정 질문 하나에 적용된 scene plan. `examples/scene_plans/*.json`(unit_01\~05)이 이에 해당하며, `examples/scene-plan-unit01.html`은 실제 plan을 디자인 시스템으로 렌더링한 스토리보드입니다.

---

## Visual Strategy Layer (`strategy/`)

**시각적 전략은 Markdown으로 관리**합니다. CSS/HTML은 "무엇이 어떻게 보이는가"를, `strategy/`의 MD 파일들은 "어떤 개념을 어떤 포맷·레이아웃·모션으로 시각화할지"를 담당합니다.

- **진입점(라우터)**: `strategy/router.md` — 모든 HTML 산출물이 이 파일로 연결됩니다.
- **연결 방식**: 각 HTML은 `@dsCard` 다음에 `<!-- @visual-strategy … -->` 주석과 `<link rel="visual-strategy" href="…/strategy/router.md">` 태그로 자신을 지배하는 전략 파일을 선언합니다.
- **정책 계층(core)**: `design_system.md`, `five_unit_frame.md`, `ux_policy.md`, `scene_object_policy.md`, `graph_policy.md`
- **포맷 라우터 + 스펙**: `visual_formats.md` → `visual_formats/*.md` (xy_coordinate, matrix, heatmap, venn, zoom, schematic, graph 등 11종)
- **도메인 정책(교체 가능)**: `strategy/domains/text-similarity/` (design.md, animation_policy.md)

---

## Fixed Structural Axes (고정 축)

| Axis | Values | Visual Encoding (색 없음 — 색은 Topic 전용) |
| --- | --- | --- |
| **Relation** | same, similar, different, contains, independent | 배치·거리·경계·bracket·Venn (주) + 선 스타일 (보조) |
| **Process** | input, procedure, output | 위치·화살표·순서·타이밍 (주) + 단계 번호·흐름선 (보조) |
| **Abstraction** | macro, meso, micro | zoom·scale·block open/close·depth label (opacity 아님) |
| **Disclosure** | open, collapsed, hidden, focus | 보임/접힘/숨김 상태·중앙 배치 (주) + 명도·테두리·state bar (보조) |
| **Representation** | data, expression, computation, category, importance | 5슬롯 레이아웃·고정 위치·라벨 (주) + 작은 아이콘 (보조) |

> **Token ownership**: 색상은 Topic Mode / Domain Profile **전용**입니다. 구조적 4개 축(Relation·Process·Representation·Abstraction)에는 색 의미를 배정하지 않으며, opacity/명도는 Disclosure의 보조 채널로만 씁니다. 전체 표는 `strategy/token-ownership.card.html` 및 `tokens/modes.css` 헤더 참고.

---

## CONTENT FUNDAMENTALS

### Language & Tone

- **Primary language**: 한국어 (Korean), with English technical terms preserved as-is
- **Tone**: 교육적이고 명확한 설명체. 학습자의 눈높이에 맞춘 친근하되 정확한 어조
- **Technical terms**: 원어(영어)를 병기. 예: "코사인 유사도(Cosine Similarity)"
- **Copy style**: 질문-답변 구조 기본. 짧은 문장 — 한 문장에 하나의 개념
- **Emoji**: 사용하지 않음. 시각적 강조는 색상과 아이콘으로 처리

---

## VISUAL FOUNDATIONS

### Color System

DaleUI의 12단계 색상 스케일 기반.

- **Brand (Light)**: Violet — `#5333E1` (violet-9)
- **Brand (Dark)**: Teal — `#12A594` (teal-9)
- **Neutral**: Slate 스케일
- **Semantic**: Red(danger), Green(success), Amber(warning), Blue(info)
- **Animation canvas**: 어두운 배경(`#0F1110`) 위에 밝은 요소

### Typography

- **Sans-serif**: Pretendard Variable — 한글 최적화 가변 폰트
- **Monospace**: JetBrains Mono — 코드, 수식, 행렬 값
- **Sizes**: 12px(xs) \~ 72px(8xl), 16px(md) 기준
- **Weights**: Normal(400), Medium(500), Semibold(600), Bold(700)

### Spacing & Layout

- 4px 기반 스케일: 0, 2, 4, 8, 12, 16, 20, 24, 32, 36, 40, 48px
- Radii: xs(2px), sm(4px), md(8px), lg(16px), full
- 애니메이션 캔버스: 16:9 (1920×1080), `transform: scale()`로 뷰포트 맞춤

### Motion

- **Easing**: `ease-default` (0.4,0,0.2,1), `ease-spring` (overshoot), `ease-bounce`
- **Duration**: 150ms(fast) → 1200ms(scene)
- **Runtime**: 내보내기/캐처 대상 모션은 **JS 타이머 트윈**으로 구동 (토큰을 읽어서) — `strategy/motion_runtime.md`
- **Stagger**: 80ms 순차 등장
- **Hover**: 배경 한 단계 진하게 / **Active**: 두 단계 진하게
- **Focus**: 2px outline, 3px offset, brand 색상

### Cards & Containers

- bg: white, border: slate-5 1px, radius: md(8px), padding: 24px

---

## ICONOGRAPHY

- **Primary**: [Lucide](https://lucide.dev/) (stroke-based, 24×24)
- **Sizes**: xs(12px), sm(16px), md(20px), lg(24px)
- **Color**: `currentColor` 상속
- **Brand icons**: `assets/icons/` (Discord, GitHub, YouTube, etc.)
- **Emoji**: 사용하지 않음

---

## File Index

### Tokens (`tokens/`)

- `colors.css` — 색상 스케일 + semantic aliases
- `typography.css` — 폰트 패밀리, 크기, 무게
- `spacing.css` — 간격, 둥글기, 테두리
- `animation.css` — 이징, 지속시간, 그림자
- `modes.css` — 고정 구조적 축 (Relation, Process, Abstraction, Disclosure, Representation, Topic slot)
- `fonts.css` — Pretendard/JetBrains Mono @font-face

### Domain Profiles (`domain-profiles/`)

- `text-similarity.css` — Lexical / Semantic / Hybrid
- `ml.css` — Supervised / Unsupervised / Reinforcement / Evaluation
- `geometry.css` — Vector / Distance / Angle / Projection

### Visual Strategy (`strategy/`)

- `router.md` — **단일 진입점**. 결정 흐름 + 모든 전략 파일 링크
- `design_system.md` — 5개 상위 시각 레이어 + 재사용 컴포넌트
- `five_unit_frame.md` — 데이터→표현→계산→분류→중요성 프레임
- `ux_policy.md`, `scene_object_policy.md`, `graph_policy.md`, `motion_runtime.md` — UX(캔버스 밀도 포함)/객체/그래프/모션 런타임 정책
- `visual_formats.md` — 포맷 라우터 → `visual_formats/*.md` (11종 포맷 스펙)
- `motion_runtime.md` — 모션 런타임 정책: 내보내기 대상 모션은 JS 타이머 트윈
- `domains/text-similarity/` — 도메인 정책 (design.md, animation_policy.md)
- `router.card.html`, `formats.card.html` — Design System 탭 카드

### Examples (`examples/`)

- `scene_plans/unit_01…05_animation_scene_plan.json` — 실제 scene-object 계획 (Example Instance)
- `scene-plan-unit01.html` — 실제 plan을 디자인 시스템으로 렌더링한 스토리보드 카드

### Components (`components/`)

- `core/` — Button, Tag, Badge, Card, Text, Heading (Tag/Badge는 `tone="topic-1..5"` 지원 — 색은 도메인 프로필이 주입)
- `forms/` — TextInput, Checkbox, Select
- `layout/` — Stack
- `animation/` — FrameBar (5칸 Representation 프레임바), ScenePlayer (씬 플레이어 셸 — 시간은 JS 트윈이 구동)

### UI Kits (`ui_kits/`)

- `animation-canvas.html` — 다크 캔버스: 좌표계 + 벡터 + 행렬 + 수식
- `scene-controls.html` — Unit 네비게이터 + process bar + scene object 패널

### Assets (`assets/`)

- `icons/` — 브랜드 SVG 아이콘 (Discord, GitHub, YouTube 등)
- 로고: 축(Chuk) 워드마크 — `guidelines/brand-logo.html` 참고 (타이포그래픽 워드마크, 별도 SVG 없음)

### Guidelines (`guidelines/`)

- Foundation specimen cards (Colors, Type, Spacing, Motion, Brand, Modes)

### Root Files

- `styles.css` — 글로벌 CSS 엔트리포인트
- `README.md` — 이 문서
- `SKILL.md` — Agent Skill 호환 파일
