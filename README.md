# Ayush — portfolio (Vue 3)

A warm, light, editorial portfolio starter built with **Vue 3 + Vite**. The experience is deliberately phone-first: one-screen-inspired sections, a touch-friendly orbital project selector, original local SVG project artwork, accessible navigation, subtle transitions, and a reduced-motion fallback.

> **Before publishing:** review every project description and add real repository/demo links. The illustration files are original interface concepts, not screenshots of finished products. Blank project links intentionally fall back to your GitHub profile so the page never links to a made-up repository.

## What is included

- Vue components split by responsibility (`SiteHeader`, `HeroSection`, `ProjectWork`, `ProjectDial`, `ProjectArtwork`, `AboutSection`, `ContactSection`, and section navigation).
- Five original, local SVG artwork pieces, plus a custom favicon, social preview card, and web manifest.
- Separate design-token, global, layout, component, and responsive stylesheets.
- Mobile navigation, section-aware navigation state, keyboard focus styles, skip link, touch swiping, click/tap dial controls, and `prefers-reduced-motion` support.
- Vercel-friendly Vite configuration, metadata, `robots.txt`, clean URL settings, and a GitHub Actions build check for pushes and pull requests.

## 1. Edit your personal details

Open `src/data/portfolio.js` and update:

- `name`, `role`, `locationLabel`, and `intro`
- `githubUrl` (currently set to `https://github.com/byhayush`)
- `email` (optional; leave blank to use GitHub for the contact action)
- `about`, `currently`, and `toolkit`

Then open `src/data/projects.js`. For each project, replace `href: ''` with its **actual** public repository or live demo URL. Update project names, summaries, technologies, and status labels to match the real work. The art assets live in `public/projects/` and can be replaced without changing the Vue components as long as the filenames remain the same.

## 2. Add this ZIP to an existing GitHub repository

Upload `ayush-portfolio-vue-pro.zip` to the **root** of your repository in the GitHub web UI, then open that repository in Codespaces. Run this single command in the Codespaces terminal:

```bash
unzip -o ayush-portfolio-vue-pro.zip -d . && rm ayush-portfolio-vue-pro.zip
```

This extracts the archive into the repository root and removes the ZIP **only when extraction succeeds**. `-o` overwrites matching files, so do not use it blindly if the repository already contains files you need to keep. This archive has no outer project folder: `package.json`, `index.html`, `src/`, and `public/` land directly in the root.

If `unzip` is missing, use `python -m zipfile -e ayush-portfolio-vue-pro.zip .` and then remove the archive with `rm ayush-portfolio-vue-pro.zip` after confirming extraction.

## 3. Install and run in Codespaces

```bash
npm install
npm run dev
```

Codespaces normally offers to open a forwarded preview for the Vite port. Stop the server with `Ctrl+C`.

## 4. Check the production build

```bash
npm run build
```

Vite writes the production site to `dist/`. Preview that output locally with:

```bash
npm run preview
```

If a build command fails, resolve the displayed error before deploying. Check the **Problems** panel and the terminal output rather than relying only on the dev preview.

## 5. Push the extracted project to GitHub

```bash
git add -A && git commit -m "Build Ayush portfolio" && git push
```

If Git says there is nothing to commit, confirm the ZIP was extracted at the repository root and check `git status`.

## 6. Publish on Vercel

1. Sign in at [vercel.com](https://vercel.com/) and choose **Add New → Project**.
2. Import the GitHub repository that now contains `package.json` at its root.
3. Use these settings (Vercel generally detects Vite automatically):
   - **Framework preset:** Vite
   - **Build command:** `npm run build`
   - **Output directory:** `dist`
   - **Install command:** `npm install`
4. Click **Deploy**. Open the deployment URL after the build reports success.
5. For later updates, commit and push changes to the connected production branch; Vercel will build a new deployment.

No environment variables are required for this starter.

## Design / implementation notes

- Palette: warm off-white, charcoal, soft sage/lime, muted lilac and beige. Bright accents are used sparingly.
- Section snapping uses CSS `proximity`, not mandatory full-page snapping, so small screens can still scroll naturally when content is taller than the viewport.
- The project dial works with buttons, arrows, pagination dots and horizontal swipes. Keyboard users can tab through project nodes.
- Animations are CSS-based and respect `prefers-reduced-motion`.
- Google Fonts are loaded remotely with system fallbacks, so the site remains readable when offline; the custom local SVG artwork is bundled.
- The portfolio does not include analytics, tracking scripts, or a third-party component library.

## Project structure

```text
.
├── index.html
├── package.json
├── vite.config.js
├── vercel.json
├── public/
│   ├── favicon.svg
│   ├── og-card.svg
│   ├── robots.txt
│   ├── site.webmanifest
│   └── projects/
│       ├── aurix.svg
│       ├── media-lab.svg
│       ├── interface-lab.svg
│       ├── tiny-tools.svg
│       └── next-thing.svg
└── src/
    ├── App.vue
    ├── main.js
    ├── components/
    ├── composables/
    ├── data/
    └── styles/
```

## Before you share the link

- Add actual project links and verify the GitHub profile URL.
- If you want email contact, set `email` in `src/data/portfolio.js`.
- Replace the social preview domain with your deployed domain in `index.html` if desired.
- Run `npm run build`, open the Vercel URL on a phone, test the project dial and nav, and confirm every link goes where expected.
