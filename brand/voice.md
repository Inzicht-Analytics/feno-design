# Voice

Feno speaks the way a knowledgeable neighbour would at the farm gate: plainly, briefly, in the grower's own words, in both languages with the same care. The app's text lives in `src/lib/i18n.tsx`; every key has an English and an Afrikaans value and a unit test fails if either is missing or untranslated.

## The rules

1. **Plain words.** Spray, not application. Block, not orchard unit. Pick, not harvest event. If a grower would not say it at the gate, Feno does not say it on the screen.
2. **Short.** One idea per sentence. A hint is one sentence and ends with a full stop. A button is one or two words.
3. **Say what happens.** A button names the action: *Save*, *Log a pick*, *Read the report*. A confirmation says what was done: *Saved*, *Sent*. An error says what went wrong and what to do: *Check your signal and try again.*
4. **Never advise.** Feno reports and forecasts. It never says *spray now* or *apply 2 kg/ha*. The reminders on Home end with "They are not spray or fertiliser advice."
5. **No apology, no cheer.** No *Oops*, no *Awesome*, no exclamation marks. Calm in both directions.
6. **Dates and numbers one way.** `formatDay()` writes "4 Oct 2026" and "4 Okt 2026", never "04" or "Okt.". Numbers take the language's separators (`formatNumber()`). Units sit after the number with a space: 12.4 t, 6 mm, 24 °C.
7. **Afrikaans is not a translation.** It is written as a grower would say it, with the curly apostrophe in every *’n* (a unit test fails on a straight one). Labels run about 30 percent longer; a layout is tested in Afrikaans first.
8. **One word for one thing.** Edit, never Change or Modify. Block, never Orchard. Entry, never Record. The tidy-up of 6 November 2026 fixed these; keep them.

## The register, side by side

| English | Afrikaans |
| --- | --- |
| Good morning, Belinda. | Goeiemôre, Belinda. |
| Block A: last entry 44 days ago. Time for a stage check. | Blok A: laaste inskrywing 44 dae gelede. Tyd vir ’n stadiumkontrole. |
| Rain expected Wednesday, about 6 mm. Plan sprays and fertiliser around it. | Reën verwag Woensdag, sowat 6 mm. Beplan spuitings en bemesting daarom. |
| Saved. It will be sent when you have signal. | Gestoor. Dit word gestuur sodra jy sein het. |
| Something went wrong and nothing was saved. Check your signal and try again. | Iets het verkeerd geloop en niks is gestoor nie. Kyk na jou sein en probeer weer. |
| Put Feno on your home screen. It opens full screen like an app and is quicker to reach in the orchard. | Sit Feno op jou tuisskerm. Dit maak volskerm oop soos ’n toep en is vinniger om in die boord by te kom. |
| Who can see this: the people on your farm, and your exporter only for what you tick under Also share. | Wie dit kan sien: die mense op jou plaas, en jou uitvoerder net vir wat jy onder Deel ook merk. |
| Feno has no range for this yet. | Feno het nog nie ’n reeks hiervoor nie. |
| Your season, kept. | Jou seisoen, bewaar. |
| Delete this farm? Everything logged on it goes too. This cannot be undone. | Skrap hierdie plaas? Alles wat daarop aangeteken is, gaan saam. Dit kan nie ongedaan gemaak word nie. |

## Where the voice goes beyond the app

- **WhatsApp and email** (`messaging.md`): the same register, one message per thing, the farm named, never a figure a grower did not share.
- **The pilot welcome PDFs** (`print.md`): longer sentences are allowed, the words are the same.
- **Decks for exporters**: precise, with the numbers, still without advice.

## Checking it

- `src/lib/i18n.test.ts`: both languages complete, same placeholders, no untranslated text, short tab labels.
- `e2e/tidy-up.spec.ts`: one word for editing, one date style, every hint ends with a full stop.
- A new screen is read aloud once in each language before it ships. If a sentence sounds like software, rewrite it.
