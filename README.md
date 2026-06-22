# Image to Figma

Codex skill for recreating screenshots or images as editable Figma designs.

## Install

Clone this repository into your Codex skills directory:

```powershell
git clone https://github.com/mahaitao/screenshot-to-figma-recreation.git "$env:USERPROFILE\.codex\skills\screenshot-to-figma-recreation"
```

## Use

Ask Codex to use:

```text
$screenshot-to-figma-recreation
```

```text
$image-to-figma
```

The skill focuses on screenshot tracing, editable text and UI layers, and separate image layers for complex visuals.

### Version History

- `v1.0.7` - `2026-06-22 16:28 +08:00` - Added screenshot type classification, proportional `402px` width normalization for complete mobile App screenshots, fidelity-safe Group/Frame/Auto Layout guidance, and incremental reuse of existing design-system variables, styles, components, and variants.
- `v1.0.6` - `2026-06-18 18:43 +08:00` - Added generated-image fill and crop rules, including FILL-by-default coverage checks, square contact-sheet crops, non-uniform stretch prevention, and geometry-safe handling for circular avatars and rendered icons.
- `v1.0.5` - `2026-06-16 16:00 +08:00` - Expanded complex image rules for avatars and real-person photos, preferring generated raster assets over final screenshot crops, and added hero/promo/feature card background handling with editable text and UI overlays.
- `v1.0.4` - `2026-06-05 11:09 +08:00` - Copilot version note: added the precise simple-icon workflow with the default `icon-library`, clarified image_gen/image2-first handling for complex generated-style assets, required source-crop exception reporting, and added a Figma short-hex color helper guard for `#fff`, `#000`, and `#777`.
- `v1.0.3` - `2026-06-03 18:13 +08:00` - Renamed the skill display name from `图片转figma` to `image to figma` while keeping the Chinese phrase as a trigger alias.
- `v1.0.2` - `2026-06-03 17:55 +08:00` - Clarified that generated-style complex assets should use image2/image_gen by default; related assets can be generated as one contact sheet, cropped into independent PNG assets, and filled back into Figma separately.
- `v1.0.1` - `2026-06-03 11:03 +08:00` - Added notes that the skill can improve recreation fidelity and can use image generation assets with Figma IMAGE fills, parent `clipsContent`, or masks.
- `v1.0.0` - `2026-06-03 10:39 +08:00` - Initial skill release for screenshot tracing, editable text/UI layers, and separate image layers for complex visuals.
