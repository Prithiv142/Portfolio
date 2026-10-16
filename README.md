# Portfolio

A single-page, animated frontend portfolio: plain HTML, CSS and JavaScript. No framework, no build step, no dependencies. Fonts load from Google Fonts, so the first view needs an internet connection.

```
portfolio/
├── index.html                  the whole site (content, styles, script)
├── Prithiv_Raj_Resume.pdf      linked from the "Download resume" button
└── README.md
```

## Preview locally

```bash
cd portfolio
python -m http.server 8000      # then open http://localhost:8000
```

(`npx serve` works too. Double-clicking `index.html` also works.)

## Publish it

All of these are free for a personal site and deploy straight from a Git repository.

| Option | Best for | Notes |
|---|---|---|
| **GitHub Pages** (recommended) | Simplest path; code and hosting in one place | URL: `https://<username>.github.io/<repo>/` |
| **Cloudflare Pages** | Fast global CDN, easy custom domain | Connect the repo, leave the build command empty, output directory `/` |
| **Netlify** | Drag-and-drop or Git deploys, preview URL per branch | Same settings as Cloudflare |
| **Azure Static Web Apps** | If you want it inside your Azure/Microsoft ecosystem | Free tier; deploys via GitHub Actions |

### GitHub Pages, step by step

1. Create a new **public** repository on GitHub (for example `portfolio`, or `<username>.github.io` for a root URL).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial portfolio"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
3. In the repo go to **Settings > Pages**, set **Source** to *Deploy from a branch*, branch `main`, folder `/ (root)`, then Save.
4. After a minute the site is live at the URL shown on that page.

### Custom domain (optional)

Buy a domain, then in **Settings > Pages > Custom domain** enter it and follow the DNS instructions (a `CNAME` record for `www`, `A` records for the root). Tick **Enforce HTTPS**.

## Maintain it

- **Edit content:** change the text directly in `index.html`. Sections are marked by `id`: `top` (hero), `about`, `experience` (tabs), `work` (cards), `lab` (controlled vs uncontrolled demo), `problems` (flip cards), `skills`, `contact`.
- **Hero name:** edit the two `data-line` spans at the top of `<main>`. The letters are split by JavaScript.
- **Rotating words in the hero:** edit the `<span>` items inside `#rotator`.
- **Counters:** change `data-count` (and `data-dec` for decimals) in the About stats.
- **Tech marquee:** edit the `<li>` items in both lists (the second list is the looping copy).
- **Add an experience tab:** add a `button.tab` and a matching `div.panel` (same pattern as the others, `aria-controls` and `aria-labelledby` ids must match).
- **Colours, fonts and themes:** edit the variables at the top of the `<style>` block. Dark is the default, `:root[data-theme="light"]` holds the light theme, and the three accent colours are the `data-accent` rules.
- **Animation speed or intensity:** the hero is in the `drawFrame` function (dot size, pointer radius `R`, letter weights). The marquee speed is the `38s` in `.track`.
- **Reduced motion:** visitors who set "reduce motion" in their OS get a static version automatically.
- **Change colours and fonts:** edit the variables at the top of the `<style>` block (`:root`). Dark mode values are in the `prefers-color-scheme: dark` block right below.
- **Add LinkedIn / GitHub links:** uncomment the example line in the contact area of the left panel and put in your real URLs.
- **Update the resume:** replace `Prithiv_Raj_Resume.pdf` with the new file, keeping the same name.
- **Add a project:** copy one `.tilt-wrap` block inside the `#work` section and edit it (delete the `.viz` block if you do not want a mini visual).
- **Deploy a change:**
  ```bash
  git add .
  git commit -m "Update projects"
  git push
  ```
  GitHub Pages redeploys automatically within a minute or two.
- **Work safely:** make changes on a branch (`git checkout -b update-skills`), open a pull request, and merge when it looks right. Cloudflare Pages and Netlify give each branch its own preview link.

## Before you publish

- Re-read every line as a public reader would. Confirm with your employer that the project descriptions (Bulk Workflow, License Manager, logging) are fine to share publicly.
- Your phone number is deliberately left out. The email address is public once the site is live.
- Test the page on your phone and check that the resume button downloads the PDF.
- The bulk workflow, license and logging visuals use sample numbers and are labelled as illustrations. Keep them labelled that way.
