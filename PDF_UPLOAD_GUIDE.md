# How to put a project PDF on the website

Your setup uses **two repos**:

| Repo | Purpose |
|---|---|
| `Qaqqaqaqaaq/qaqqaqaqaaq.github.io` | The Jekyll website itself (this folder) |
| `qaqqaqaqaaq/cedricphillips.github.io` | PDF hosting — reports live in its `pdf2/` folder |

**PDFs go in the second repo, not this one.** The `pdf2/` folder inside this repo is a leftover local copy — nothing on the site links to it.

## Step-by-step

### 1. Name the file correctly
- Must end in `.pdf` (lowercase). Without the extension, GitHub serves it as a raw download instead of rendering it in the PDF viewer.
- No spaces — use underscores or hyphens, e.g. `math_470_hierarchical_trees.pdf`.

### 2. Upload to the PDF repo
Easiest way (browser):
1. Go to https://github.com/qaqqaqaqaaq/cedricphillips.github.io/tree/main/pdf2
2. **Add file → Upload files**
3. Drag the PDF in, write a short commit message, **Commit changes** to `main`.

Or by command line, from a local clone of that repo:
```
cp ~/path/to/report.pdf pdf2/
git add pdf2/report.pdf
git commit -m "Add report PDF"
git push
```
(GitHub renders PDFs up to ~25 MB in the viewer; files over 100 MB are rejected entirely. Compress large reports first.)

### 3. Link it from a website page
In this repo, edit the relevant page **in all three languages** (`en/`, `fr/`, `hi/` — e.g. `math-projects.html`), using this exact URL pattern:

```html
<a href="https://github.com/qaqqaqaqaaq/cedricphillips.github.io/blob/main/pdf2/YOUR_FILE.pdf" target="_blank">Report (PDF)</a>
```

- Use `github.com/...../blob/main/pdf2/...` → opens GitHub's nice PDF viewer.
- The résumé is the one exception: it uses `raw.githubusercontent.com/...` for a direct download.
- The filename in the link must match the uploaded filename **exactly** (case-sensitive).

### 4. Push the website changes
```
git add en/ fr/ hi/
git commit -m "Link new PDF"
git push
```

### 5. Verify
Wait a minute for GitHub Pages to rebuild, then click the link on the live site. If you get a 404, the filename in the link doesn't match what's in `pdf2/` (check extension and capitalization).

## Common mistakes (all have happened on this site)
- **Adding the link before uploading the PDF** → 404. Two links are currently in this state: `math_470_hierarchical_trees.pdf` and `geog_506_spatial_knn.pdf`.
- **Uploading without the `.pdf` extension** → file downloads as a blob instead of rendering. Currently true of `math-330-martingales`, `math-358-advanced-calculus`, `math-454-analysis-3`.
- **Putting the PDF in this repo's `pdf2/`** → does nothing; links point at the other repo.
- **Updating only the English page** → fr/hi pages go stale.
