# Welcome to Abdubidopsis Profile

A minimal Quarto website scaffold ready for GitHub Pages.

## Local preview

1. Install Quarto: https://quarto.org/docs/get-started/
2. Run:

   ```bash
   quarto preview
   ```

## Publish to GitHub

1. Create the repository on GitHub if it does not already exist.
2. Make the first commit locally, then push `main`.
3. In GitHub, enable Pages from the `gh-pages` branch, or let the workflow deploy it.
4. Push changes to `main`; the workflow will render and publish the site.

## First push fix

If you see `src refspec main does not match any`, it usually means there is no commit yet.

Run:

```bash
git add .
git commit -m "Initial Quarto website"
git push -u origin main
```

## Files

- `_quarto.yml` configures the site.
- `index.qmd` is the homepage.
- `about.qmd` is an extra page.
- `styles.css` adds a simple visual theme.
