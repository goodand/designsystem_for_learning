# 저장소 범위 (Notice)

이 저장소는 claude.ai/design 프로젝트에서 배포되는 **디자인 시스템 배포본(distribution)**입니다:

- `tokens/` — 디자인 토큰 CSS 6종 (colors · typography · spacing · animation · modes · fonts)
- `styles.css` — 글로벌 엔트리포인트 (@import 묶음)
- `_ds_bundle.js` — 컴파일된 컴포넌트 번들 (FrameBar, ScenePlayer, Button, Card 등 12종 → `window.MLAnimationsDesignSystem_947957`)
- `_ds_manifest.json` — 컴포넌트/카드 매니페스트
- `_adherence.oxlintrc.json` — DS 준수 lint 규칙. 원본의 `x-omelette` 블록(빌드 자동생성 토큰 인벤토리)은 중복이라 요약 노트로 대체함 — 권위 있는 토큰 목록은 `tokens/*.css` 참고
- `README.md` — 디자인 시스템 문서 (원문 그대로)

README가 언급하는 `components/`(소스), `strategy/`, `guidelines/`, `examples/`, `domain-profiles/` 등은 디자인 프로젝트 쪽 소스 계층으로, 이 배포본 저장소에는 포함되지 않습니다. 컴포넌트 소스는 `_ds_bundle.js`에 컴파일되어 들어 있습니다.

사용 예시는 소비 저장소 참고: https://github.com/goodand/Visual-Explanatory-Material-on-Transformer-Architecture
