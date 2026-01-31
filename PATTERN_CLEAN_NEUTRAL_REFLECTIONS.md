# Pattern: Clean Neutral Reflections (Abstract Silver)

**Goal:** Create a polished silver surface with smooth gradients, no visible objects, and a professional "product shot" aesthetic.

---

## When to Use Clean Reflections

- **UI Components:** Buttons, icons that need to work on any background.
- **Logo Animations:** Brand elements that should look "premium" without context.
- **Abstract Design:** When the focus is the metal itself, not what it reflects.

---

## Methods to Achieve Clean Reflections

### Method 1: Studio Preset + Blur (Recommended)

The "studio" preset has photography lighting but visible light stands. Adding blur removes the stands while keeping the gradient.

```tsx
<Environment
  preset="studio"
  background={false}
  blur={0.5} // Softens the light stands
  environmentRotation={[0, rotationY, 0]}
/>
```

**Trade-off:** Higher blur = fewer details, more gradient. Lower blur = more visible elements.

---

### Method 2: Lobby/Apartment + High Blur

Use a realistic preset but blur it heavily. This keeps natural light falloff without object shapes.

```tsx
<Environment
  preset="lobby"
  background={false}
  blur={0.8} // Heavy blur
/>
```

---

### Method 3: Custom Lightformers (Advanced)

Build your own studio with abstract light shapes. Requires careful positioning (Z-axis matters).

```tsx
<Environment resolution={1024}>
  <Lightformer form="ring" intensity={4} scale={30} position={[0, 0, 10]} />
  <Lightformer form="rect" intensity={2} scale={20} position={[0, 10, 0]} />
</Environment>
```

**Warning:** Lightformers must be positioned IN FRONT of the button (positive Z, larger than camera Z) to reflect on its face.

---

## Material Settings for Clean Silver

```tsx
<meshPhysicalMaterial
    color="#ffffff"
    metalness={1.0}
    roughness={0.12 to 0.18}  // Slightly rough for soft gradients
    envMapIntensity={1.5}
    clearcoat={0.8}
    clearcoatRoughness={0.0}
/>
```

---

## Comparison: Blur Levels on "studio" Preset

| Blur  | Result                                 |
| ----- | -------------------------------------- |
| `0.0` | Sharp, visible light stands/equipment  |
| `0.3` | Stands slightly visible, good gradient |
| `0.5` | Stands blurred, smooth gradient        |
| `0.8` | Almost abstract, very soft transitions |
| `1.0` | Nearly flat lighting, minimal contrast |

**Sweet Spot:** `blur={0.4 to 0.6}` for clean but dynamic reflections.

---

## Subtle Color for Realism (Optional)

Pure white environments can look "sterile". A tiny bit of color adds life:

```tsx
<meshPhysicalMaterial
  color="#f8f8ff" // Very slight cool tint
  // OR
  color="#fff8f0" // Very slight warm tint
/>
```

Or use a preset like "dawn" with high blur for soft color gradients.
