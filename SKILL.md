---
name: screenshot-to-figma-recreation
description: image to figma. Recreate provided screenshots or images as editable Figma design files or frames with pixel-matched canvas size, OCR-accurate editable text, editable UI layers, editable SVG/component icons for simple UI symbols, and separate image layers for complex visuals. Use when a user asks for image to figma, 图片转Figma, image-to-Figma, screenshot-to-Figma, or asks to restore, trace, clone, imitate, copy, recreate, or convert a screenshot/image into a Figma file/design draft while prioritizing visual fidelity over redesign or component reuse.
---

# image to figma

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
4. Rebuild the base UI with editable Figma layers: background blocks, cards, nav bars, buttons, dividers, simple UI icons, badges, lines, masks, and text.
5. Treat simple UI icons, line icons, filled glyphs, and small flat symbols as editable vectors or component instances. Use the user's icon library or original SVG sources before hand-drawing paths.
6. Treat photos, avatars, complex illustrations, 3D icons, textures, complex gradients, and complex lighting as image layers. Use image generation/image2 as the default asset source for generated-style illustrations, 3D assets, product renders, decorative visual objects, complex rendered icons, real-person photos, and avatar portraits instead of cropping the final screenshot.
7. Keep each independent visual object as its own image asset and image layer. Do not merge separate illustrations or photos into one large screenshot layer.
8. Put every image layer inside its owning frame/card/mask. Recreate clipping, rounded corners, occlusion, and stacking with `clipsContent` or masks.
9. When several complex icons or illustrations in the same functional region share one style, generate them as one image2/image_gen contact sheet when practical, then crop that generated sheet into separate local PNG assets and fill the corresponding Figma nodes individually.
10. For hero, promo, and feature cards with one continuous complex visual background, rebuild the card as a full-card image background with editable text/UI overlays rather than splitting the background into unrelated vector approximations.
11. Name layers by region, role, and source so another designer can edit the file without reverse engineering it.
12. Compare the finished Figma output against the source screenshot and adjust position, size, color, radius, shadows, opacity, and stacking before reporting completion.

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

Use SVG/vector/component instances for simple icons when it preserves the screenshot's visual style. Do not replace source-specific icons with unrelated default library icons.

Do not use SVG, hand-drawn vectors, CSS gradients, or Python-drawn placeholders to approximate complex illustrations, 3D icons, product renders, or photo-like assets. If a visual has lighting, material, depth, texture, or painterly detail, make it an IMAGE layer backed by image_gen/image2 or another real raster asset.

## Icon And Simple Vector Rules

Use this section for simple UI icons, line icons, filled glyphs, common navigation symbols, status symbols, small flat illustrations, and other low-complexity vector-like shapes. This section must not override the complex image rules: complex illustrations, rendered 3D icons, product imagery, textures, and photo-like assets still use image_gen/image2 or other raster assets first.

Default user icon library:

- Name: `icon-library`
- URL: https://www.figma.com/design/tyn2BHErZDe4nECltSPdpQ/icon-library?node-id=2004-3620&t=TYqMHHBR5iUihCS5-1
- Figma file key: `tyn2BHErZDe4nECltSPdpQ`
- Starting node id: `2004:3620`

Simple icon source priority:

1. Exact or near-exact component from the user's Figma `icon-library`.
2. Original SVG from a user-provided free/open icon library.
3. Existing Figma component or vector from the target file/design system.
4. Auto-vectorized or traced SVG from a tightly cropped icon reference, then manually cleaned.
5. Hand-drawn SVG path only as a last resort.
6. Raster image only when editability is less important than fidelity, or when the icon is actually a complex rendered/image asset.

When using an icon library component:

- Preserve it as a component instance when possible.
- Resize proportionally to match the screenshot's bounding box.
- Tune stroke width, stroke cap, stroke join, fill, opacity, corner radius, and color to match the source screenshot.
- Detach only when necessary for visual fidelity, and keep the resulting vector editable.
- Name the layer with its source, for example `Icon library / tab / home` or `Icon SVG / wallet / coupon`.

When tracing an icon:

- Crop the source icon tightly and inspect it enlarged before drawing.
- Match the actual silhouette, internal negative space, stroke endings, and alignment to the pixel reference.
- Prefer fewer clean paths over many noisy points, but do not simplify away recognizable features.
- Overlay-check the vector against the screenshot before considering it finished.

Do not use image_gen/image2 for simple flat UI icons only because the image-generation path is convenient. Conversely, do not force complex rendered icons into SVG paths only because editability is desired.

## Complex Image Rules

Use separate image layers for:

- Photos and avatars
- Complex illustrations
- 3D icons and rendered objects
- Complex textures, gradients, shadows, glow, and lighting effects
- Any region where editable reconstruction would reduce visual fidelity too much

Apply these constraints:

- Use the source screenshot primarily as layout/OCR/reference, not as the default source for complex visual assets.
- For generated-style illustrations, 3D objects, product renders, decorative visual assets, complex rendered icons, real-person photos, and avatar portraits, call the available image generation capability, such as image2 or image_gen. This is mandatory unless the user explicitly allows another source.
- For real-person photos and avatar portraits, prefer generated raster assets over source-screenshot crops. Use the screenshot only as visual reference for pose, crop, lighting, clothing, approximate age/gender/presentation, and palette; do not claim identity preservation unless the user explicitly asks for exact source-photo preservation.
- Do not crop complex generated-style assets, real-person photos, or avatars from the final screenshot just because it is easier. Source-screenshot crops are allowed only when the user explicitly requests exact screenshot crops, when an exact logo/brand mark must remain unchanged, when exact original-photo identity is more important than generated approximation and the user has accepted that exception, or when image generation is unavailable and the limitation is reported.
- For a group of related complex assets with the same style, prefer generating one contact sheet/sprite sheet with clear spacing and no text, labels, numbers, or watermarks. Then crop the generated sheet into independent assets before uploading to Figma.
- Do not substitute Python drawing, SVG drawing, CSS/gradient drawing, simple vector approximation, or placeholder artwork for a final complex image asset unless the user explicitly allows that fallback.
- Do not generate text, labels, numbers, or watermarks inside generated image assets.
- For transparent assets, generate or process a clean transparent PNG. If needed, use a flat chroma-key background and remove it locally.
- Save every generated or extracted final image asset to the local project directory.
- When cropping a generated sheet, save both the sheet and every cropped asset locally. Keep a manifest or clear file naming that maps each crop to its target Figma layer/node.
- Upload each final image asset to Figma and apply it as an IMAGE fill or image node.
- Keep each distinct source visual as a separate asset and layer.
- Place each image inside its semantic parent frame/card/mask.
- Recreate clipping and rounded crops through the parent frame's clipping/mask behavior.

## Hero And Complex Card Background Rules

When a hero, promo, feature, membership, offer, or banner card contains a continuous visual treatment across the card, classify that treatment as a card background image layer. Continuous visual treatment includes rendered people or products blended into glows, waveforms, abstract lighting, textured gradients, atmospheric effects, decorative illustrations, and non-uniform background art.

For these cards:

- Create the card frame at the exact screenshot position and size.
- Set the card frame's radius and `clipsContent`/masking so the image background is clipped by the card shape.
- Generate or source one full-card background image for the complex visual treatment, with no text, labels, numbers, logos, buttons, badges, or UI copy baked into the image.
- Fill the full card with that image layer first, then overlay all readable content as editable Figma layers: headings, subtitles, counters, badges, avatar stacks, buttons, chips, icons, and metadata.
- If a card has an irregular silhouette or decorative cutout, use the closest editable mask/vector for the card shape and keep the complex visual as an image fill clipped by that shape.
- If the screenshot clearly shows separate independent images inside the card, keep those as separate image layers. Otherwise prefer one full-card background image so gradients, glow, and illustration edges stay visually continuous.
- Name these layers explicitly, for example `Image2 asset / hero card background / no text` and `Hero overlay / title`.

Use clear asset/layer names such as:

- `Image2 asset / shortcut / ...`
- `Image2 asset / feature / ...`
- `Image2 asset / category / ...`
- `Image2 sheet crop / shortcut / ...`
- `Image2 sheet crop / feature / ...`
- `Image layer / photo / ...`
- `Image layer / avatar / ...`

## Figma Implementation

When using Figma tools, follow the required Figma tool skills and protocols before calling Figma MCP operations. In particular, load the relevant Figma skill before `create_new_file`, `use_figma`, `generate_figma_design`, or diagram/slide-specific tools when those operations are needed.

Implementation expectations:

- When writing JavaScript color helpers for Figma paints, support CSS short hex forms before parsing. Expand `#rgb` to `#rrggbb` and `#rgba` to `#rrggbbaa`; do not slice `#fff`, `#000`, or `#777` as if they were six-digit colors. Invalid hex strings should throw instead of silently producing wrong colors.
- Create or reuse the target Figma file requested by the user.
- Create the screenshot-matched main frame.
- Build basic UI as editable layers.
- Use the user's icon library or original SVG sources for simple UI icons before hand-drawing SVG paths.
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
- Simple UI icons use accurate editable vectors/component instances from the user's icon library or another original SVG source where practical.
- Colors, spacing, radius, shadows, opacity, and stacking are close to the screenshot.
- No unexpected redesign, beautification, or added content appears.
- Complex photos/avatars/illustrations/3D/texture regions are image layers.
- Generated-style illustrations, 3D objects, product renders, complex rendered icons, decorative assets, real-person photos, and avatar portraits were generated with image2/image_gen, either as individual assets or as a generated sheet that was then cropped.
- Hero, promo, feature, and banner cards with continuous complex visuals use a full-card background image layer with editable text/UI overlays.
- No generated-style complex asset, real-person photo, or avatar portrait was taken from a final screenshot crop unless the user explicitly allowed that exception, exact original-photo identity was required, image generation was unavailable, or the asset was an exact logo/brand mark.
- No complex image asset was substituted with SVG/vector/CSS/Python-drawn approximation unless the user explicitly allowed that fallback.
- Independent visual objects are separate image layers, not one merged image.
- Image layers sit inside the correct frame/card/mask and clipping is enabled where needed.
- Any generated sheet used for related assets was saved locally, cropped into independent assets, and mapped to the correct Figma nodes/layers.
- Layer names are clear and grouped by area/function.
- The final Figma link is available.

## Final Response

Report the Figma link and briefly state:

- The frame name and canvas size.
- Which regions are editable layers.
- Which simple icons came from the user's Figma icon library, another SVG source, tracing, or hand-drawn paths.
- Which regions are image layers and where their local assets were saved.
- Which image layers were generated with image2/image_gen, including full-card hero/background images, generated photos/avatar portraits, any generated sheet/contact sheet, and its cropped local assets.
- Any source-screenshot crop exceptions and why they were explicitly requested or necessary, such as exact logo/brand marks, accepted exact-photo preservation, or image generation being unavailable.
- Any text marked `[unreadable]`.
- Any limitations, such as unavailable exact fonts or generated approximations for complex assets.
