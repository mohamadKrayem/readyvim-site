# readyvim-site

The landing page for [ReadyVim](https://github.com/mohamadKrayem/readyvim) — my
personal Neovim + tmux setup. Served by GitHub Pages from `main`:

**https://mohamadkrayem.github.io/readyvim-site/**

## How it works

Plain HTML and CSS, plus [htmx](https://htmx.org) to swap sections in without a
page reload. There is no build step, no framework and no JavaScript of my own —
GitHub Pages serves the files exactly as they sit in this repo.

```
index.html      page shell + the intro, written inline
style.css       one stylesheet, colours taken from the tmux status line
partials/       one HTML fragment per section, fetched by htmx
og-image.png    1200x630 link preview, rendered from assets/og-card.html
assets/         source for the preview image
favicon.svg
robots.txt
sitemap.xml
.nojekyll       serve the files as-is, skip Jekyll processing
```

Each nav button is an `hx-get` pointing at a file in `partials/`. Adding a
section means writing a fragment and adding a button.

The intro is the exception: it lives directly in `index.html` rather than in a
fragment, and the Intro nav item is a plain link home. Link-preview bots
(Slack, WhatsApp, Telegram, LinkedIn, iMessage) and non-JavaScript crawlers
never run htmx, so anything they need to see has to be in the HTML they get —
otherwise a shared link previews as an empty page.

Since it's a static host, htmx is doing fragment loading rather than talking to
an API — which is all this page needs.

## Regenerating the preview image

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --window-size=1200,630 \
  --screenshot=og-image.png assets/og-card.html
```

## Editing

Open `index.html` in a browser and it works, though a local server keeps the
paths honest:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000.
