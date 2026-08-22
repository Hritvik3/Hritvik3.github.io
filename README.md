# Hritvik Patwa — Portfolio

Personal portfolio website built with React (Create React App). Live at **https://hritvik3.github.io**.

---

## Tech Stack

- React 16 (Create React App / `react-scripts`)
- `styled-components` for theming (`src/theme.js`, `src/global.js`)
- `react-router-dom` v5 for routing (`src/containers/Main.js`)
- `react-reveal` for scroll animations
- Font Awesome + Iconify (loaded via CDN in `public/index.html`) for icons
- Deployed as a static site to **GitHub Pages** via the `gh-pages` npm package

---

## Getting Started (Local Development)

```bash
# install dependencies
npm install

# start local dev server (http://localhost:3000)
npm start

# create a production build in /build
npm run build
```

> Note: scripts use `--openssl-legacy-provider` (`react-scripts 3.2.0` + newer Node versions need this flag). If `npm start`/`npm run build` fail with an OpenSSL error, make sure you're using the scripts defined in `package.json` and not calling `react-scripts` directly.

---

## Deployment (GitHub Pages)

This repo is named `Hritvik3.github.io`, which is what allows it to be served at the root domain `https://hritvik3.github.io` (GitHub Pages requires the special `username.github.io` repo name for root-domain hosting).

**Branch layout:**
- `main` — source code (what you edit)
- `gh-pages` — auto-generated production build output (never edit this branch by hand)

**To deploy the latest changes:**

```bash
npm run deploy
```

This runs `predeploy` (`npm run build`) automatically, then publishes the `/build` folder to the `gh-pages` branch using the `gh-pages` package. GitHub Pages is configured (repo **Settings → Pages**) to serve from the `gh-pages` branch, so the live site updates a minute or two after this finishes.

**Important:** Pushing to `main` alone does **not** update the live site — you must run `npm run deploy` after pushing/merging your changes.

### One-time GitHub Pages setup (already done, for reference)
1. Repo Settings → Pages → Source → select branch `gh-pages`, folder `/ (root)`.
2. `package.json` → `"homepage": "https://hritvik3.github.io"` (needed so built asset paths resolve correctly).

---

## Making Changes — Recommended Git Workflow

1. Create a new branch off `main` for your change:
   ```bash
   git checkout main
   git pull
   git checkout -b my-change
   ```
2. Make your edits, test locally with `npm start`.
3. Commit and push the branch, then merge into `main` (via PR or direct merge):
   ```bash
   git checkout main
   git merge my-change
   git push
   ```
4. Deploy:
   ```bash
   npm run deploy
   ```

---

## Where to Update Things

Almost all personal/content data lives in **`src/portfolio.js`** — you rarely need to touch component code just to update content.

| What you want to change | File |
|---|---|
| Site title, SEO meta description | `src/portfolio.js` → `seo` |
| Show/hide splash screen | `src/portfolio.js` → `settings.isSplash` |
| Name, tagline, resume link, GitHub profile link | `src/portfolio.js` → `greeting` |
| Social media links/icons | `src/portfolio.js` → `socialMediaLinks` |
| Skills sections (Data Science, Cloud, etc.) | `src/portfolio.js` → `skills` |
| Competitive coding profile links (LeetCode, Kaggle, etc.) | `src/portfolio.js` → `competitiveSites` |
| Education / degrees | `src/portfolio.js` → `degrees` |
| Certifications | `src/portfolio.js` → `certifications` |
| Work experience entries | `src/portfolio.js` → `experience.sections` |
| Projects page header text | `src/portfolio.js` → `projectsHeader` |
| Project cards shown on Projects page | `src/shared/opensource/projects.json` |
| Publications | `src/portfolio.js` → `publications` |
| Contact page text/photo | `src/portfolio.js` → `contactPageData` |
| Images used above (logos, icons, profile photo, etc.) | `src/assests/images/` — add your image file here, then reference its filename (e.g. `"logo_path": "my_logo.png"`) in the relevant `portfolio.js` entry |
| Color theme | `src/theme.js` |
| Global styles (fonts, body defaults) | `src/global.js`, `src/index.css` |

### Updating your Resume without a rebuild
`greeting.resumeLink` in `src/portfolio.js` points to a Google Drive share link. To update your resume with **no code changes needed**:
1. Open the file in Google Drive.
2. Use **File → Manage versions → Upload new version** (not "upload as a new file").
3. This keeps the same share URL, so the site's "See My Resume" button automatically serves the new PDF — no redeploy required.
4. Make sure sharing is set to **Anyone with the link → Viewer**.

### Adding a new project card
Add a new object to the `data` array in `src/shared/opensource/projects.json`:
```json
{
  "id": "unique-id",
  "name": "Project Name",
  "createdAt": "2024-01-01T00:00:00Z",
  "url": "https://github.com/your-username/your-repo",
  "description": "Short description of the project.",
  "isFork": false,
  "languages": [
    { "name": "Python", "iconifyClass": "logos-python" }
  ]
}
```
`iconifyClass` values can be looked up at [icon-sets.iconify.design](https://icon-sets.iconify.design/).

---

## Project Structure (high level)

```
public/            static HTML shell, favicon, manifest
src/
  portfolio.js     <-- most content edits happen here
  theme.js         color theme definitions
  global.js        global styled-components styles
  App.js           top-level app + theme provider
  containers/      routing (Main.js) + larger page sections (greeting, skills, education, experience accordion)
  pages/           one folder per route (home, education, experience, projects, contact, errors)
  components/      reusable UI pieces (header, footer, cards, buttons, social media icons, etc.)
  shared/opensource/projects.json   project cards data
  assests/images/  all images/logos used across the site
```

---

## Useful Links
- Repo: https://github.com/Hritvik3/Hritvik3.github.io
- Live site: https://hritvik3.github.io
- GitHub Pages docs: https://docs.github.com/en/pages
