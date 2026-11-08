# Photography

Feno is offline first on farm phones with weak signal, and its running costs stay as low as they can. Photographs cost both. So the app draws (`illustration.md`), and photographs appear only where they earn their weight.

## Where a photograph may appear

| Surface | Allowed | How |
| --- | --- | --- |
| The app's screens | No | Drawn leaf, icons, stage drawings |
| Sign-in and the install step | Only as a small, lazy image | Never precached by the service worker; the screen must read without it |
| The website (one day) and decks | Yes | Real orchards, real fruit, real light |
| The pilot welcome PDFs | Yes, sparingly | One cover photograph at most |
| Feno Facts posts | Growers' own photos | Stored in the private bucket; shown only to people on Feno |
| A grower's diary photos | The grower's own | Theirs; shown to the farm and, only if ticked under *Also share*, to the exporter; never to anyone else |

## What a Feno photograph looks like

- An orchard in the Western Cape, in its real light: early morning or late afternoon, never flash, never studio.
- Figs and pomegranates on the tree, in the crate, in a hand. Leaves, bark, soil, irrigation lines, bins. Weather.
- People only when they are working and have agreed to be shown. Never a face as decoration.
- No stock photography of farming in general, no drone shots of fields that are not ours, no handshakes.
- Colour as it was. No filters, no heavy grading; the brand's green is in the leaves already.

## Rules

- A photograph never carries text or a control without the `scrim` plate behind them (`colour.md`).
- The mark never sits on a photograph without its plate (`logo.md`).
- A grower's farm, name, block names or figures never appear in marketing unless they said yes in writing, and the privacy policy says what Feno shares (CLAUDE.md → Privacy).
- Images for the web are WebP or AVIF, sized for the slot, with `loading="lazy"` and a real `alt` that says what is in the picture, or an empty `alt` when it is decoration.
- A photograph in the app would need the content security policy's `img-src` to allow its host first (`vercel.json`); the two map tile servers and Supabase are the only image hosts today.

## Sources

Belinda's own photographs from the pilot farms, with permission, are the library. Until there are enough of them, a surface that wants a photograph uses the drawn leaf instead.
