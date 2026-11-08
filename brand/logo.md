# Logo

Chosen by Belinda on 8 November 2026 from three marks and three wordmarks (`logo/explorations/`, `decisions.md`).

## The pieces

| File | What it is | Where it goes |
| --- | --- | --- |
| `logo/feno-mark.svg` | The mark: one leaf with a single midrib on the leaf-green plate, a pomegranate-pink sun clear of its tip. Rounded corners of 22 on 100. | The app icon (`public/icon.svg`, and the PNGs `scripts/icons.mjs` renders), the sign-in card, the install step |
| `logo/feno-mark-mono.svg` | The leaf and sun in one colour (`currentColor`), no plate | Stamps, print in one colour, a favicon on a plate of its own |
| `logo/feno-wordmark.svg` | "Feno" in Bricolage Grotesque at 800, tracked tight, with a leaf in the counter of the o in leaf green. The letters take the colour of what they sit on (`fill` on the group). | The header of documents, decks and the website; the sign-in heading |
| `logo/feno-lockup.svg` | The mark at the wordmark's cap height, then the wordmark, on one baseline | Covers, email headers, anywhere both are wanted |

The explorations stay in `logo/explorations/` as the record of what was considered.

## Colour

- The mark is always on its plate in `primary` (light `#187640`) with the leaf in `white` and the sun in `pom` (dark-theme value `#F0919F`, which is the only pink that reads on the green). It does not change with the theme.
- The wordmark's letters are `ink` on a light surface and `ink` of the dark theme on a dark one: in the app, `currentColor`. The leaf in the o is always `primary` of the light theme.
- One-colour: `feno-mark-mono.svg` in `ink`, `on-primary` or print black. Never in a tint.

## Clear space and size

- Clear space all round the mark and the lockup: the height of the sun (8 on 100 of the mark; the o's counter height for the wordmark).
- Minimum sizes: the mark 16 px (favicon), the wordmark 64 px wide, the lockup 120 px wide. Below that use the mark alone.
- The app icon is the mark exactly; maskable icons need no extra padding, the plate is the safe area.

## Misuse

- Never stretch, rotate or add a shadow or outline.
- Never set the wordmark in another face or weight, or add a tagline inside the lockup.
- Never put the mark on a photo without its plate, or on a tint (`-soft` colours).
- Never recolour the sun or the leaf; the one-colour version is the only other version.
- The name is written "Feno", never "FENO" in running text (the spaced capitals exploration is not used).

## Changing it

Edit the SVG in `logo/`, copy the mark to `public/icon.svg`, run `node scripts/icons.mjs`, and check `/brand` → Logo in both themes. The sign-in and install screens show the icon, so the axe run covers it.
