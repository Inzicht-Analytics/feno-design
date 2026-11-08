# Motion

Motion is feedback, never decoration. Four named motions, built on three durations and two easings from `tokens.json`, all off under *reduce motion*. Each has a *Play* button on `/brand`.

## Tokens

| Token | Value | For |
| --- | --- | --- |
| `--dur-fast` | 120 ms | A screen's first paint |
| `--dur-base` | 200 ms | A confirmation |
| `--dur-slow` | 320 ms | Something arriving; the sync pulse runs at three times this |
| `--ease-out` | cubic-bezier(0.2, 0, 0, 1) | Things that arrive or settle |
| `--ease-in-out` | cubic-bezier(0.4, 0, 0.2, 1) | Things that breathe |

## The four motions

| Class | What it does | Where |
| --- | --- | --- |
| `.motion-saved` | Scales from 96 percent and settles, 200 ms | A notice that something was saved or sent |
| `.motion-sync` | The icon fades to 55 percent and back, on a loop | The sync bar while entries go out; the words keep their contrast |
| `.motion-stage` | Rises 8 px and fades in, 320 ms | A stage reached on Home or the Timeline |
| `.motion-enter` | Rises 4 px and fades in, 120 ms | A screen's first paint |

## Rules

- Nothing moves unless the grower did something or something arrived.
- No loops except the sync pulse, and that only while sending.
- `@media (prefers-reduced-motion: reduce)` sets every animation and transition to 0.01 ms (`src/styles.css` → Motion); `e2e/brand.spec.ts` proves every named motion stops.
- Transitions on hover are for laptops only and never longer than `--dur-base`.
- Keys stay stable so lists do not remount and flicker: Home's prompts carry `promptKey()` (`src/lib/suggestions.ts`), not their index.

## Adding a motion

Name it by what it means (`.motion-<what happened>`), build it on the tokens, add it to `Motions.tsx` on `/brand`, and the reduced-motion check covers it. If it needs a new duration, it goes into `tokens.json` first.
