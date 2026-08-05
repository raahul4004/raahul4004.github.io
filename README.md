# Portfolio — raahul4004.github.io

Static single-page site. No build step, no dependencies, no framework.
`index.html` is the whole thing: edit it directly.

```
index.html          the site (HTML + CSS + JS in one file)
assets/resume.pdf   linked from the header as "Résumé"
.nojekyll           stops GitHub Pages running Jekyll over the files
README.md           this file
PROFILE_README.md   NOT part of this site — see "Profile README" below
```

## Deploy to GitHub Pages

The repo must be named **`raahul4004.github.io`** exactly, or Pages serves it
from a subpath instead of the root domain.

1. Create a new **public** repo at github.com named `raahul4004.github.io`.
   Do not initialize it with a README.
2. From this folder:

```bash
git init
git add -A
git commit -m "Portfolio"
git branch -M main
git remote add origin https://github.com/raahul4004/raahul4004.github.io.git
git push -u origin main
```

3. In the repo: **Settings → Pages → Source = "Deploy from a branch"**,
   branch `main`, folder `/ (root)`, Save.

Live at https://raahul4004.github.io within a minute or two. Every later
`git push` redeploys automatically.

### If you'd rather not use the terminal

On the new repo's page choose **"uploading an existing file"**, drag in
`index.html`, `.nojekyll`, `README.md` and the `assets` folder, then commit and
do step 3 above. `.nojekyll` is a hidden file — enable hidden files in Finder
with `Cmd + Shift + .` so you can select it.

## Local preview

```bash
cd path/to/this/folder
python3 -m http.server 8000
# then open http://localhost:8000
```

Open it through the server rather than double-clicking the file, so the
relative link to `assets/resume.pdf` resolves the way it will in production.

## Updating the résumé

The header links `assets/resume.pdf`. To swap in a differently tailored
version, keep the filename so the link never breaks:

```bash
cp ~/Downloads/Resumes/resume_<target>.pdf assets/resume.pdf
```

## Adding a photo

There is no photo on the page right now. To add one, drop a square image at
`assets/portrait.jpg` (~800x800) and add this inside the `<header>` block,
after the `.meta` paragraph:

```html
<img class="portrait" src="assets/portrait.jpg" alt="Raahul Muthukrishnan"
     width="160" height="160">
```

...plus a rule in the `<style>` block:

```css
.portrait{width:160px; height:160px; border-radius:10px; object-fit:cover;
          border:1px solid var(--rule); margin-top:1.35rem}
```

## Things worth knowing before editing

- **Dark mode is a selected palette, not an inversion.** Both themes are
  declared as custom properties at the top of the `<style>` block, under three
  scopes: `:root` (light), a `prefers-color-scheme: dark` media query (OS
  setting), and `:root[data-theme="dark"]` (the toggle). Change a colour in all
  the scopes that apply, or the toggle and the OS setting will disagree.
- **The theme choice persists in `localStorage`.**
- **Every number on the page is measured.** If you change one, change it in the
  résumé too, and keep the metric name attached to it — average precision and
  accuracy are not interchangeable.
- **Do not hide results behind a click.** The tables were deliberately taken
  out of `<details>` wrappers: instrumented studies of explanatory pages found
  the median reader interacts with disclosure widgets zero times.
- **Section reveal animation:** most sections carry `class="rv"` and fade in on
  scroll. The About section deliberately does not, because on a short viewport
  it sits below the fold and would render as a blank gap on load.
- **Nothing loads from a CDN except Google Fonts** (Inter + JetBrains Mono).
  If you want the page fully self-contained, delete the three `<link>` tags in
  `<head>`; it falls back to system fonts and still looks correct.

## Profile README

`PROFILE_README.md` is **not** part of this site. GitHub only renders a profile
README from a repo named after your username:

1. Create a second public repo called `raahul4004` (initialized with a README).
2. Paste the contents of `PROFILE_README.md` into that repo's `README.md`.

It then renders on https://github.com/raahul4004.
