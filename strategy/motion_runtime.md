# Motion Runtime Policy

## Rule

**Any motion that must survive capture or export is driven by JS timer tweens, not CSS transitions.**

CSS transition/animation clocks pause or skip under frame-stepped rendering (screenshot
sequences, PDF/PPTX export, video capture): a scene that animates correctly live exports
as a frozen or half-finished frame. Verified in unit_01, where every CSS transition had
to be replaced with a JS tween mid-production.

| Motion | Runtime |
|---|---|
| Scene transitions, reveals, draws, morphs — anything captured/exported | **JS timer tween** (reference below) |
| Hover / focus / active micro-interactions (live preview only) | CSS transitions OK (`--transition-*` presets) |

Tokens remain the single source of truth: the tween **reads** duration/easing from
`tokens/animation.css` — never hardcode ms or bezier values in scene code.

## Reference implementation (verified in unit_01)

```js
// Read animation tokens once per document
const css = getComputedStyle(document.documentElement);
const tokenMs = (name) => parseFloat(css.getPropertyValue(name)) || 0;   // "300ms" → 300
const tokenEase = (name) => {
  const m = css.getPropertyValue(name).match(/-?[\d.]+/g);
  return m && m.length === 4 ? cubicBezier(...m.map(Number)) : (t) => t;
};

// cubic-bezier(x1,y1,x2,y2) solver — Newton–Raphson, sufficient at 1080p
function cubicBezier(x1, y1, x2, y2) {
  const cx = 3 * x1, bx = 3 * (x2 - x1) - cx, ax = 1 - cx - bx;
  const cy = 3 * y1, by = 3 * (y2 - y1) - cy, ay = 1 - cy - by;
  const sampleX = (t) => ((ax * t + bx) * t + cx) * t;
  const sampleY = (t) => ((ay * t + by) * t + cy) * t;
  const solveX = (x) => {
    let t = x;
    for (let i = 0; i < 8; i++) {
      const dx = sampleX(t) - x;
      const d = (3 * ax * t + 2 * bx) * t + cx;
      if (Math.abs(dx) < 1e-5 || d === 0) break;
      t -= dx / d;
    }
    return t;
  };
  return (x) => (x <= 0 ? 0 : x >= 1 ? 1 : sampleY(solveX(x)));
}

// Timer tween — runs on rAF live, or on a manual clock for capture
function tween({ duration, ease, onUpdate, onDone, clock = null }) {
  duration = duration ?? tokenMs('--duration-normal');
  ease = ease ?? tokenEase('--ease-default');
  let start = null, raf = null;
  const step = (now) => {
    if (start === null) start = now;
    const p = Math.min(1, (now - start) / duration);
    onUpdate(ease(p), p);
    if (p < 1) { if (!clock) raf = requestAnimationFrame(step); }
    else if (onDone) onDone();
  };
  if (clock) return { advance: (t) => step(t) };   // capture mode: caller owns the clock
  raf = requestAnimationFrame(step);
  return { cancel: () => cancelAnimationFrame(raf) };
}
```

Usage: `tween({ duration: tokenMs('--anim-morph-duration'), ease: tokenEase('--ease-spring'), onUpdate: (v) => { el.style.transform = \`translateX(${v * 200}px)\`; } })`

## Capture mode

For deterministic export, pass `clock: true` and drive the same tween with
`advance(ms)` step-by-step — identical easing, frame-exact output.

## Stagger

Sequential reveals: offset each object's tween start by `tokenMs('--anim-stagger-delay')`
(80ms) — do not use CSS `transition-delay` for exported scenes.
