# Yongkang Yang

Source for [yongkang-yang.github.io/Yongkang-Yang](https://yongkang-yang.github.io/Yongkang-Yang/): a blog-first personal site (Hugo, no theme) with About, Research, and Teaching pages.

## Layout

- `content/posts/`: blog posts (moved from `source-ykblog`; URLs keep the `/posts/<slug>/` shape)
- `content/about.md`, `content/research.md`, `content/teaching.md`: the former homepage, split into pages
- `static/data/`, `static/images/`: paper PDFs and images, served at the same paths as before
- `layouts/`, `static/css/site.css`: a few plain templates and one stylesheet in the original homepage style (Lato, blue links, one 800px column)
- `.github/workflows/hugo.yml`: builds on every PR, deploys to GitHub Pages on push to `master`

## Local preview

```bash
hugo server            # Hugo >= 0.146
```

New post: `hugo new content posts/my-post.md`.

The teaching video is hosted on Cloudflare R2 (`homepage/` prefix), not in this repo.
