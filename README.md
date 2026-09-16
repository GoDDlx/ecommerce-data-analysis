# E-Commerce Data Analysis — Data Analyst Portfolio Project

An interactive case-study page covering the full analytics workflow:
**Collect → Clean → Analyze → Visualize → Communicate**

Built with React + TypeScript, Vite, Tailwind CSS, Chart.js and Lucide icons.

---

## Quick start

```bash
npm install     # install dependencies
npm run dev     # local dev server (http://localhost:5173)
npm run build   # production build → dist/index.html
npm run preview # preview the production build locally
```

> **Note:** this project uses `vite-plugin-singlefile`, so the entire site builds
> into **one self-contained `dist/index.html`** with all JS and CSS inlined.
> There are no relative asset references, which is why GitHub Pages works
> without any `base` path configuration.

---

## Deploying to GitHub

### Step 1 — Create the repository

Create a new **empty** repo on GitHub (no README, no .gitignore — this project
already has both).

### Step 2 — Push the code

```bash
git init
git add .
git commit -m "E-Commerce Data Analysis portfolio project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
```

Replace `YOUR-USERNAME` and `YOUR-REPO` with your own values.

### Step 3 — Turn on GitHub Pages ⚠️ required

In your repo: **Settings → Pages → Build and deployment → Source**, select
**GitHub Actions**.

This step is easy to miss. If you skip it, the workflow's deploy job fails with
a "Pages is not enabled" style error.

### Step 4 — Wait for the build

The included workflow (`.github/workflows/deploy.yml`) runs automatically on
every push to `main`. Watch it under the **Actions** tab. When it finishes, your
site is live at:

```
https://YOUR-USERNAME.github.io/YOUR-REPO/
```

Every later `git push` to `main` redeploys automatically.

---

### Alternative: deploy without GitHub Actions

Because the build is a single HTML file, you can also publish manually:

```bash
npm run build
```

Then either:

- **Netlify / Vercel / Cloudflare Pages** — connect the repo, set build command
  `npm run build` and publish directory `dist`.
- **Drag-and-drop** — upload `dist/index.html` to Netlify Drop, or open it
  straight from your filesystem (it works offline, fonts excluded).
- **`gh-pages` branch** — commit just `dist/index.html` to a `gh-pages` branch
  and point Settings → Pages at that branch. Remember to remove `dist/` from
  `.gitignore` if you go this route.

---

## Customizing the content

Everything editable lives in **one file**:

```
src/data/projectData.ts
```

It is split into numbered, commented sections:

| Section | What it controls |
| --- | --- |
| 1. `LINKS` | ⚠️ GitHub, Tableau and dataset URLs (**placeholders — replace these**) |
| 2. `AUTHOR` | Your name, role and year |
| 3. `PROJECT` | Title, subtitle, overview, business problem, conclusion |
| 4. `TECHNOLOGIES` | The tools & technologies badges |
| 5. `KPIS` | The four headline metrics and their deltas |
| 6. Chart data | `SALES_TREND`, `TOP_PRODUCTS`, `CUSTOMER_SEGMENTS`, `REGIONS`, `CATEGORIES` |
| 7. `DATASET` | Dataset description and the schema table |
| 8. `WORKFLOW` | The six pipeline stages |
| 9. `CLEANING_STEPS` / `CLEANING_STATS` | Data-cleaning checklist and before/after numbers |
| 10. `SQL_QUESTIONS` / `SQL_SNIPPET` | Analytical questions and SQL code shown on the page |
| 11. `PYTHON_LIBS` / `PYTHON_SNIPPET` | Python libraries and code snippet |
| 12. `EDA_FINDINGS` | Exploratory analysis notes |
| 13. `INSIGHTS` | The key-insight cards |
| 14. `TABLEAU_FEATURES` | Dashboard feature list |

Change a number there and the KPI cards, charts, tooltips and percentages all
update together — no component edits needed.

### Before you publish

Search for `⚠️ REPLACE` in `src/data/projectData.ts` and swap in:

- `LINKS.github` — your repository URL
- `LINKS.tableau` — your published Tableau Public dashboard URL
- `LINKS.dataset` — your dataset source
- `AUTHOR.name` — your name

---

## Project structure

```
src/
├── data/projectData.ts        # ← all content, numbers and URLs
├── lib/chartSetup.ts          # Chart.js registration + shared theme
├── hooks/useAnimation.ts      # in-view, count-up, scroll-lock hooks
├── components/
│   ├── ProjectCard.tsx        # hero project card (hover interactions)
│   ├── ProjectModal.tsx       # full-screen case study
│   ├── Dashboard.tsx          # Tableau-style analytics canvas
│   ├── KpiCards.tsx           # animated KPI tiles
│   ├── charts/Charts.tsx      # the six Chart.js charts
│   ├── sections/              # workflow, cleaning, SQL, Python, insights
│   └── ui/                    # icons, code block, badges, buttons
└── App.tsx                    # page shell
```

---

## Troubleshooting

**Actions run succeeds but the page is 404.**
Pages source is probably still "Deploy from a branch". Set it to
**GitHub Actions** (Step 3) and re-run the workflow.

**Deploy job fails with a permissions error.**
Check **Settings → Actions → General → Workflow permissions** and ensure
Actions are allowed to run for the repository.

**`npm ci` fails in CI.**
`package-lock.json` must be committed. It is not ignored by this `.gitignore`,
so confirm it was included in your first commit.

**Page loads but looks unstyled for a moment.**
That is the Google Fonts request resolving. The layout itself is fully inlined
and does not depend on the network.
