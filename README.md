# readyvim-site

The landing page for [ReadyVim](https://github.com/mohamadKrayem/readyvim) — my
personal Neovim + tmux setup. Served by GitHub Pages from `main`:

**https://mohamadkrayem.github.io/readyvim-site/**

## How it works

Plain HTML and CSS, plus [htmx](https://htmx.org) to swap sections in without a
page reload. There is no build step, no framework and no JavaScript of my own —
GitHub Pages serves the files exactly as they sit in this repo.

```
index.html    page shell: header, nav, footer
style.css     one stylesheet, colours taken from the tmux status line
partials/     one HTML fragment per section, fetched by htmx
.nojekyll     serve the files as-is, skip Jekyll processing
```

Each nav button is an `hx-get` pointing at a file in `partials/`. The first
button also carries `hx-trigger="click, load"`, so the intro is showing when the
page opens. Adding a section means writing a fragment and adding a button.

Since it's a static host, htmx is doing fragment loading rather than talking to
an API — which is all this page needs.

## Editing

Open `index.html` in a browser and it works, though a local server keeps the
paths honest:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000.
