# Feno brand library: design

Decided with Belinda on 7 November 2026. This spec is the brief for the implementation plan.

## Goal

Feno works well and has good features. It lacks a stand-out look and feel. The brand library fixes that in two steps: a reference library for the whole Feno brand, kept in this repository, and a first re-skin of the app in the library's chosen direction, deployed before the in-season window starts on 1 December 2026.

The library is for everything Feno puts in front of people: the app, the pilot welcome PDFs, exporter decks, WhatsApp and email messages, print, and a website one day. Its first users are Belinda and Claude. A designer or a second codebase can join later without the library changing shape.

## Decisions already made

| Question | Decision |
| --- | --- |
| Scope | The whole brand, not only the app |
| Where it lives | A `brand/` folder in this repository now; split into its own repository once a second consumer (a website, say) exists |
| What is fixed | Only the name, **Feno**. The mark, palette, type and components are all open |
| Personality | A trusted field notebook: warm, calm, crafted, made by someone who knows orchards. Greens and earthy colours stay |
| Finish | Consumer-grade polish, in one line: *a field notebook with Headspace polish*. Lead references: Headspace, then Airbnb, Spotify, Slack, Uber, Dribbble, and the smart-home dashboard screenshot in `brand/references/001` |
| Master | Code is the master, Figma is the mirror |
| Pace | Library and first re-skin before 1 December; deploys Monday to Thursday mornings; the last deploy day is Thursday 26 November |
| Figma | Yes: one file, "Feno brand", on Belinda's team |

## Scope

In:

- The `brand/` folder with the brand book, tokens, references and decisions log.
- A token pipeline: `brand/tokens.json` generated into `src/tokens.css`, with tests.
- A `/brand` screen in the app behind `VITE_BRAND`, showing every component in every state, both themes, both languages.
- Three visual directions as mockups, one chosen and recorded.
- The first re-skin: shell, Home, Log menu, forms, Timeline.
- Self-hosted fonts, with the privacy policy, content security policy and service worker updated.
- A Figma file with tokens as variables and the components pushed from code.
- Logo and wordmark explorations.

Out, for now (each is a later small change, added to the library at its own pace):

- Print templates, messaging patterns, the illustration set, photography rules beyond the written principles.
- A website.
- A published Figma team library, if the starter tier does not allow it.
- Any change to a diary table, any new outside service.

## Folder layout

```
brand/
  README.md          what the library is, how to add to it, how it splits out later
  identity.md        name, promise, personality, what Feno is not
  voice.md           tone and wording, English and Afrikaans side by side
  logo.md            mark, wordmark, lockups, clear space, minimum sizes, misuse
  logo/              SVG masters, PNG exports at the sizes the app and documents need
  colour.md          palette, semantic roles, both themes, contrast table, crop and kind colours
  type.md            typefaces, scale, weights, line heights, bilingual notes (Afrikaans runs longer)
  spacing.md         4 px scale, layout grid, tap targets, safe areas
  motion.md          durations, easings, the named motions, reduced-motion rule
  illustration.md    the drawn style (from the stage art), when to draw and when not to
  photography.md     when photos are allowed, where they load from, never precached
  print.md           page sizes, margins, the PDF template rules
  messaging.md       WhatsApp, email and push patterns
  tokens.json        the one source of truth for every value
  references/        numbered items with a note each, plus sources.md
  decisions.md       dated log of each choice and why
```

Everything is Markdown and SVG so it reads on GitHub, and the whole folder moves to its own repository later with one `git mv`. `brand/README.md` says how.

## Tokens

### Format and layers

`brand/tokens.json` follows the W3C Design Tokens Community Group format (`$value`, `$type`, `$description`, references as `{group.name}`), so Figma and other tools can read it. Three layers:

1. **Primitives.** Raw values named by what they are. Colour ramps per hue (for example `leaf.100` to `leaf.900`, `soil`, `gold`, `fig`, `pom`, and the hues the kinds of entry use), a type scale, a 4 px spacing scale, radii, elevation, durations, easings. Primitives never appear in CSS.
2. **Semantic.** What the app refers to, per theme (`light`, `dark`). They keep today's names so nothing in `styles.css` is renamed: `bg`, `surface`, `surface-2`, `ink`, `muted`, `line`, `line-soft`, `shadow`, `primary`, `on-primary`, `primary-soft`, `focus`, `gold`, `warn`, `good`, `bad`, `fig`, `pom`, each kind colour and its `-soft` tint, `font-display`, `font-body`, `r`. New semantic tokens are added as the re-skin needs them (for example `bar`, `on-bar`, `hero`).
3. **Component.** Only where a component needs its own value, such as the bottom bar's fill or a tile's tint. Each references a semantic token.

### Generation

`scripts/tokens.mjs` reads `brand/tokens.json` and writes `src/tokens.css`: `:root` for light, the `prefers-color-scheme: dark` block guarded by `:root:not([data-theme="light"])`, and `:root[data-theme="dark"]`, exactly as `styles.css` declares them today. `styles.css` loses its token blocks and keeps everything else. `src/main.tsx` imports `tokens.css` before `styles.css`. `npm run build` and `npm run dev` run the generator first; `src/tokens.css` is committed so the app builds without it, and a test fails when it is stale.

### Tests

- Every text pair in the semantic layer, in both themes, is at least 4.5:1; every large-text and icon pair at least 3:1. The pairs are listed in the JSON itself (`$extensions.feno.pairs`) so the test and `colour.md`'s contrast table read the same list. Today this promise is a comment at the top of `styles.css` and nothing checks it.
- Every semantic token is used in `styles.css`, `charts.tsx` or the `/brand` screen, and every `var(--…)` used in the app is defined in the JSON.
- `src/tokens.css` equals what the generator writes from the JSON.

## Components and the `/brand` screen

### Inventory

Feno has about twenty pieces of interface, styled by class in `styles.css`. The library names each, lists its states, and the re-skin restyles it in place rather than rebuilding it:

- **Shell:** top bar (farm name, avatar), bottom tab bar with the Log button, sync bar, screen loader.
- **Surfaces:** card, tile (the per-kind Log tiles), notice (info, error, ok), chip and filter chip, badge and tag, key-value list, table wrap.
- **Actions:** primary, secondary, text and danger buttons, icon button, segmented control, pressed-button bars, the Google sign-in button (which keeps Google's own colours and rules).
- **Forms:** field with label, hint and error, error summary, search and suggest lists, confirm dialog, photo thumbs, map picker.
- **Content:** Timeline entry card, fact card, stage art, weather strip, stat row, the three chart types.
- **Brand pieces:** logo and wordmark lockups, the empty-state illustration style, a hero header for sign-in and install.

### New in the re-skin

Taken from the references and kept within the field-notebook personality:

- A **hero number** treatment: the one figure that matters on a screen set large, with its unit and label small.
- **Soft tinted fills** on cards and tiles, using the per-kind colours Feno already has, each still at least 4.5:1 for its text and icon in both themes.
- The bottom bar as a **floating dark pill** with one active label and the Log button as its centre.
- **Depth** from soft shadow and tint, never from 3D objects.
- A short set of **named motions**: saved, syncing, stage reached, screen enter. All off under `prefers-reduced-motion`.

Readability in sun and use with gloves stay non-negotiable: 44 px tap targets, 16 px body text, WCAG 2.1 AA in both themes.

### The `/brand` screen

A route at `/brand` inside the normal shell, shown only when `VITE_BRAND=on` (read in `src/lib/features.ts` like the other switches; CI builds with it on). Linked from nowhere in the app. It shows, with a theme and language switch at the top:

- colour swatches with contrast ratios read live from the tokens;
- the type scale, spacing scale, radii and elevation;
- the icon set;
- every component in every state;
- the motions, each with a play button;
- the logo lockups.

It runs through the existing axe check (`e2e/a11y.spec.ts`) in light, dark, English and Afrikaans. Its text is in `src/lib/i18n.tsx` in both languages like any screen.

## Visual directions

Before the tokens are settled, three directions are drawn as mockups of the Home screen and the Log menu: the same personality, each with a different palette and type pairing. They are drawn in the Figma file and published as a page Belinda can open on her phone. Belinda picks one or mixes. The mockups and the choice go into `brand/references/` and `brand/decisions.md`. Tokens v1 are then written from the chosen direction.

## References and decisions

Two kinds of entry in `brand/references/`:

- **A shared item**, numbered: `001-smart-home-dashboard/` holds the image and a `note.md` with where it came from, what to take and what to leave. For 001: take the tinted tiles, the hero number, the dark pill bar and the depth of the accents; leave the blue and lilac palette and the 3D cubes.
- **A source**, one line each in `sources.md`: the Muzli "top 25 app UI design inspiration" list, Dribbble popular mobile shots, Refero, Mobbin's latest iOS apps, with what each is good for and what to search there for Feno. A later link to a specific shot becomes a numbered item.

Whenever a reference changes a token or a component, `decisions.md` gets a dated line that points at it.

## Figma

One Figma file, "Feno brand", on Belinda's team (starter tier, full seat, admin). Pages: tokens, components, directions, screens. Code stays the master:

- `scripts/tokens.mjs` also writes the variable collections (light and dark modes) that the Figma connection loads into the file.
- Components are pushed from the `/brand` screen through the Figma connection, so the file shows the real thing.
- When Belinda edits in Figma, she says what changed and the token is changed in code. Nothing flows back automatically.

Whether the starter tier can publish a team library is checked before anything depends on it; if not, the file itself is the library.

## Fonts

Each direction proposes a type pairing. The winner is self-hosted:

- Font files in `public/fonts/` (woff2, the weights used, SIL Open Font License only, the licence file beside them), with `@font-face` in `tokens.css` and `font-display: swap`.
- The Google Fonts preconnects and stylesheet leave `index.html`.
- `vercel.json`: `fonts.googleapis.com` and `fonts.gstatic.com` leave `style-src`, `font-src` and `connect-src`. `vite.config.ts` reads the same policy for `vite preview`, and `e2e/security-headers.spec.ts` fails if a screen is refused a font.
- `vite.config.ts`: the Google Fonts runtime cache goes; the font files are precached with the app.
- The privacy policy stops naming Google Fonts, in both languages, with `POLICY_DATE` in `src/lib/contact.ts` and `CONSENT_VERSION` in `src/lib/consent.ts` raised. Policy v19 is written but unpublished; if it is still unpublished when the fonts ship, the change folds into v19, otherwise it is v20. `GO_LIVE` stays false, so nobody is asked to agree again.

One fewer third party, Feno fully offline, and first paint no longer waits on a font server.

## Rollout and timeline

The `/brand` screen stays behind `VITE_BRAND` for good. The re-skin changes the stylesheet growers already load, so it is not behind a switch: it deploys as one release on a Monday to Thursday morning before 1 December, with the policy update in the same release. Anything not ready by Thursday 26 November waits behind a switch until June.

| By | Done |
| --- | --- |
| Fri 14 Nov | `brand/` folder; references 001 and the four sources; tokens v1 generated into the app with the contrast test; three directions drawn; Belinda's choice recorded |
| Fri 21 Nov | `/brand` screen with every component restyled; fonts self-hosted; logo and wordmark explorations; Feno brand file in Figma with tokens and components |
| Thu 26 Nov | New look on the shell, Home, Log menu, forms and Timeline; policy updated; deployed |

Each row is its own pull request or small set of pull requests. CI stays green at every step: type check, unit tests, browser checks, database rules, build, workflow files.

## Tests that ship with it

- Unit: the token tests above (contrast pairs, no orphan tokens, generated CSS up to date), and the generator's own test.
- Browser: axe on `/brand` in both themes and languages; `prefers-reduced-motion` turns every named motion off; every tap target on `/brand` is at least 44 px; the security-headers check with the policy change.
- Not tested: the mockups and the Figma push. They are design artefacts, kept in `references/` and in the Figma file.

## Splitting out later

The day a second consumer exists, `brand/` becomes its own repository: `git mv` into a new repo keeping history, `tokens.json` published as a package or fetched at build time, `scripts/tokens.mjs` reads it from `node_modules`. `brand/README.md` records these steps so the move is a morning's work.

## Risks

| Risk | Answer |
| --- | --- |
| Three weeks is tight | The directions are decided in week one; the `/brand` screen is the gate for week two; week three applies only what the screen already shows. Anything short waits behind a switch |
| A tinted-card look fails contrast in dark mode | The contrast test fails CI before it deploys; the tints are tuned in the tokens, not in the CSS |
| Growers notice a changed app during the last picks of the old season | The deploy is before 1 December, on a weekday morning, with the usual hour's watch on Sentry, the sync bar and Amplitude |
| The Figma starter tier limits libraries | One file, few components; the file is the library if publishing is not allowed |
| Tokens and CSS drift | The orphan-token test and the stale-CSS test fail CI |
