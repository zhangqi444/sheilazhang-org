# Working in this repository

## Branch

Work on `main`, commit to `main`, push to `main`. Do not open a side branch
for a change and do not open a pull request unless asked for one.

## What this is

The front door for <https://sheilazhang.org/> — a Linktree-shaped page of links
to everything being made. There is no build step, no framework and no
dependencies: the repository root *is* the published site, so `index.html` as it
sits on disk is exactly what a visitor gets.

Preview it with any static server — `python3 -m http.server 8000` — or just open
`index.html` in a browser.

## Where things live

- `index.html` — the page. The links are the `<li>` blocks inside
  `<ul class="links">`, written as plain HTML on purpose: they belong in the
  document for readers and crawlers with JavaScript off, so do not move them
  into a data file rendered at runtime.
- `assets/styles.css` — the theme tokens are at the top. They are the "Calm
  Scholar" neutrals with a blue accent, shared with
  [`creating`](https://github.com/zhangqi444/creating); keep the two in step so
  the sites read as one family. Light is `:root`, dark is the `.dark` class that
  the inline script in the `<head>` sets before first paint.
- `.github/workflows/pages.yml` — uploads the root to GitHub Pages on every push
  to `main`.

## Before pushing a change to the page

Load it in a browser at phone width and at desktop width, in both themes, and
check the console is clean. The whole site is one screen; looking at it is the
test suite.

## Pages

Deploys fail at `actions/configure-pages` until GitHub Pages is switched on by
hand under Settings → Pages → Source: GitHub Actions. `GITHUB_TOKEN` is not
allowed to create a Pages site, so no change to the workflow can fix a run that
fails there — it needs a human with repository settings access.
