---
name: generate-fixed-fashion-profile
description: Generate a vertical loose color-block editorial fashion illustration from one uploaded left-profile portrait while locking the bundled walking pose, wardrobe, palette, background grid, framing, and doodle treatment, with an optional height_cm variable that changes leg proportions relative to the 170 cm template. Use when the user uploads a left-side face/profile photo and asks for the established fixed-outfit illustration, asks to replace only the head or identity above the neck, provides a target height, or asks to keep the outfit and stride while adapting stature.
---

# Generate Fixed Fashion Profile

Create one bitmap illustration by editing the bundled template at `assets/locked-fashion-template.png`. Treat the template as the source of truth for every pixel-level visual decision below the neck and for the overall composition. Treat the user's portrait only as an identity reference above the neck.

## Input contract

- Require one clear left-facing profile photograph. Accept a slightly three-quarter-left view only when the nose, forehead, jaw, ear, and hair silhouette remain readable.
- Ask for a clearer left-profile photo only when the head shape or facial silhouette cannot be inferred.
- Use the uploaded photo only for head shape, skull silhouette, hairline, hairstyle, hair color, forehead, ear, brow, nose, lips, jaw, chin, skin tone, facial hair, and expression.
- Ignore the uploaded photo's clothing, accessories, body, pose, background, lighting, and photographic texture.
- Keep facial hair in a muted gray-black charcoal treatment when present. Omit it when the identity reference is clean-shaven.

## Height variable

- Treat the bundled template as `170 cm` by default.
- Accept an optional user-supplied `height_cm`. Use `170` when the user omits it. Never look up or infer a person's height when the user supplies a value.
- Compute the stylized leg-length multiplier as:

  `leg_scale = clamp(1 + (height_cm - 170) / 100, 0.80, 1.30)`

- Map `170 cm` to `1.00`, `180 cm` to `1.10`, `190 cm` to `1.20`, `160 cm` to `0.90`, and `150 cm` to `0.80`.
- Treat this as a visual proportion rule, not an anatomical measurement claim. Keep the head size, shoulder width, torso length, coat body, hands, and shoe size unchanged unless the user separately requests those changes.
- Scale both thigh and lower-leg segments along their existing stride directions. Preserve hip placement, knee bend, foot orientation, and the walking gesture; move knees, ankles, socks, and shoes only as required by the new leg lengths.
- Extend or compress the trouser shapes to follow the legs. Continue the irregular red grid with similar line weight and density instead of stretching existing cells into long rectangles.
- Recenter the complete figure or adjust top/bottom whitespace minimally to keep both shoes visible and preserve generous margins. Do not imitate height by uniformly enlarging the entire figure.

## Locked template

Preserve all of the following unless the user explicitly asks to unlock one item:

- vertical full-body composition and generous off-white margins
- left-facing walking pose, slight forward lean, relaxed shoulders, one leg planted and the other lifted behind
- hand placement, upper-body proportions, garment silhouette, and the walking gesture; preserve baseline leg proportions and foot positions only when `height_cm` is `170`
- oversized light beige coat with the same loose pocket and sleeve treatment
- vivid red-orange scarf, deep cobalt-blue sunglasses, off-white trousers with irregular red-orange grid marks, orange-red socks, and beige chunky shoes
- warm off-white paper field with sparse, broken pale-gray and blue graph lines
- line placement, broad color-block rhythm, palette balance, and loose editorial mood

Do not import any wardrobe or body information from the identity photo. Do not redesign, restyle, clean up, or improve the template. When `height_cm` differs from `170`, unlock only leg-segment lengths, corresponding trouser coverage, foot positions, and the minimum framing adjustment required to keep the full figure visible.

## Fixed visual language

- Use thin, wandering, irregular black contours with wobble, doubled searching strokes, broken joins, floating marks, and occasional unclosed shapes.
- Build the figure from broad, casually placed matte color blocks in warm beige, taupe, olive-brown, muted gray, red-orange, cobalt blue, and black.
- Allow color shapes to miss the contours slightly, overlap, stop abruptly, or leave areas unfinished.
- Describe the new identity through a simplified profile silhouette and a small number of expressive marks. Preserve likeness through proportions and recognizable head features, not photographic detail.
- Keep the trousers' red grid hand-drawn, uneven, incomplete, and slightly displaced. Keep the background grid sparse and imperfect.
- Avoid photorealism, accurate fabric rendering, polished fashion illustration, clean vector edges, precise shoe construction, glossy shading, 3D depth, and anatomically over-resolved facial detail.

## Generation workflow

1. Inspect the uploaded identity photo and the bundled template with the image viewing tool.
2. Read `height_cm`; default it to `170`, calculate `leg_scale`, and state the result before generating.
3. Use the built-in image generation tool in edit or identity-preserve mode; do not generate the body from scratch when the template can be supplied as the edit target.
4. Pass the images in this role order:
   - Image 1: `assets/locked-fashion-template.png` — edit target plus style, wardrobe, pose, composition, and background authority.
   - Image 2: uploaded portrait — identity reference for the region above the neck only.
5. State the locked invariants before describing the new identity. When height differs from `170`, identify leg lengths, related foot positions, trouser coverage, and minimum reframing as the only additional unlocked regions.
6. Generate one vertical image. Add no props, people, typography, logos, or narrative elements.
7. Inspect the output against the bundled template. Check identity, `leg_scale`, preserved knee angles and stride direction, full-body coverage, outfit fidelity, and style. Reject and retry once when unrelated regions drift materially.
8. On retry, correct only the observed drift. Do not introduce unrelated refinements.
9. Save the result non-destructively and show it to the user.

## Prompt blueprint

Prompt suggestion: provide the person's `height_cm` together with the profile image. The skill uses that value to estimate a visually appropriate leg-length proportion relative to the 170 cm template, so no manual leg-length percentage is required. Treat the result as an illustrative approximation rather than an anatomical measurement.

```text
Use case: identity-preserve + precise localized style-transfer
Asset type: vertical loose editorial fashion doodle
Variables:
- template_height_cm: 170
- target_height_cm: <user value or 170>
- leg_scale: clamp(1 + (target_height_cm - 170) / 100, 0.80, 1.30)
Input images:
- Image 1 is the locked edit target and controls body, pose, wardrobe, accessories, palette,
  linework, color blocks, background grid, framing, and all regions below the neck except the
  explicit leg and framing adjustments required by target_height_cm.
- Image 2 is an identity reference and controls only the person's anatomy and appearance above
  the neck: head shape, face shape, hair, hairline, ear, brow, nose, mouth, jaw, chin, skin tone,
  facial hair, and expression.

Primary request: Keep Image 1 unchanged except for replacing the person's identity above the
neck with a simplified left-profile interpretation of Image 2. If target_height_cm differs from
170, scale only the thigh and lower-leg lengths by leg_scale along the existing stride directions.

Locked invariants: preserve the exact walking gesture, upper-body proportions, target leg scale,
beige oversized coat,
red-orange scarf, cobalt-blue sunglasses, off-white trousers with irregular red-orange grid,
orange-red socks, beige chunky shoes, off-white paper background, sparse broken blue-gray grid,
composition, margins, and loose color-block rhythm. Ignore Image 2's clothes, body, pose,
accessories, background, and photographic lighting.

Height adaptation: keep head size, shoulder width, torso length, coat body, hands, shoe size,
hip placement, knee bend, and foot orientation unchanged. Move knees, ankles, socks, and shoes
only as required by the scaled leg segments. Extend the trousers and continue their irregular
grid at similar density. Recenter minimally to keep both shoes visible. Do not scale the entire
figure uniformly.

Style: loose color-block graffiti doodle; wandering imperfect black lines; broken, doubled, and
unclosed contours; broad misregistered matte color patches; simplified expressive facial marks;
recognizable identity without photographic detail; unfinished editorial energy.

Avoid: changes below the neck other than explicit height adaptation, redesigned clothing,
changed joint angles, changed stride direction, uniform whole-body scaling, cropped shoes,
realistic portrait rendering, detailed fabric or shoes, clean vector outlines, perfect geometry,
3D, glossy shading, extra people, props, text, logos, or watermark.
```

## Bundled example

Read [references/examples.md](references/examples.md) when applying or evaluating the height variable. Use the bundled height-adaptive output as a visual acceptance reference for adjusted legs, preserved stride, stable wardrobe, and full-body framing. Do not use the example output as the edit target; always start from `assets/locked-fashion-template.png`.

## Failure corrections

- If clothing or pose changes, make the bundled template the dominant edit target and repeat: “change only the identity above the neck plus the explicit height-driven leg adjustments; preserve every other region.”
- If the result becomes too realistic, reduce facial detail to profile silhouette, hair mass, blue glasses, a few black marks, and flat skin blocks.
- If the result becomes too polished, require searching contours, broken joins, misplaced washes, unfinished areas, and no vector-clean edges.
- If identity is weak, strengthen only the distinctive head silhouette, hairline, nose, lips, jaw, chin, ear, and facial-hair pattern from the portrait.
- If the photo's outfit leaks into the result, explicitly ignore all identity-reference pixels below the neck.
- If the beard becomes brown or overly dark, render it as sparse muted gray-black charcoal marks.
- If a taller person looks merely zoomed in, restore the original head, torso, shoulder, coat, hand, and shoe sizes; lengthen only the thigh and lower-leg segments.
- If the stride changes, restore the original hip anchor, knee angles, leg directions, and foot orientations; move joints only along those existing directions.
- If the trousers look stretched, continue the irregular red grid with additional marks at the original visual density instead of elongating its cells.
- If feet crop after height adaptation, recenter vertically or reduce only the minimum overall framing scale needed to restore the original margins.
