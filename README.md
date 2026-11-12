# Wedding guest page

A one-page wedding invitation for guests: schedule, venues, dress codes, calendar invites, directions, photo album, WhatsApp sharing, a printable QR code, and an English / हिन्दी / বাংলা switch. It's a single static page with no build step and no server, hosted free on GitHub Pages.

**Live:** https://saumyakumar.github.io/wedding/

| File | What it is |
|---|---|
| `wedding.json` | **All the wedding details.** This is the file you edit. |
| `index.html` | The design and code. Same for every wedding. |
| `wedding.schema.json` | Describes every field, so editors like VS Code autocomplete and flag mistakes in `wedding.json`. |

---

## Editing the details (`wedding.json`)

### Text in three languages
Any text can be plain:
```json
"venue": "Beldih Golf Course"
```
or written in each language:
```json
"venue": { "en": "Beldih Golf Course", "hi": "बेलडीह गोल्फ़ कोर्स", "bn": "বেলডি গলফ কোর্স" }
```
If a language is missing, English is shown. The page's own wording (buttons, headings) is already translated inside `index.html`.

### Top-level fields
| Field | Example | Notes |
|---|---|---|
| `couple` | `[{ "en": "Sushmit", … }, { "en": "Manaswita", … }]` | Exactly two first names, in display order. The first gets the gold thread, the second the red thread. |
| `blessing` | `"॥ श्री गणेशाय नमः ॥"` | The line above the names. `""` hides it. |
| `hashtag` | `"#SushmitWedsManaswita"` | `""` hides it. |
| `city` | `{ "en": "Jamshedpur, Jharkhand", … }` | Shown under the dates. |
| `welcome` | `""` | Optional line under the arch. |
| `siteUrl` | `"https://saumyakumar.github.io/wedding/"` | **The live link.** Used for the QR code, sharing and calendar entries. |
| `photoAlbumUrl` | `"https://photos.app.goo.gl/…"` | Google Photos → Share → Create link. |
| `shareMessage` | `{ "en": "You're invited! … {url}", … }` | WhatsApp text. `{url}` becomes the page link. |
| `parents` | `[{ "label": …, "names": [ … ] }]` | The "With the blessings of" section. `[]` hides it. |
| `contacts` | `[{ "name": …, "role": …, "phone": "+91 91996 94008" }]` | Shows Call and WhatsApp buttons. Include the country code. |
| `events` | see below | The functions. |

### Each function in `events`
| Field | Example | Notes |
|---|---|---|
| `name` | `{ "en": "Haldi", "hi": "हल्दी", "bn": "গায়ে হলুদ" }` | The English name also picks the card's drawing (haldi, mehendi, sangeet, wedding, reception). Use `motif` to force one. |
| `date` | `"2027-02-16"` | `YYYY-MM-DD`, India time. Cards sort by date automatically. |
| `start` | `"19:00"` | 24-hour time. |
| `end` | `"23:00"` | **Optional.** Leave it out to show "7:00 PM onwards". Calendar entries then last 4 hours. `"00:30"` means after midnight. |
| `venue`, `address` | | Shown on the card and in calendar entries. |
| `mapsUrl` | `"https://www.google.com/maps/search/?api=1&query=22.8091068%2C86.1737869"` | The Directions button. Coordinates are the most exact. |
| `dressCode`, `note` | | Optional. A missing one is simply not shown. |
| `accent` | `"#A51C30"` | The card's colour. |
| `palette` | `["#A51C30", "#E07B39"]` | Colour dots next to the dress code. `[]` hides them. |

The function named Wedding (or Vivah / Shaadi / Phera) is where the gathbandhan threads tie their knot.

---

## Making a page for another couple

1. On GitHub, open this repo and click **Use this template → Create a new repository**. Make it public: GitHub Pages is free for public repos.
2. Replace the details in `wedding.json`. Your editor will underline anything that doesn't match the format.
3. In `index.html`, edit the 4 lines marked **`EDIT FOR EACH WEDDING`** (`<title>`, description and `og:` tags). WhatsApp link previews read these lines directly and don't see `wedding.json`.
4. In the new repo: **Settings → Pages → Deploy from a branch → `main` / root**.
5. Put the new link (e.g. `https://<user>.github.io/<repo>/`) in `siteUrl`, so the QR code points to the right place.

---

## Previewing on your computer

Browsers don't let a page opened straight from disk read `wedding.json`, so start a tiny local server in this folder:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/.

**Handy test links:**
- `?lang=hi` or `?lang=bn` opens the page in Hindi or Bengali. These are good links to send each family.
- `?preview-now=2027-02-16T14:00` shows the page as it would look at that moment (India time): finished functions greyed out, the next one highlighted.

If `wedding.json` has a typo, the page shows "Couldn't load the wedding details", and the browser console (F12) gives the exact line and column.
