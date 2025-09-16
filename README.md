# mike7seven.github.io

Personal GitHub Pages site for Mike Weihrouch. The published site is built from
this repo's `content.md` using the [React Slides](https://github.com/STR-Ventures/react-slides)
presentation framework.

## How the site is built

- Every push to `main` (or manual dispatch) runs
  [`.github/workflows/ci.yaml`](.github/workflows/ci.yaml).
- The workflow checks out this repo **and** the `react-slides` repo.
- `content.md` is copied into `react-slides/public/` so the slide deck can
  render it.
- The React Slides project is installed and built with Vite, producing the
  static site under `react-slides/dist/`.
- `actions/upload-pages-artifact` packages the build output, and
  `actions/deploy-pages` publishes it to GitHub Pages at
  <https://mike7seven.github.io/>.

### Secrets

- `GH_PAT`: personal access token that allows the workflow to pull the private
  `react-slides` repository. Ensure it has **repo** scope.

## Editing content

1. Update `content.md` with new markdown sections and links.
2. Commit and push to `main`.
3. Wait for the GitHub Actions deployment to finish; the site updates
   automatically.

## Previewing locally

You can build the site locally with the React Slides repo:

```bash
git clone https://github.com/mike7seven/react-slides.git
cd react-slides
cp ../mike7seven.github.io/content.md public/
npm install
npm run dev
```

Open the local dev server URL (default `http://localhost:5173`) to see the
changes before pushing.

## Troubleshooting

- Ensure the workflow reports success in GitHub Actions; rerun the job if
  GitHub Pages reports transient download errors.
- Check that `VITE_BASE_URL` stays `/` so static assets resolve on the root
  domain.
