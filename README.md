# Party for Your Mind

Two interactive pages for the U-M Digital Accessibility table at **Party
for Your Mind**, the undergraduate welcome event at Shapiro Library.

| Page | What visitors do |
| --- | --- |
| [`index-how-to-read.html`](index-how-to-read.html) | Tap the format they read in. A live donut chart fills in with everyone's answers. |
| [`index-try-tools.html`](index-try-tools.html) | Try Panorama alternate formats, zoom and spacing, read aloud, and contrast. |
| [`index.html`](index.html) | Landing page linking to both. |

Everything runs in the browser. There is no build step, no server code,
and no network request &mdash; each page is a single self-contained HTML
file next to `digital-accessibility-logo.png`.

## Running it at the table

Open either HTML file directly in a browser (double-click, or
File &rarr; Open). Keep the `.html` files and the logo in the same
folder. Chrome, Edge, Firefox, and Safari all work.

One laptop per page works well: one running **How do you read?**, one
running **Try our tools!**

### Clearing the tally

Responses on **How do you read?** are kept in that browser's local
storage, so they survive a refresh and stay on the machine. The reset
control is deliberately not on screen, so a visitor cannot wipe the
board by accident.

To clear it, load the page with `?reset` on the end of the address:

```
index-how-to-read.html?reset
```

That zeroes the counts, then reveals a **Reset responses** button for
the rest of the session, so staff can clear it again without retyping
the address. The parameter is dropped from the address bar afterwards,
so a refresh will not wipe the board a second time.

Responses are per browser profile. Two laptops keep two separate
tallies, and a private window starts from zero.

### Try our tools

Every setting resets when a visitor leaves a tool &mdash; whether they
use the **All tools** button, the browser back button, or a trackpad
back-swipe. Contrast, zoom, spacing, and any generated format all
return to their defaults, so the next person starts from a clean page.

Read aloud uses the browser's own speech synthesis. It needs no setup,
but the available voices depend on the machine, so it is worth trying
once on the laptop you plan to bring.

## Hosting on GitHub Pages

The repository is already laid out for it &mdash; static files at the
root, with `index.html` as the entry point.

1. Push this repository to GitHub.
2. **Settings &rarr; Pages**.
3. Under **Source**, choose **Deploy from a branch**.
4. Pick branch `main` and folder `/ (root)`, then **Save**.

After a minute the site is at
`https://<user>.github.io/<repository>/`, with the two pages at
`/index-how-to-read.html` and `/index-try-tools.html`.

Hosting is optional. The pages behave the same opened from a local
folder, which is worth relying on if the venue's wifi is unreliable.

## Notes on the Panorama page

The Panorama view is a simulation, not the real product. It mirrors
what a student sees in Canvas: the blue accessibility icon beside a
file, and an **Alternative Formats** menu using YuJa's own format names
and descriptions.

Three formats are wired up and generate real output in the browser:

- **Text File** &mdash; the reading as plain text, with a `.txt` download.
- **PDF** &mdash; a page preview at true US Letter proportions, with a
  real `.pdf` download built on the fly.
- **Gradient Reader** &mdash; the reading recolored line by line, the way
  YuJa's Gradient Reader carries the eye from one line to the next.

Panorama offers more formats in Canvas (EPUB, Braille, Audio Podcast,
Immersive Reader, translations). Those are named in a footnote under the
menu rather than shown as options, so nobody clicks something that
cannot do anything.

References:
[Panorama for Students](https://accessibility.umich.edu/contact-services/canvas-accessibility/panorama-students),
[YuJa on gradient text](https://www.yuja.com/blog/gradient-text-makes-content-accessible/).

## Accessibility

The pages are the demo, so they hold themselves to the same standard:

- Every control is reachable and operable by keyboard, with a visible
  focus ring.
- Tool cards are one focusable control each &mdash; the whole card is the
  target, and its accessible name is the card title.
- Chart data is also available as text through the chart description and
  a live region, so it is not conveyed by color alone.
- Colors meet WCAG AA against their backgrounds. The Gradient Reader
  palette is checked at 7:1 or better on white.
- `prefers-reduced-motion` and `forced-colors` are both honored.
