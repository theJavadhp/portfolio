# javadhakimpanah — portfolio

Personal portfolio site for Javad Hakimpanah — UI/UX Designer & Front-End Developer, Toronto.

Single self-contained `index.html`. No build step, no dependencies, no framework. All CSS is inline in the document head.

## Local preview

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000

## Deploy

**Cloudflare Pages** (recommended — lets you pick the subdomain)
1. Push this repo to GitHub
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git
3. Pick this repo. Build command: *(leave empty)*. Build output directory: `/`
4. Deploy. Set the project name to `javadhakimpanah` for `javadhakimpanah.pages.dev`

**GitHub Pages**
1. Push to GitHub
2. Repo → Settings → Pages → Source: `main`, folder: `/ (root)`
3. Live at `https://<username>.github.io/<repo>`

**Netlify Drop** (no git needed)
Drag this folder onto https://app.netlify.com/drop

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole site |
| `01_Resume_Javad_Hakimpanah_ATS.pdf` | Résumé, linked from the hero |
| `.nojekyll` | Stops GitHub Pages running Jekyll |

## Contact

mjhp29@yahoo.com · [linkedin.com/in/javadhakimpanah](https://www.linkedin.com/in/javadhakimpanah)
