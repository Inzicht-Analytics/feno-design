# Messages

What Feno sends outside the app: sign-in codes and invitations by email or WhatsApp, push notifications, and the messages Belinda writes to growers and exporters by hand. All in the voice (`voice.md`), in the person's language.

## Sign-in codes and invitations

Sent by Supabase's email templates and, when switched on, by Twilio Verify on WhatsApp (`docs/whatsapp-setup.md`). The rules:

- Subject or first line says what it is: *Your Feno sign-in code*, *You are invited to Kleinplaas on Feno*.
- The code on its own line, large, nothing else on that line. The email carries the code and a link; the code is what people use in the orchard.
- Who it is from: *Feno*, then Belinda's name in the signature, with the WhatsApp number and email in `src/lib/contact.ts`.
- Never a figure, a block name or anything from the diary in a message. An invitation names the farm and the role, nothing more.
- Afrikaans or English by the person's preferred language; a new person gets the language they were invited in.

## Push notifications (`docs/push-setup.md`)

- One line, the farm and block named, the kind of entry, who logged it: *Kleinplaas · Block A: a spray was logged by Piet.* Never the figures or the notes; the phone maker's push service sees the notification (the privacy policy says so).
- Grouped by farm, so a busy morning is one notification, not ten.
- The app icon is the mark; the badge count is the number of new entries since the person last opened Feno.

## Messages Belinda writes

- **To a grower**: short, by WhatsApp, in their language, about their farm only. Opening a conversation with what changed in Feno and what it means for them. Never asking for figures over WhatsApp; the figures belong in the diary.
- **To an exporter's staff**: by email, precise, with the farm names they are allowed to see and nothing from any other farm. Decks follow `print.md`.
- **Release notes**: one message per release that a grower would notice, three lines at most: what is new, what to do, who to ask. Nothing for a release they would not notice.

## Signature

```
Belinda Kennedy · Feno
WhatsApp and email, the contact shown under Help in the app
```

(The values come from `src/lib/contact.ts`; change them there.)

## What never goes in a message

- A grower's figures, notes, lab results, locations or photos.
- A promise about fees, a date for a feature, or spray advice.
- Another grower's name.
