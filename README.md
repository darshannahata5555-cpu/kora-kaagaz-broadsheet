# Kora Kaagaz — The Broadsheet

The Kora Kaagaz studio portfolio, set as a newspaper. The front page folds open as you scroll, then the inside pages stack like sheets of paper: Forms, Work, People, Editorial, Rough copy, Classifieds and the Back page.

Everything is in one self-contained file, `index.html` (about 8.5 MB). All the images and fonts are embedded in it. React loads from unpkg and the Film and People photos load from korakaagaz.co, so it needs an internet connection.

## Open it

Double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
# then open http://127.0.0.1:8765/
```

To publish it, any static host works. On GitHub Pages: Settings → Pages → Deploy from a branch → `main` / root.

## What's on the Work page (P. 05)

- **Featured:** Ascent, the Techfest '26 identity for Scaler School of Technology (19-frame gallery)
- **Websites:** Ascent, [Splayed](https://splayed.ai/), [Symbiotes](https://symbiotes-pied.vercel.app/), GenC (four versions), [SuperMatrix](https://supermatrix.in/), [AcePro Advisors](https://darshannahata5555-cpu.github.io/acepro-website/)
- **Decks & brochures:** Yugaantar 2026 sponsorship deck, Node Zero Labs company deck, Lumora Solar brochure
- **Campaigns:** admissions, PromptWars, Ascent and Yugaantar posts and posters, Ascent venue entrance
- **Merch:** club jackets, tees and hoodies, notebooks, tote, keychain, Academic Clubs logo

Tap any image to open the full-screen viewer. Use ← → or swipe to browse, and Esc to close. Website cards open the live site in a new tab.

People (P. 06) shows the two people behind the studio, Ashmit and Darshan, with links to their LinkedIn profiles. Still placeholder: the Film image on the Forms page.

## How the file is built

`index.html` is a bundle exported from Claude Design. A short loader script unpacks two JSON blocks at load time:

- `<script type="__bundler/manifest">` maps each asset uuid to base64 data: fonts, the page runtime, React and the WebP portfolio images.
- `<script type="__bundler/template">` holds the page itself as a JSON string: markup with `{{ }}` bindings and a `Component` class with the data (`SITES`, `DECKS`, `CAMPAIGNS`, `MERCH`, `GALLERIES`, `WORK`) and the scroll and lightbox logic.

The loader swaps each uuid in the template for a blob URL. To change content, decode the template JSON, edit it, and encode it back. To add an image, add a manifest entry (mime `image/webp`, base64 data) under a new uuid and reference that uuid from the template.
