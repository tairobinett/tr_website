# tr_website

Personal site for Tai Robinett — a single static page with no build step and no
dependencies. Hosted on GitHub Pages for now; the files are plain HTML/CSS, so
moving to another host later means copying the directory.

## Files

| Path                  | What it is                                            |
| --------------------- | ----------------------------------------------------- |
| `index.html`          | All page content. Four `EDIT ME` blocks mark what to fill in. |
| `styles.css`          | All styling. Theme colors are CSS variables at the top. |
| `assets/profile.svg`  | Placeholder portrait — replace with your photo.       |
| `assets/favicon.svg`  | Browser-tab icon.                                     |
| `.nojekyll`           | Tells GitHub Pages to serve the files as-is, without running Jekyll. |

## Editing

Everything personal lives in `index.html`, inside four commented blocks:

1. **Metadata** — title and description used by browsers and search engines.
2. **Header** — photo, name, headline, bio, and the GitHub / LinkedIn / email links.
3. **Projects** — one `<li class="project">` per project; copy the block to add more.
4. **Experience** — optional; delete the whole `<section>` to drop it.

To use your own photo, add it to `assets/` (square, 400×400 or larger) and point
the `<img class="avatar">` `src` at it, e.g. `assets/profile.jpg`. Update the
`alt` text too.

To change the accent color, edit `--accent` and `--accent-sf` in `styles.css` —
once in `:root` for light mode and once in the `prefers-color-scheme: dark` block.

## Previewing locally

Open `index.html` in a browser, or serve it so paths behave exactly as they will
in production:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying to GitHub Pages

1. Push `main`.
2. On GitHub: **Settings → Pages → Build and deployment**.
3. Source: **Deploy from a branch**. Branch: `main`, folder: `/ (root)`. Save.
4. After a minute the site is live at <https://tairobinett.github.io/tr_website/>.

Every later push to `main` redeploys automatically.

## Moving to a custom domain or another host

- **Custom domain, still on Pages:** add a `CNAME` file containing the bare
  domain (e.g. `example.com`), point DNS at GitHub, then set the domain under
  Settings → Pages and enable *Enforce HTTPS*.
- **Another host:** upload `index.html`, `styles.css`, and `assets/`. All paths
  are relative, so the site works from any directory without changes.
