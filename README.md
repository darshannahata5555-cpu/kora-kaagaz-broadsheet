# Kora Kaagaz — The Broadsheet

The Kora Kaagaz studio portfolio, set as a newspaper. It opens on a blank folded sheet (kora kaagaz) with an inked roller resting at its top edge. The roller is a 3D rubber drum with steel collars, brass rings and wooden handles; it rolls without slipping, catches the light and casts a soft shadow. As you scroll it prints the visible half of the page: masthead first, then the headline and the start of the article. The sheet then unfolds, its already printed lower half bending as it lifts off the fold, and the camera zooms in to read the front page top to bottom. Then the page turns and the inside pages stack like sheets of paper: Forms, Work, People, Editorial, Rough copy, Classifieds and the Back page.

The site is `index.html` (about 1.3 MB: fonts, scripts and the front page's own photos) plus `img/` (78 WebP portfolio images, about 4.7 MB). The images load only as you reach them, each with a tiny blurred preview holding its place until it arrives. Keep `index.html` and `img/` together. Everything is local except React, which loads from unpkg on first visit.

On a phone over 4G the first screen appears in about 1.9 seconds. The old single 8.6 MB file took about 7.5.

With reduced motion turned on, the front page appears already printed, with no roller and no fold.

On phones (narrower than 720px) the site is a calmer, leaner edition. Laptop and tablet widths are unchanged from v1.

- **Opening:** a compact front page (masthead, date line, headline, standfirst, one photo and the call to action) lies open and flat, and the roller prints it in one pass. There is no fold, zoom, pan or page turn, and the opening is less than half as long.
- **Forms, Websites and Decks:** swipeable card rows with shorter text.
- **Campaigns and Merch:** a few highlights each, with a "See all" button that opens the full gallery.
- **Trimmed on phones:** the project index, the featured project's numeral and metadata, all but the first paragraph of the editorial, the placeholder lines in Rough copy, and the Available and Terms boxes in Classifieds.
- **Navigation:** the Work section menu is one swipeable row.

## Versions

- `v1` (git tag): the print-run opening with the 3D roller printing only the visible half; real projects and People. Also saved as `Kora Kaagaz Broadsheet v1.html` on the Desktop.
- `main`: v1 plus the phone edition above. (Commit a4d5c12 holds an earlier phone attempt that kept the full sequence.)

## Open it

Double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
# then open http://127.0.0.1:8765/
```

To publish it, any static host works. On GitHub Pages: Settings → Pages → Deploy from a branch → `main` / root.

## What's on the Work page (P. 05)

- **Featured:** Ascent, the Techfest '26 identity for Scaler School of Technology (17-frame gallery)
- **Websites:** Ascent, [Splayed](https://splayed.ai/), [Symbiotes](https://symbiotes-pied.vercel.app/), GenC (four versions), [SuperMatrix](https://supermatrix.in/), [AcePro Advisors](https://darshannahata5555-cpu.github.io/acepro-website/)
- **Decks & brochures:** Yugaantar 2026 sponsorship deck, Node Zero Labs company deck, Lumora Solar brochure
- **Campaigns:** admissions, PromptWars, Ascent and Yugaantar posts and posters, Ascent venue entrance
- **Merch:** club jackets, tees and hoodies, notebooks, tote, keychain, Academic Clubs logo

Tap any image to open the full-screen viewer. Use ← → or swipe to browse, and Esc to close. Website cards open the live site in a new tab.

People (P. 06) shows the two people behind the studio, Ashmit Kumar Nayak and Darshan N, with their LinkedIn photos and details and links to their profiles. Still placeholder: the Film image on the Forms page (now stored locally as `img/form-film.webp`).

## How the file is built

`index.html` is a bundle exported from Claude Design. A short loader script unpacks two JSON blocks at load time:

- `<script type="__bundler/manifest">` maps each asset uuid to base64 data: fonts, the page runtime, React and the front page's three photos.
- `<script type="__bundler/template">` holds the page itself as a JSON string: markup with `{{ }}` bindings and a `Component` class with the data (`SITES`, `DECKS`, `CAMPAIGNS`, `MERCH`, `GALLERIES`, `WORK`) and the scroll and lightbox logic.

The loader swaps each uuid in the template for a blob URL. Portfolio images are not in the manifest. The template's `ASSETS` map points each one at `img/<name>.webp` and carries its size and a tiny preview (`lq`). To change content, decode the template JSON, edit it, and encode it back. To add an image, drop a WebP into `img/` and add an `ASSETS` entry for it.

A single-file version with every image embedded (about 7.6 MB, handy for sending as one file) is kept on the Desktop as `Kora Kaagaz Broadsheet.html`. It shows the same site but takes longer to open over a network.
