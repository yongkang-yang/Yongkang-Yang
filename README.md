# Yongkang Yang

Source for [yongkang-yang.github.io/Yongkang-Yang](https://yongkang-yang.github.io/Yongkang-Yang/): a blog-first personal site (Hugo + PaperMod) with About, Research, and Teaching pages.

## Layout

- `content/posts/`: blog posts (moved from `source-ykblog`; URLs keep the `/posts/<slug>/` shape)
- `content/about.md`, `content/research.md`, `content/teaching.md`: the former homepage, split into pages
- `static/data/`, `static/images/`: paper PDFs and images, served at the same paths as before
- `themes/PaperMod/`: vendored theme
- `.github/workflows/hugo.yml`: builds on every PR, deploys to GitHub Pages on push to `master`

## Local preview

```bash
hugo server            # needs Hugo extended >= 0.146
```

New post: `hugo new content posts/my-post.md`.

The teaching video is hosted on Cloudflare R2 (`homepage/` prefix), not in this repo.
