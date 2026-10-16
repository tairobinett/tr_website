# tr_website

Personal site for Tai Robinett — a single static page with no build step and no
dependencies. Hosted on GitHub Pages for now; the files are plain HTML/CSS, so
moving to another host later means copying the directory.

## Files

| Path                         | What it is                                           |
| ---------------------------- | ---------------------------------------------------- |
| `index.html`                 | All page content and copy.                           |
| `styles.css`                 | All styling. Theme colors are CSS variables at the top. |
| `assets/headshot-square.jpg` | 800×800 crop of the headshot, used on the page.      |
| `assets/headshot.jpg`        | Original 3024×2710 photo, kept as the crop source. Safe to delete. |
| `assets/resume.pdf`          | Linked from the header.                              |
| `assets/shot-placeholder.svg`| Stand-in for project screenshots. Follows light/dark. |
| `assets/favicon.svg`         | Browser-tab icon.                                    |
| `.nojekyll`                  | Tells GitHub Pages to serve the files as-is, without running Jekyll. |

## Adding project screenshots

Every `<img>` in a `.shots` block currently points at
`assets/shot-placeholder.svg`, and its `alt` text describes the screenshot that
belongs in that slot. To fill one in:

1. Put the image in `assets/` (e.g. `assets/pandamaps-dungeon.png`).
2. Change that one `<img>`'s `src` to the new path.
3. Leave the `alt` text alone — it is already written for the real image.

Delete any `<figure class="shot">` you do not fill. The row is a three-column
grid on desktop and a swipeable strip on mobile; it works with one, two, or
three images.

Screenshots look best at a 16:10 ratio (they are cropped to that), around
1280×800. Keep them under ~300 KB each.

## Other edits

- **The PandaMaps demo link** is an `<a>` with no `href`, which renders as muted,
  non-clickable text rather than a dead link. When the deployment is live, add
  `href="https://..."` and change the text to "Live demo".
- **The availability badge** in the header is one `<p class="availability">`.
  Delete it once you are no longer job-seeking.
- **Accent color:** edit `--accent` and `--accent-sf` in `styles.css` — once in
  `:root` for light mode and once in the `prefers-color-scheme: dark` block.
- **The `og:image` meta tag** has an absolute URL pointing at the GitHub Pages
  domain. Update it if the site moves.

## Re-cropping the headshot

The square crop was made with Pillow: open `assets/headshot.jpg`, apply EXIF
rotation, take the largest centered square, resize to 800×800, and save as JPEG
at quality 85. Any image editor does the same job.

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
- **Another host:** upload `index.html`, `styles.css`, and `assets/`. Every path
  in the page is relative, so the site works from any directory without changes.
