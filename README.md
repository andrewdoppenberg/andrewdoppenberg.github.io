# andrewdoppenberg.github.io

Academic website. One HTML file, no build step, no dependencies. Editing
`index.html` and pushing to `main` publishes the site.

## Files

| Path | Notes |
| --- | --- |
| `index.html` | The whole site: markup, styles, and structured data. |
| `files/cv.pdf` | Copied from `02_Curriculum_Vitae/cv.pdf` after each rebuild. |
| `files/headshot.jpg` | 512&nbsp;px square, metadata stripped, quality 85. |
| `favicon.ico` | 16/32/48&nbsp;px. `apple-touch-icon.png` is 180&nbsp;px. |
| `robots.txt`, `sitemap.xml` | Update `lastmod` when the page changes. |

Names are case-sensitive on GitHub Pages, so they must match the markup exactly.

## What is published here

The CV is the only document on the site. The research statement, writing
sample, teaching dossier, and dissertation abstract are sent on request.
Do not add them to `files/` — anything committed here stays retrievable from
the repository history even after it is deleted from the working tree.

## Updating the headshot

Resize to 512&nbsp;px and strip the camera metadata before committing. A
straight export carries the camera model, lens, editing software, and capture
timestamp, and is roughly eight times larger than it needs to be.

```python
from PIL import Image
src = Image.open("original.jpg").convert("RGB").resize((512, 512), Image.LANCZOS)
clean = Image.new("RGB", src.size)      # a fresh image carries no metadata
clean.putdata(list(src.getdata()))
clean.save("files/headshot.jpg", "JPEG", quality=85, optimize=True, progressive=True)
```

## Conventions worth keeping

- The abstract in the title block is the part a search committee actually
  reads. Three sentences: what you study, what your best paper found, what you
  are looking for.
- Section numbers (`§1`–`§4`) are decorative and marked `aria-hidden`. Renumber
  them together if a section is added or removed.
- Every colour is a custom property in `:root`. Small text uses `--pencil`,
  which sits at 4.98:1 against `--paper`. Do not lighten it past 4.5:1.
- Links are omitted rather than left broken. A dead link on a job market page
  is worse than no link.
- Check the page at <https://validator.w3.org/nu/> after structural edits.
