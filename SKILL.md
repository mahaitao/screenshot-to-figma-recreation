---
name: screenshot-to-figma-recreation
description: 图片转figma. Recreate provided screenshots or images as editable Figma design files or frames with pixel-matched canvas size, OCR-accurate editable text, editable UI layers, and separate image layers for complex visuals. Use when a user asks for 图片转figma, image-to-Figma, screenshot-to-Figma, or asks to restore, trace, clone, imitate, copy, recreate, or convert a screenshot/image into a Figma file/design draft while prioritizing visual fidelity over redesign or component reuse.
---

# 图片转figma

## Goal

Treat the task as screenshot tracing, not UI redesign. Preserve the original composition and prioritize:

1. Visual fidelity
2. Editable layers
3. Component reuse

Do not beautify, modernize, reinterpret, reorganize, or add content that is not visible in the source screenshot.

## Workflow

1. Inspect the source screenshot dimensions and create one main Figma frame whose width and height exactly match the image pixels.
2. If the user provides an existing Figma file, append a new clearly named frame/page without overwriting existing work. If no target exists and Figma creation tools are available, create a new Figma file.
3. Run OCR or manually transcribe visible text. Preserve capitalization, punctuation, line breaks, alignment, and visible truncation. Use `[unreadable]` for text that cannot be read; do not guess.
4. Rebuild the base UI with editable Figma layers: background blocks, cards, nav bars, buttons, dividers, simple icons, badges, lines, masks, and text.
5. Treat photos, complex illustrations, 3D icons, textures, complex gradients, and complex lighting as image layers. Extract them from the screenshot when possible; otherwise generate close visual replacements with available image generation/image2 tools.
6. Keep each independent visual object as its own image asset and image layer. Do not merge separate illustrations or photos into one large screenshot layer.
7. Put every image layer inside its owning frame/card/mask. Recreate clipping, rounded corners, occlusion, and stacking with `clipsContent` or masks.
8. Name layers by region and role so another designer can edit the file without reverse engineering it.
9. Compare the finished Figma output against the source screenshot and adjust position, size, color, radius, shadows, opacity, and stacking before reporting completion.

## Canvas And Layout Rules

- Match the original screenshot canvas size exactly.
- Preserve overall scale, aspect ratio, crop, and composition.
- Position elements as close as possible to the original x/y coordinates.
- Match width, height, spacing, corner radius, stroke, shadow, blur, opacity, and layer order.
- Do not use responsive reinterpretation unless the user provides multiple screenshots for multiple viewports.
- When appending to an existing Figma file, create an independent, clearly named frame or page instead of replacing existing content.

## Text Rules

- Recreate all visible text as editable Figma Text layers.
- Preserve casing, punctuation, spacing, line breaks, and alignment.
- Use `[unreadable]` for unreadable text. Do not invent likely copy.
- Do not bake text into image layers.
- Match font family, size, weight, line height, letter spacing, color, and opacity as closely as possible.
- If the exact font is unavailable, choose the closest available visual match and keep the text editable.

## Editable Layer Rules

Rebuild these as editable Figma primitives whenever practical:

- Backgrounds and section blocks
- Navigation bars, tab bars, menus, and sidebars
- Cards, sheets, modals, and list rows
- Buttons, chips, tags, pills, inputs, and toggles
- Dividers, strokes, simple geometric icons, progress bars, and badges
- Text, labels, headings, captions, counters, and metadata

Use SVG/vector for simple icons only when it preserves the screenshot's visual style. Do not replace source-specific icons with unrelated default library icons.

## Complex Image Rules

Use separate image layers for:

- Photos and avatars
- Complex illustrations
- 3D icons and rendered objects
- Complex textures, gradients, shadows, glow, and lighting effects
- Any region where editable reconstruction would reduce visual fidelity too much

Apply these constraints:

- Extract visual objects from the screenshot if possible.
- If extraction is not possible, generate a similar asset by calling the available image generation capability, such as image2 or image_gen. This is mandatory for final complex image assets.
- Do not substitute Python drawing, SVG drawing, CSS/gradient drawing, simple vector approximation, or placeholder artwork for a final complex image asset unless the user explicitly allows that fallback.
- Do not generate text, labels, numbers, or watermarks inside generated image assets.
- For transparent assets, generate or process a clean transparent PNG. If needed, use a flat chroma-key background and remove it locally.
- Save every generated or extracted final image asset to the local project directory.
- Upload each final image asset to Figma and apply it as an IMAGE fill or image node.
- Keep each distinct source visual as a separate asset and layer.
- Place each image inside its semantic parent frame/card/mask.
- Recreate clipping and rounded crops through the parent frame's clipping/mask behavior.

Use clear asset/layer names such as:

- `Image2 asset / shortcut / ...`
- `Image2 asset / feature / ...`
- `Image2 asset / category / ...`
- `Image layer / photo / ...`
- `Image layer / avatar / ...`

## Figma Implementation

When using Figma tools, follow the required Figma tool skills and protocols before calling Figma MCP operations. In particular, load the relevant Figma skill before `create_new_file`, `use_figma`, `generate_figma_design`, or diagram/slide-specific tools when those operations are needed.

Implementation expectations:

- Create or reuse the target Figma file requested by the user.
- Create the screenshot-matched main frame.
- Build basic UI as editable layers.
- Use independent IMAGE layers for complex visuals.
- Keep images inside the correct parent frames or cards.
- Use clipping or masks where the screenshot shows cropped content.
- Avoid screenshot-as-background shortcuts except temporarily for tracing. Remove or hide tracing references in the final deliverable unless the user asks to keep them.
- Do not combine independent images into a single large image fill.
- Do not rasterize text.

## Final Self-Check

Before responding, verify:

- Canvas size exactly matches the source screenshot.
- OCR is complete, including capitalization, punctuation, and line breaks.
- Unreadable text is marked `[unreadable]`.
- Text remains editable.
- Colors, spacing, radius, shadows, opacity, and stacking are close to the screenshot.
- No unexpected redesign, beautification, or added content appears.
- Complex photos/illustrations/3D/texture regions are image layers.
- Any complex image asset that could not be extracted from the source screenshot was generated with image2/image_gen, not with ad hoc code drawing or placeholders.
- Independent visual objects are separate image layers, not one merged image.
- Image layers sit inside the correct frame/card/mask and clipping is enabled where needed.
- Layer names are clear and grouped by area/function.
- The final Figma link is available.

## Final Response

Report the Figma link and briefly state:

- The frame name and canvas size.
- Which regions are editable layers.
- Which regions are image layers and where their local assets were saved.
- Which image layers were extracted from the source screenshot and which were generated with image2/image_gen.
- Any text marked `[unreadable]`.
- Any limitations, such as unavailable exact fonts or generated approximations for complex assets.
