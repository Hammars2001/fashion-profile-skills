# V1 Examples

Use both paired examples to verify that V1 replaces identity above the neck while keeping the bundled walking pose, outfit, palette, background, and composition fixed.

## Example A: elderly fixed-fashion profile

- Input: `../assets/examples/elderly-fixed-fashion-input-rights-unverified.png`
- Output: `../assets/examples/elderly-fixed-fashion-output.png`
- Edit target: `../assets/locked-fashion-template.png`
- Height: use the 170 cm baseline unless the user supplies another value.

The input supplies the elderly subject's balding head shape, loose gray-white hair, forehead, ear, nose, lips, jaw, skin tone, and expression. The output demonstrates that these above-neck identity features can be translated into loose profile marks while the V1 clothing and walking template remain fixed.

### Input

![Elderly fixed-fashion input, publication rights unverified](../assets/examples/elderly-fixed-fashion-input-rights-unverified.png)

### Output

![Elderly fixed-fashion illustration output](../assets/examples/elderly-fixed-fashion-output.png)

## Example B: Haaland profile with height adaptation

- Input: `../assets/examples/haaland-profile-input-rights-unverified.jpeg`
- Output: `../assets/examples/haaland-profile-output.png`
- Edit target: `../assets/locked-fashion-template.png`
- `template_height_cm`: `170`
- `target_height_cm`: `190`
- `leg_scale`: `1.20`

The input supplies the very light blond hair slicked backward into a tied ponytail, forehead-to-nose profile, broad jaw, and squared chin. The output demonstrates simultaneous identity replacement and stylized height adaptation.

### Input

![Haaland profile input obtained from the internet, publication rights unverified](../assets/examples/haaland-profile-input-rights-unverified.jpeg)

### Output

![Haaland 190 cm fixed-fashion illustration output](../assets/examples/haaland-profile-output.png)

## Acceptance criteria

- Preserve the recognizable head silhouette and key profile features without photographic rendering.
- Keep the V1 coat, scarf, sunglasses, trousers, socks, shoes, graph-paper background, and walking gesture fixed.
- For the 190 cm example, make both legs visibly longer than the 170 cm template without uniformly scaling the full figure.
- Continue the trouser grid with additional irregular marks instead of stretching existing cells.
- Keep both shoes fully visible with generous top and bottom margins.

## Publication-rights note

The Haaland photograph was obtained from the internet. Publication rights for both bundled input photographs have not been verified. They are included for private workflow testing only. Before publishing the Skill publicly, confirm permission or replace them with licensed equivalents.
