# Pattern: The "Frameless" Round Button (3D)

**Problem:**
When creating a highly rounded button (Pill shape) using `RoundedBox` geometry in Three.js/R3F, a visible "frame" or "rim" artifact appears at high radii (e.g., radius 0.8+).
This happens because `RoundedBox` creates a distinct bevel geometry that reflects light differently than the flat face, especially when using High Contrast (Studio) HDRI environments. The bevel catches the dark floor/corners of the studio, creating a dark outline.

**Solution:**
Use **`CapsuleGeometry`** instead of `RoundedBox`.

**Physics:**
A Capsule is mathematically a cylinder with two perfect hemispheres. It has **C0 continuity** (smooth transition) with NO distinct bevel edge.

- **Geometry**: `<capsuleGeometry args={[radius, length, capSegments, radialSegments]} />`
- **Orientation**: Default is vertical. Rotate `[0, 0, Math.PI / 2]` for horizontal buttons.

**Environment Fix:**
Even with Capsule Geometry, a rotating "Studio" environment can cause the "Spinning World" effect.

- **Fix:** Use a **Static Environment** (no rotation) and animate a **Moving Light Source** (SpotLight/Lightformer) instead.
- **Result:** The object stays solid, but the glint travels across it. This mimics "Cinematic Lighting" rather than "Spinning Camera".

**Code Example:**

```tsx
<mesh rotation={[0, 0, Math.PI / 2]}>
  <capsuleGeometry args={[0.9, 4.0, 8, 64]} />
  <meshPhysicalMaterial metalness={1.0} roughness={0.1} color="#ffffff" />
</mesh>
```
