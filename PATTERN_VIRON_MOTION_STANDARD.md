# PATTERN: VIRON MOTION STANDARD

**Context:** Motion Design for Viron Studio (Enterprise Level).
**Status:** MANDATORY.

## 1. THE ANTI-LINEAR RULE

**Never** use linear interpolation for motion. It looks cheap and robotic.

## 2. THE GOLDEN BEZIER

For standard "Ease-In-Out" transitions (e.g. Lines drawing, Objects moving):

```typescript
import { Easing } from "remotion";
const vironEase = Easing.bezier(0.65, 0, 0.35, 1);
```

- **Profile:** Slow Start -> Very Fast Middle -> Slow Snap End.
- **Feel:** "Expensive", "Heavy", "Industrial".

## 3. SPRING PHYSICS

For UI Elements (Bars, Cards, Text) appearing:

```typescript
import { spring } from "remotion";
const spr = spring({
  frame: frame - delay,
  fps,
  config: { damping: 12, stiffness: 100, mass: 1 }, // "Heavy Metal" feel
});
```

- **Damping 12/Stiffness 100:** No wobbly jelly. Firm but reactive.

## 4. STAGGERING

Never animate a group at once. Always stagger by 2-5 frames.

```typescript
const delay = index * 5;
```

This creates organic "waves" of data.
