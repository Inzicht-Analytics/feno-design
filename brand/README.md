# Feno brand library

## What this is

The one place that says what Feno looks, sounds and feels like: in the app, in the pilot welcome PDFs, in exporter decks, in WhatsApp and email, in print and on a website one day. It is written for Belinda and Claude first; a designer or a second codebase can join later without the library changing shape. The design behind it is in `docs/superpowers/specs/2026-11-07-feno-brand-library-design.md`.

The direction, in one line: **a field notebook with Headspace polish.** Warmth and craft from paper, soil and leaf tones and illustration. Finish from type hierarchy, spacing, soft depth and motion. The only fixed thing is the name, Feno.

| File | What it holds |
| --- | --- |
| `identity.md` | Name, promise, personality, what Feno is not |
| `voice.md` | Tone and wording, English and Afrikaans side by side |
| `logo.md`, `logo/` | Mark, wordmark, lockups, clear space, sizes, misuse; the SVG masters |
| `colour.md`, `type.md`, `spacing.md`, `motion.md` | The visual system, each read from `tokens.json` |
| `illustration.md`, `photography.md` | When to draw, when a photo is allowed |
| `print.md`, `messaging.md` | The PDFs, WhatsApp, email and push |
| `tokens.json` | The one source of every value |
| `references/` | What Belinda shares, numbered, each with a note; `sources.md` for standing sources |
| `decisions.md` | A dated log of each choice and why |

## How values flow

```
brand/tokens.json  ──scripts/tokens.mjs──▶  src/tokens.css            (the app reads this; styles.css holds no values)
                                        ──▶  brand/figma-variables.json (loaded into the Figma file)
                                        ──▶  brand/colour.md, the pairs table between its markers
```

- Edit `tokens.json`, then run `npm run tokens` and commit `src/tokens.css`, `brand/figma-variables.json` and `brand/colour.md` with it. `npm run build` refuses a stale file.
- `tokens.json` follows the W3C design-tokens format: `$type`, `$value`, references written as `{color.leaf.700}`. Three layers: primitives (`color`, `font`, `space`, `radius`, `duration`, `easing`), semantic per theme (`theme.light`, `theme.dark`, the names the CSS uses), and component values only where a piece needs its own.
- Three unit tests guard it: every text pair listed in `$extensions.feno.pairs` meets its ratio in both themes (`src/lib/tokens.test.ts`); every variable the app uses is defined and every theme variable defined is used (same file); the committed `src/tokens.css` equals what the generator writes (`scripts/tokens.test.mjs`).
- Never write a hex colour in `src/styles.css` or a component. The stage drawings (`StageArt.tsx`) and Google's sign-in button are the only exceptions.

## Adding a reference

- **Something shared** (a screenshot, a link to one shot): the next number, a folder `references/NNN-<short-name>/` with the image(s) and a `note.md` under three headings: *Source*, *Take*, *Leave*.
- **A standing source** (a gallery, a site to search): one line in `references/sources.md` with what it is good for and what to search there.
- Whenever a reference changes a token or a component, add a dated line to `decisions.md` pointing at it.

## Figma

One file, **Feno brand**, on Belinda's team. Pages: *Tokens*, *Components*, *Directions*, *Screens*. Code is the master: the variable collections are loaded from `brand/figma-variables.json`, and the components are pushed from the app's `/brand` screen. An edit made in Figma is reported and the token is changed in code; nothing flows back by itself.

File: https://www.figma.com/design/XNIou2IncdVbQeYsjAYjZt (key `XNIou2IncdVbQeYsjAYjZt`), created 8 November 2026 with the pages *Tokens*, *Components* and *Directions* (the starter plan allows three pages, so screens go on *Directions*). The variable collections generated into `brand/figma-variables.json` by `npm run tokens` are loaded as *Primitives*, *Theme Light*, *Theme Dark* and *Scale* (the starter plan allows one mode per collection, so Light and Dark are two collections rather than two modes of one). *Tokens* carries the type, motion and depth values as text; *Components* holds the core pieces bound to the Theme Light variables; *Directions* records the choices with links to the review pages. Loading again after a token change: run the variable script in a session with the Figma connection (it skips when collections exist; delete them first to reload). Publishing a team library needs a Professional plan; until then the file itself is the library. Caught up on 8 November 2026 after the imagery change: `stage-plate` and `stage-plate-2` added to *Theme Light* and *Theme Dark* (and `color/leaf/775` to *Primitives*), and a *Growth stages* frame on *Components* with image renders of the 21 clay-like drawings in both themes, because Figma cannot hold the SVG filter that draws them; the master stays `src/components/StageArt.tsx`.

## The `/brand` screen

The app shows every component in every state, both themes and both languages, at `/brand` when `VITE_BRAND=on`. CI builds with it on; it is never set in production. Live contrast ratios are read from the tokens on that screen.

## Splitting out

The day a second consumer exists (a website, a second app), this folder becomes its own repository:

1. `git filter-repo --subdirectory-filter brand` on a fresh clone keeps the folder's history.
2. Publish `tokens.json` as a small package (or fetch it at build time).
3. Point `scripts/tokens.mjs` at the package in `node_modules` instead of `brand/tokens.json`.
4. The `/brand` screen stays in the app; it only reads tokens.

A morning's work; nothing in the app changes shape.
