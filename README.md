# sheilazhang.org

The front door for <https://sheilazhang.org/> — a short page that points at
everything I'm making, the way a Linktree does.

There is no build step, no framework and no dependencies: the repository root
*is* the site. Open `index.html` in a browser and you are looking at
production.

## The files

| File | What it is |
|---|---|
| `index.html` | the page, links and all |
| `assets/styles.css` | the theme tokens and the layout |
| `assets/favicon.svg` | the monogram, also the app icon |
| `assets/site.webmanifest` | name, colors and icon for browsers that install the page |
| `404.html` | sends a stray URL back to the front door |
| `CNAME` | the custom domain GitHub Pages serves this on |
| `.nojekyll` | stops Pages running Jekyll over the files |
| `.github/workflows/pages.yml` | uploads the root to Pages on every push to `main` |

## Adding a link

Links are plain HTML, so they are in the page itself and need no JavaScript to
appear. In `index.html`, find the `<ul class="links">` list, copy a whole `<li>`
block, and edit four things:

```html
<li>
  <a class="link" href="https://example.sheilazhang.org/">   <!-- 1. where it goes -->
    <span class="link-glyph" aria-hidden="true">
      <svg viewBox="0 0 24 24"><!-- 2. the icon: any stroked 24×24 path --></svg>
    </span>
    <span class="link-text">
      <span class="link-title">Example</span>                 <!-- 3. the name -->
      <span class="link-note">One line about it.</span>       <!-- 4. the subtitle -->
    </span>
    <span class="link-arrow" aria-hidden="true">
      <svg viewBox="0 0 24 24"><path d="M5 12h13M12.5 5.5L19 12l-6.5 6.5" /></svg>
    </span>
  </a>
</li>
```

Icons are inline SVG drawn with strokes, not fills — the stroke width, caps and
color all come from the stylesheet, so a bare `<path>`, `<circle>` or `<rect>` on
a `0 0 24 24` grid inherits the rest and matches the others. The `link-note` is
optional; drop that span for a link that needs no explanation.

## The theme

The tokens at the top of `assets/styles.css` are the "Calm Scholar" neutrals
with a blue accent, the same set
[`creating`](https://github.com/zhangqi444/creating) uses, so the two sites read
as one family. Light is the default on `:root` and dark is the `.dark` class,
which the small script in the `<head>` sets from the saved choice or the
operating system before the first paint — no flash of the wrong theme. The
button in the corner flips it and remembers.

## Deploying

Every push to `main` runs `.github/workflows/pages.yml`, which uploads the root
of the repository to GitHub Pages. Two things are needed once, on GitHub:

1. **Settings → Pages → Build and deployment → Source: GitHub Actions.** This
   one is done by hand and cannot be automated: the workflow asks for it
   (`configure-pages` with `enablement: true`), but the `GITHUB_TOKEN` an Action
   runs with is not allowed to create a Pages site, so the request comes back
   `Resource not accessible by integration` and the run fails there. Flip the
   switch once and every run after it passes.
2. **DNS for the apex domain.** `sheilazhang.org` needs four `A` records (and,
   for IPv6, four `AAAA` records) pointing at GitHub's Pages servers; the
   current addresses are in
   [GitHub's apex-domain documentation](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain).
   Once they resolve, tick **Enforce HTTPS** in Settings → Pages.

`www` is not configured here. To serve it too, add a `CNAME` record for `www`
pointing at `zhangqi444.github.io` and GitHub will redirect it to the apex.

## Working on it locally

Any static server will do, and none is strictly required:

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```
