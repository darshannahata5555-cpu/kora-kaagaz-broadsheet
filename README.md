# Kora Kaagaz — The Broadsheet

The Kora Kaagaz studio portfolio, set as a newspaper. It opens on a blank folded sheet (kora kaagaz) with an inked roller resting at its top edge. The roller is a 3D rubber drum with steel collars, brass rings and wooden handles; it rolls without slipping, catches the light and casts a soft shadow. As you scroll it prints the visible half of the page: masthead first, then the headline and the start of the article. The sheet then unfolds, its already printed lower half bending as it lifts off the fold, and the camera zooms in to read the front page top to bottom. Then the page turns and the inside pages stack like sheets of paper: Forms, Work, People, Editorial, Rough copy, Classifieds and the Back page.

Everything is in one self-contained file, `index.html` (about 8.6 MB). All the images and fonts are embedded in it. React loads from unpkg and the Film photo loads from korakaagaz.co, so it needs an internet connection.

With reduced motion turned on, the front page appears already printed, with no roller and no fold.

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

People (P. 06) shows the two people behind the studio, Ashmit Kumar Nayak and Darshan N, with their LinkedIn photos and details and links to their profiles. Still placeholder: the Film image on the Forms page.

## How the file is built

`index.html` is a bundle exported from Claude Design. A short loader script unpacks two JSON blocks at load time:

- `<script type="__bundler/manifest">` maps each asset uuid to base64 data: fonts, the page runtime, React and the WebP portfolio images.
- `<script type="__bundler/template">` holds the page itself as a JSON string: markup with `{{ }}` bindings and a `Component` class with the data (`SITES`, `DECKS`, `CAMPAIGNS`, `MERCH`, `GALLERIES`, `WORK`) and the scroll and lightbox logic.

The loader swaps each uuid in the template for a blob URL. To change content, decode the template JSON, edit it, and encode it back. To add an image, add a manifest entry (mime `image/webp`, base64 data) under a new uuid and reference that uuid from the template.
