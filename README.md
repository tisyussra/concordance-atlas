# concordance-atlas
# Concordance Atlas

Interactive KWIC concordance and collocate analysis of the Corpus of Founding Era American English (COFEA) and the Corpus of Early Modern English (COEME), focused on the Second Amendment lexicon.

## Run locally

You need Node.js 18+ installed. Get it from [nodejs.org](https://nodejs.org/) if you don't have it.

```bash
npm install
npm run dev
```

Open the URL it prints (usually `http://localhost:5173`).

## Deploy to Vercel (easiest, ~5 minutes)

1. Create a free account at [vercel.com](https://vercel.com) — sign in with GitHub.
2. Push this folder to a new GitHub repo:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/concordance-atlas.git
   git push -u origin main
   ```
3. On Vercel, click **Add New → Project**, pick the repo, and click **Deploy**.
4. Vercel auto-detects Vite. Done. You get a URL like `concordance-atlas.vercel.app`.

Every time you `git push`, Vercel redeploys automatically.

## Deploy to Netlify (alternative)

1. Run `npm run build` locally — this creates a `dist/` folder.
2. Go to [netlify.com](https://netlify.com), drag the `dist/` folder onto the page.
3. You get a URL instantly.

For auto-deploy on push, connect the GitHub repo through Netlify's dashboard instead.

## Deploy to GitHub Pages

1. Add this to `vite.config.js`:
   ```js
   export default defineConfig({
     plugins: [react()],
     base: '/concordance-atlas/', // your repo name
   });
   ```
2. Install the deploy helper:
   ```bash
   npm install -D gh-pages
   ```
3. Add to `package.json` scripts:
   ```json
   "deploy": "npm run build && gh-pages -d dist"
   ```
4. Run `npm run deploy`. URL will be `YOUR_USERNAME.github.io/concordance-atlas`.

## Project layout

```
concordance-atlas/
├── public/
│   ├── concordances.json   # 14,948 KWIC lines (5.3 MB)
│   ├── collocates.json     # statistical collocate analysis (22 KB)
│   └── favicon.svg
├── src/
│   ├── main.jsx            # React entry
│   └── App.jsx             # the whole app
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

## Updating the data

If you re-run the corpus queries and want to refresh the data, just replace `public/concordances.json` and `public/collocates.json`. The expected JSON shapes are:

**concordances.json** — array of objects with short keys:
- `q` (query/search term), `c` (corpus: "COFEA" | "COEME"), `y` (year)
- `L` (left context), `m` (match/keyword), `R` (right context)
- `a` (author), `t` (title), `l` ("L" for Legal, "N" for Non-Legal), `s` (sub-genre)

**collocates.json** — `{ data: { query: [...] }, meta: { query: { lines, window } } }`. Each collocate has `rank, word, freq, corpus_freq, doc_pct, ratio, mi, g2`.

## Credits

Data: COFEA and COEME, BYU Law School.
Statistical method: log-likelihood G² (Dunning 1993), pointwise mutual information.
