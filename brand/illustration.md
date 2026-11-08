# Illustration

Feno draws rather than photographs. Three kinds of drawing, each with one job.

## 1. Icons (`src/components/Icon.tsx`)

Sixty-odd line icons on a 24 px grid, 2 px stroke, round caps and joins, no fills. With `duo` the closed shapes also get a fill of the same colour, lit from above: a gradient from 42 percent at the top to 12 percent at the foot, so a tile's icon reads as a raised shape at arm's length in the sun rather than a flat wash (decisions, 8 November). The line stays flat and the gradient is the icon's own colour, so every icon still takes its tile's hue. Every icon is paired with visible text; none is an accessible name on its own.

- One icon per kind of entry, the same everywhere (`colour.md`): the leaf is the growth stage, the sprayer the spray, the drop irrigation, the scissors pruning, the bug the pest count, the fig wasp pollination, the basket the harvest, the crate the day's pick, the flask the lab result.
- The fig and the pomegranate are drawn as the fruit, so a block shows its crop.
- New icons follow the grid and the stroke. Draw it in the `paths` map, check it on `/brand` → Icons in both weights.

## 2. Stage drawings (`src/components/StageArt.tsx`)

Simple original drawings of each BBCH growth stage, one branch running up and to the right with buds, leaves, flowers and fruit on it, so a grower can match what they see. They are clay-like (decisions, 8 November; `references/005`): every bud, leaf, flower and fruit is a rounded shape lit from the top left with a soft inner shade at the bottom right, drawn with one SVG filter and one radial gradient per plant colour, and the whole drawing casts a soft shadow onto its plate. The shapes are the same as before; only the light changed. The plant colours stay fixed (wood, bud, leaf, fruit) because they are pictures of plants, not interface, and they look the same in both themes; they are the one place in the app that may hold a hex colour. The plate is interface, so it reads the `stage-plate` tokens: pale green in light, deep green in dark. Each drawing carries its own defs under its own id, because the stage picker shows ten at once. All 21 are on `/brand` → Growth stages.

A real photo from a pilot farm can replace a drawing (`growth_stages.reference_photo_path`); the app prefers the photo when one exists.

## 3. The mark and the wallpaper (`logo.md`)

The leaf of the mark is Feno's one illustration beyond the icons: it is the app icon, the wallpaper behind every screen, and the leaf in the wordmark's o. It is a single closed curve with a midrib. Nothing else is drawn as "decoration".

## Rules

- Draw the idea, not the detail. A grower matches a shape, not a texture.
- Line icons stay line icons; no filled icon set is mixed in.
- No clip art, no emoji in the interface, no rendered 3D images (`references/001` → Leave; `references/005` → shaded SVG instead). Depth is drawn in with light and shade; a drawing stays a drawing.
- Illustration is never the only cue: an icon has a label, a stage drawing has its code and name.
- Anything drawn for print or a deck (`print.md`) uses the same leaf, the same icons at a larger size, and the same two crops.

## When a photo is right

See `photography.md`. In short: on sign-in and marketing surfaces only, never precached, never a grower's farm without permission.
