# Print and documents

The pilot welcome guides (`docs/pilot-welcome-en.pdf`, `docs/pilot-welcome-af.pdf`), the exporter data agreement and onboarding notes, and any deck for an exporter follow the same system as the app, on paper.

## Page

- A4 portrait, 20 mm margins, one column of text at most 75 characters wide; a second column only for a table.
- Body in Source Sans 3 at 11 pt on 15 pt. Headings in Bricolage Grotesque: the title 28 pt, a section 16 pt, a subsection 12 pt, all 700.
- Colour on paper: `ink` of the light theme for text, `primary` for headings and links, the kind tints only behind a table row or a callout. Nothing relies on colour alone, since the guide is often printed in black and white.
- The lockup (`logo/feno-lockup.svg`) at 32 mm wide top left of the first page; the one-colour mark 8 mm at the foot of every page with the page number.
- Screenshots come from the Screenshots workflow (`e2e/screens.spec.ts` with `SCREENSHOTS=1`), on a phone frame, in the language of the document, at 60 mm wide, with a one-line caption under each.

## Decks

- 16:9. One idea per slide, the idea in the title. Titles in the display face at 36 pt, body 20 pt, never smaller than 16 pt.
- Dark ground slides use the dark theme's `bg` and `ink`; light slides the light theme's. Not both in one deck.
- Charts follow the dataviz rules in `src/components/charts.tsx`: one axis, the series in the `viz-*` colours, a table slide after a chart slide for anyone who wants the numbers.
- A grower's figures never appear in a deck for an exporter unless that grower shares them with that exporter in Feno already.

## Documents that are agreements

The exporter data agreement and the privacy policy are plain text in the voice (`voice.md`), with numbered sections, no colour, and the date and version at the top. The policy in the app (`src/pages/Privacy.tsx`) is the master; a printed copy says which version it is.

## Files

Masters for print live beside the documents in `docs/`. The brand assets they use (the lockup, the mark, the fonts) are the ones in this folder; nothing is redrawn for print.
