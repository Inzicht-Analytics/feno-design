# Spacing, shape and depth

## The scale

A 4 px scale, `space/1` to `space/8` in `tokens.json` (`--space-1` 4 px to `--space-8` 32 px). The stylesheet uses these sizes directly; the most common are 8 (between related things), 12 (inside a tile), 16 (the page gutter), 18 (inside a card) and 20 (between cards in a stack).

| Where | Value |
| --- | --- |
| Page gutter on a phone | 16 px, more on the sides a system bar takes (`env(safe-area-inset-*)`) |
| Between cards in a stack | 20 px (`.stack`), 10 px for a tight stack |
| Inside a card | 18 px |
| Inside a tile | 12 px |
| Between a label and its field | 6 px |
| Between the pill bar and the screen edges | 12 px plus the safe area |

## Targets

Everything a grower taps is at least 44 px in both directions; primary buttons and inputs are 52 px; tabs 52 px; icon buttons 48 px. `e2e/brand.spec.ts` measures every control on the `/brand` screen in Afrikaans.

Edit and delete are icon buttons (`iconbtn`, `iconbtn danger`): a pencil or a bin, 48 px round, with the action's name as the accessible label and on hover. They sit in a card's top right corner (`card-tools`) or in the card's action row; a card with no heading row (Farm details) gives them their own row at the right (`tools-row`), so they never sit over the first line. Full-width buttons are for what a grower does every day on that card, such as Season view and Log (decisions, 8 November).

## Shape

| Token | Value | Used for |
| --- | --- | --- |
| `radius/card` | 14 px | Cards, drawers, the map panel, dialogs |
| `radius/tile` | 12 px | Tiles, notices, choice rows, stat tiles |
| `radius/button` | 10 px | Buttons, inputs, the farm switch |
| `radius/pill` | 999 px | The pill bar, chips, badges, segments |
| `radius/focus` | 6 px | The focus ring |

Icon plates on tiles are circles (`references/003`). The mark's plate is 22 on 100.

## Depth

Direction B drew crisp lines and no shadows; reference 003 asked for depth, and depth won (`decisions.md`, 8 November). Four levels:

| Level | Where | How |
| --- | --- | --- |
| Flat | The page, inputs, chips, notices | A 1 px `line-soft` border, no shadow |
| Resting | Cards, tinted tiles, stat tiles, the sign-in card | `--elevation`: a lit top edge in `highlight`, a 1 px close shadow and a soft one 14 px below in `shadow`; a tinted tile also gets `--lit` (light from above over its fill) and a shaded foot in `shade` |
| Raised | The icon plate on a tile, the weather icon, a crop badge, the Log button | `--raised`: the lit edge and a 2 px shadow, so the plate stands on the tile (`references/003`) |
| Floating | The pill bar, a chart tooltip, the photo viewer | A deeper shadow (`0 8px 24px shadow`) |

The wallpaper is the mark's leaf, 440 px, at 7 percent of `primary`, fixed top right behind every screen. It is a CSS mask so it takes the theme's colour, and it is hidden in Windows High Contrast.

## Layout

- One column on a phone, up to 560 px wide. Tablets 860 px. From 1000 px the pill bar becomes a left column and the content gets a second column where it has one (Home, the Season view, forms two across from 1200 px).
- Things that belong together sit in a grid with a gap, never with margins on each item.
- A header and the bar are sticky; `scroll-padding` keeps a focused control out from under them.
