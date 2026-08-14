# HM Fashion Profile Skills

Two Codex image-generation skills for turning a person reference photo into a loose editorial fashion illustration built from wandering ink lines, flat color blocks, hand-drawn patterns, and a warm graph-paper composition.

本仓库包含两个 Codex 图像生成 Skill，用于把人物参考照片转译成松散的编辑感时装插画：游移墨线、平涂色块、手绘纹样与暖米白方格纸构图。

## Skills

### `hm-generate-fixed-fashion-profile-v1`

V1 keeps the bundled walking pose, wardrobe, palette, shoes, background, and composition fixed. The uploaded photo changes only the identity above the neck. An optional height value adjusts only the stylized leg-length proportion.

V1 固定模板中的步态、服装、配色、鞋袜、背景与构图。上传照片只替换颈部以上的人物特征；可选身高参数只调整风格化腿长比例。

Typical invocation:

```text
Use $hm-generate-fixed-fashion-profile-v1 with this profile photo and height_cm 180.
```

### `hm-generate-variable-fashion-profile-v2`

V2 keeps the established illustration language, walking rhythm, framing, and graph-paper background, while translating the visible clothing in each uploaded photo into the same loose line-and-color-block style. Clothing is not fixed.

V2 固定画风、步态节奏、构图和方格纸背景，但服装会跟随每次上传照片中的可见穿搭变化。V2 的核心区别是服装不固定。

Typical invocation:

```text
Use $hm-generate-variable-fashion-profile-v2 to turn this full-body fashion photo into the established illustration style. Use height_cm 170.
```

## Visual examples / 视觉范例

### V1 — fixed fashion / 固定穿搭

V1 contains two paired examples. Both preserve the same fixed outfit, walking rhythm, palette, shoes, graph-paper background, and loose line-and-color-block language. Only the identity above the neck and the optional height-driven leg proportion change.

V1 包含两组输入/输出范例。两组都保持同一套固定服装、步态、配色、鞋袜、方格纸背景，以及松散线条与色块语言；只替换颈部以上的人物特征，并可按输入身高调整腿长比例。

#### V1 example A — elderly fixed-fashion profile / 老人固定穿搭范例（网络参考图）

**Input photograph / 输入照片**

<p align="center">
  <img src="hm-generate-fixed-fashion-profile-v1/assets/examples/elderly-fixed-fashion-input-rights-unverified.png" width="560" alt="Elderly fixed-fashion input photograph, publication rights unverified">
</p>

**Generated illustration / 生成插画**

<p align="center">
  <img src="hm-generate-fixed-fashion-profile-v1/assets/examples/elderly-fixed-fashion-output.png" width="560" alt="V1 elderly fixed-fashion illustration output">
</p>

#### V1 example B — Haaland profile and height / 哈兰德侧脸与身高范例

This pair demonstrates identity transfer and the `190 cm → 1.20` stylized leg scale while keeping the V1 clothing template fixed.

这组范例用于展示人物侧脸替换，以及 `190 cm → 1.20` 的风格化腿长比例；V1 的固定服装模板保持不变。

**Input photograph / 输入照片**

<p align="center">
  <img src="hm-generate-fixed-fashion-profile-v1/assets/examples/haaland-profile-input-rights-unverified.jpeg" width="420" alt="Haaland profile input photograph, publication rights unverified">
</p>

**Generated illustration / 生成插画**

<p align="center">
  <img src="hm-generate-fixed-fashion-profile-v1/assets/examples/haaland-profile-output.png" width="560" alt="V1 Haaland profile and 190 cm height illustration output">
</p>

> 来源说明：参考输入图片均来自网络，如有侵权请告知撤换，仅作示例用。

### V2 — variable fashion / 百变穿搭

The female silver-suit pair demonstrates V2's defining behavior: preserve the visible clothing category, silhouette, layers, colors, accessories, and shoes from the uploaded photograph, then translate them into the established loose illustration language. This is an example, not a fixed female clothing template.

银灰套装女性范例用于说明 V2 的核心功能：保留上传照片中可见的服装类别、廓形、层次、颜色、配饰与鞋子，再统一转译成既定的松散插画语言。它只是范例，不是固定女性服装模板。

**Input photograph / 输入照片**

<p align="center">
  <img src="hm-generate-variable-fashion-profile-v2/assets/examples/female-silver-suit-input-rights-unverified.jpeg" width="420" alt="Female silver-suit variable-fashion input photograph, publication rights unverified">
</p>

**Generated illustration / 生成插画**

<p align="center">
  <img src="hm-generate-variable-fashion-profile-v2/assets/examples/female-silver-suit-output.png" width="560" alt="V2 female silver-suit variable-fashion illustration output">
</p>

> 来源说明：参考输入图片均来自网络，如有侵权请告知撤换，仅作示例用。

## V1 and V2 at a glance

| Feature | V1 fixed fashion | V2 variable fashion |
| --- | --- | --- |
| Person identity | From uploaded profile photo | From uploaded person photo |
| Clothing | Locked bundled outfit | Follows visible clothing in the photo |
| Walking rhythm | Locked | Style-guided and consistent |
| Background | Warm paper and graph grid | Warm paper and graph grid |
| Optional height | Supported | Supported |
| Best input | Clear left-facing profile | Clear person photo with visible outfit |

## Height variable

Both skills use `170 cm` as the visual baseline:

```text
leg_scale = clamp(1 + (height_cm - 170) / 100, 0.80, 1.30)
```

Examples: `160 cm → 0.90`, `170 cm → 1.00`, `180 cm → 1.10`, `190 cm → 1.20`.

This is an illustration proportion rule, not an anatomical measurement. 输入人物身高即可估算插画中的大概腿长比例，不代表真实人体测量结果。

## Repository structure

```text
hm-generate-fixed-fashion-profile-v1/
├── SKILL.md
├── agents/openai.yaml
├── assets/
└── references/

hm-generate-variable-fashion-profile-v2/
├── SKILL.md
├── agents/openai.yaml
├── assets/
└── references/
```

## Installation

Copy either complete skill directory into your Codex skills directory. Keep the directory name unchanged because it must match the `name` field in `SKILL.md`.

```text
~/.codex/skills/hm-generate-fixed-fashion-profile-v1/
~/.codex/skills/hm-generate-variable-fashion-profile-v2/
```

Restart or refresh Codex after installation if the skills do not appear immediately.

## Input guidance

- V1 works best with a clear left-facing profile. It ignores the source photo's clothing and background.
- V2 needs enough visible clothing to identify the intended outfit. If trousers, skirt, or shoes are hidden, provide another photo or a short text description.
- Height is optional; omitted height defaults to `170 cm`.
- Exact logos and unreadable text are normally simplified or omitted.

## Naming

- Human-facing prefix: `HM`
- Machine-readable skill names: `hm-generate-fixed-fashion-profile-v1` and `hm-generate-variable-fashion-profile-v2`

Codex skill names use lowercase letters, digits, and hyphens. The uppercase `HM` prefix is retained in the interface display names.
