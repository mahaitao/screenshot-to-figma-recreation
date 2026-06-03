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
