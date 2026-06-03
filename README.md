# Screenshot to Figma Recreation

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

The skill focuses on screenshot tracing, editable text and UI layers, and separate image layers for complex visuals.

## Notes

- This skill can improve recreation fidelity by treating the task as screenshot tracing rather than UI redesign.
- It can call image generation tools to create image assets, fill them directly into Figma, and preserve cropped visuals through the parent Frame's `clipsContent` setting or a mask.
- For related complex icons or illustrations in the same functional area, the preferred workflow is to generate one image2/image_gen contact sheet, crop that generated sheet into separate assets, and fill each Figma image layer independently. The final screenshot should be used as layout reference, not as the default source for generated-style complex assets.
- Versioning rule: unless a special version change is requested, each update increments the previous version by `+0.0.1`.

### Version History

- `v1.0.2` - `2026-06-03 17:55 +08:00` - Clarified that generated-style complex assets should use image2/image_gen by default; related assets can be generated as one contact sheet, cropped into independent PNG assets, and filled back into Figma separately.
- `v1.0.1` - `2026-06-03 11:03 +08:00` - Added notes that the skill can improve recreation fidelity and can use image generation assets with Figma IMAGE fills, parent `clipsContent`, or masks.
- `v1.0.0` - `2026-06-03 10:39 +08:00` - Initial skill release for screenshot tracing, editable text/UI layers, and separate image layers for complex visuals.
