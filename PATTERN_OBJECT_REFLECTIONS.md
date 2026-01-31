# Pattern: Object Reflections for Realism (Scene-Based HDRI)

**Goal:** Use real-world environments (apartments, cities, lobbies) to create reflections that show actual objects, adding realism and context to the metal surface.

---

## When to Use Object Reflections

- **Product Visualization:** Showing a product "in context" (e.g., a phone on a desk).
- **Cinematic Shots:** Metal reflecting a cityscape, skyline, or interior.
- **Realism over Abstraction:** When the design brief calls for "grounded" visuals.

---

## HDRI Presets with Visible Objects

| Preset      | Reflected Content                   | Mood/Feel       |
| ----------- | ----------------------------------- | --------------- |
| `apartment` | Windows, furniture, warm lighting   | Cozy, interior  |
| `city`      | Buildings, sky, urban structures    | Dynamic, modern |
| `lobby`     | Columns, floors, neutral tones      | Professional    |
| `park`      | Trees, sky, greenery                | Natural, calm   |
| `forest`    | Dense foliage, dappled light        | Organic, wild   |
| `sunset`    | Orange/pink sky, warm glow          | Dramatic, warm  |
| `dawn`      | Soft blue/purple, gentle light      | Soft, peaceful  |
| `night`     | Dark blues, artificial lights       | Moody, noir     |
| `warehouse` | Industrial, exposed beams, concrete | Raw, edgy       |

---

## Code Example (City Reflection)

```tsx
import { Environment } from '@react-three/drei';

<Environment
    preset="city"
    background={false}
    environmentRotation={[0, rotationY, 0]}
/>

<mesh>
    <capsuleGeometry args={[0.92, 4.0, 8, 128]} />
    <meshPhysicalMaterial
        color="#f0f0f0"
        metalness={1.0}
        roughness={0.1}     // Low = sharp reflections of buildings
        envMapIntensity={1.8}
    />
</mesh>
```

---

## Tips for Object Reflections

1. **Lower Roughness = Sharper Objects:** `roughness: 0.05` shows clear building outlines. `roughness: 0.2` blurs them.
2. **Rotate for Composition:** Use `environmentRotation` to position the most interesting part of the HDRI where it reflects best.
3. **Color Temperature:** Interior presets (apartment, lobby) are warm. Outdoor presets (city, sunset) vary. Match to your scene.
4. **Combine with Blur:** If objects are too distracting, use `blur={0.3}` to soften them while keeping the lighting.

---

## When NOT to Use Object Reflections

- When you want a **neutral, abstract** silver look.
- When the reflected objects **distract** from the product.
- For **UI elements** that need to work on any background.

→ See `PATTERN_CLEAN_NEUTRAL_REFLECTIONS.md` for those cases.
