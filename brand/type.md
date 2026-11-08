# Type

Feno serves its own fonts (`decisions.md`, 7 November 2026): two variable files in `public/fonts`, both under the SIL Open Font License, precached with the app so they are there without signal. Google Fonts is no longer used anywhere.

## The faces

| Role | Family | Weights served | File | Token |
| --- | --- | --- | --- | --- |
| Display: headings, the wordmark, the hero number, numbers on tiles | **Bricolage Grotesque** | 500 to 700, optical size 96 | `public/fonts/bricolage-grotesque-latin.woff2` (77 KB) | `--font-display` |
| Body: everything else | **Source Sans 3** | 400 to 700 | `public/fonts/source-sans-3-latin.woff2` (29 KB) | `--font-body` |

Both are latin subsets, which cover every letter Afrikaans uses (ê, ë, ô, û, ’) and the degree sign. Fallbacks are the phone's own sans. `@font-face` is written into `src/tokens.css` from `tokens.json` → `$extensions.feno.fonts`, with `font-display: swap`, so text shows at once in the fallback and swaps when the file is read.

## The scale

Set in `src/styles.css`; the body is 16 px and nothing on a screen a grower taps is smaller than 0.72 rem (the pill bar's labels).

| Element | Size | Weight | Face | Notes |
| --- | --- | --- | --- | --- |
| Hero number | 2.6 rem | 700 | display | Letter-spacing −0.01 em, tabular figures; its unit at 1 rem beside it |
| Weather temperature | 2.4 rem | 700 | display | |
| h1 | 1.7 rem | 700 | display | Balanced wrapping, letter-spacing −0.01 em |
| Tile and stat numbers | 1.5 rem | 700 | display | Tabular figures |
| h2 | 1.15 rem | 700 | display | |
| Wordmark in the header | 22 px tall | 800 | display (as an SVG) | `logo.md` |
| h3, buttons, labels | 1 rem | 700 | body | Buttons 700, field labels 700 |
| Body | 1 rem / 1.5 | 400 | body | Inputs 17 px, so iOS does not zoom |
| Meta, hints | 0.9 / 0.88 rem | 400 to 600 | body | In `muted` |
| Eyebrow | 0.78 rem | 700 | body | Upper case, letter-spacing 0.06 em |
| Pill bar labels | 0.72 rem | 700 | body | |

## Rules

- Headings are 700 in the display face; nothing else is. Weight carries the hierarchy, not colour.
- Numbers that line up (tables, stat rows, the hero) use tabular figures.
- Afrikaans runs about 30 percent longer: a label is checked at 360 px in Afrikaans before it ships (`e2e/brand.spec.ts` does this for the pill bar).
- No italics in the interface. Emphasis is 600 or 700 weight.
- No text smaller than 0.72 rem, and that only on the bar. Legal text (the privacy policy) is body size.

## Changing a face

Pick an OFL face, add its latin woff2 and licence to `public/fonts`, list it under `$extensions.feno.fonts` and change `font.display` or `font.body` in `tokens.json`, run `npm run tokens`. `scripts/fonts.test.mjs` checks the files exist and are precached. The privacy policy does not change (Feno serves the file; no third party learns anything).
