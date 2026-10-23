# Ayush Portfolio — Update v1

A light, minimalist, mobile-first portfolio built with Vue 3 and Vite. This update follows the supplied visual reference: warm off-white surfaces, confident typography, a quieter hero, and a large project showcase with a rotating circular orbit rather than the previous project dial.

## What's changed in Update v1

### Updated
- `src/components/ProjectWork.vue` — rebuilt the project area as a large orbital/swirl showcase. Select any project around the circle; use the previous/next buttons, horizontal swipe on mobile, or keyboard arrow keys.
- `src/components/ProjectArtwork.vue` — removed small labels and decorative chrome so the artwork reads clearly.
- `src/components/HeroSection.vue` — removed the extra scroll cue, section counter and secondary tagline from the hero footer to reduce clutter.
- `src/data/projects.js` — now contains seven showcase entries with concise copy. Only Aurix is described as a personal project; the other six are clearly labelled fictional concept studies.
- `src/main.js` — loads the new dedicated orbit stylesheet.
- `package.json` — renamed package to `ayush-portfolio-update-v1`, version `1.0.0`.
- `README.md` — update/deletion list, install/build instructions and repo structure refreshed.

### Added
- `src/styles/project-swirl.css` — circular project motion, selected state, responsive styling, transitions, and reduced-motion support.
- `public/projects/relay.svg` — original local concept artwork for Relay.
- `public/projects/form-field.svg` — original local concept artwork for Form & Field.

### Removed
- `src/components/ProjectDial.vue` — the old compact dial interface is no longer used. The new orbit selector lives inside `ProjectWork.vue`.
- Old dial controls and excess micro-labels inside the project showcase.

### Important honesty note
The six entries marked **CONCEPT STUDY** are fictional design concepts made to show the visual direction, not claims that finished apps exist. Replace descriptions/status/links with real work before presenting the site as a factual portfolio. Project links are blank and fall back to your configured GitHub profile rather than inventing repositories.

## 1. Personal details

Edit `src/data/portfolio.js`:
- `name`, `role`, `locationLabel`, `intro`
- `githubUrl` (currently `https://github.com/byhayush` — confirm this is your intended profile)
- `email`, `about`, `currently`, and `toolkit`

Edit `src/data/projects.js` to update project names, descriptions, tags, statuses, and real repository/demo URLs. The SVG files are in `public/projects/`.

## 2. Put this update into an existing GitHub repository

Upload `ayush-portfolio-update-v1.zip` to the **root** of the same repository, open its Codespace, and run this one command in the terminal:

```bash
unzip -o ayush-portfolio-update-v1.zip -d . && rm -f src/components/ProjectDial.vue && rm ayush-portfolio-update-v1.zip
```

This archive has no outer folder. `package.json`, `index.html`, `src/`, and `public/` are extracted directly into the repository root. Existing matching files are overwritten. The command also removes the obsolete dial component from the previous version and deletes the ZIP only if extraction succeeds. Commit or back up any unrelated local changes first.

## 3. Run in Codespaces

```bash
npm install && npm run dev
```

Open the forwarded Vite port when Codespaces offers it. Stop the server with `Ctrl+C`.

## 4. Verify production build

```bash
npm run build
```

Vite writes the production site to `dist/`. Do not deploy until this command succeeds. The development environment used to prepare this ZIP had a package-install timeout, so the production build has not been represented as pre-verified here.

## 5. Commit and push

```bash
git add -A && git commit -m "Update portfolio to orbital projects layout" && git push
```

If Git reports nothing to commit, inspect `git status` and confirm extraction happened at the repository root.

## 6. Deploy on Vercel

1. Open [Vercel](https://vercel.com/) and choose **Add New → Project**.
2. Import the GitHub repository.
3. Use **Vite** as the framework preset, `npm run build` as the build command, and `dist` as the output directory. Install command: `npm install`.
4. Deploy. The Vercel deployment URL appears after the build succeeds.

No environment variables are required.

## Repo structure

```text
.
├── .github/
│   └── workflows/
│       └── verify.yml
├── public/
│   ├── favicon.svg
│   ├── og-card.svg
│   ├── robots.txt
│   ├── site.webmanifest
│   └── projects/
│       ├── aurix.svg
│       ├── form-field.svg        # added in Update v1
│       ├── interface-lab.svg
│       ├── media-lab.svg
│       ├── next-thing.svg
│       ├── relay.svg             # added in Update v1
│       └── tiny-tools.svg
├── src/
│   ├── App.vue
│   ├── main.js                   # updated
│   ├── components/
│   │   ├── AboutSection.vue
│   │   ├── ContactSection.vue
│   │   ├── HeroSection.vue       # simplified
│   │   ├── HeroVisual.vue
│   │   ├── ProjectArtwork.vue    # simplified
│   │   ├── ProjectWork.vue       # rebuilt orbital showcase
│   │   ├── SectionDots.vue
│   │   └── SiteHeader.vue
│   ├── data/
│   │   ├── portfolio.js
│   │   └── projects.js           # expanded to seven entries
│   └── styles/
│       ├── components.css
│       ├── global.css
│       ├── layout.css
│       ├── project-swirl.css     # added in Update v1
│       ├── responsive.css
│       └── tokens.css
├── .editorconfig
├── .gitignore
├── .prettierrc.json
├── index.html
├── package.json                 # renamed/versioned
├── vercel.json
└── vite.config.js
```

## Before publishing

- Confirm your GitHub profile URL.
- Replace concept studies with real projects or keep their concept label visible.
- Add actual repository/demo links only when they exist.
- Run `npm run build` and test the deployed site on a phone.
