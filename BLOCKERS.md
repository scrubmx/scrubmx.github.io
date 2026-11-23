# Blockers

## Featured Projects — no content in the repo

The reference has a Featured Projects section (cards with title, description, Source/Preview
links and a screenshot). This repo has no project content, and the reference's projects are
placeholders (Spotify/Shopify/Instagram clones) that must not ship.

Agreed handling: the section and its nav link are hidden, with `<!-- TODO -->` comments in
`index.html` and `_layouts/default.html`. This is the only intended layout difference from the
reference besides content changes.

To unblock: provide project names, one-line descriptions, source/preview URLs and a screenshot
for each. The card styles can be copied from the reference: `rounded-2xl` card, 1px
`neutral/20` border, `#1c232d` at 85% with texture, 2-column grid at ≥640px, `h-96` at ≥768px,
sticky stacking at `top: 98px + 40px` per card.

## Not blockers, noted for the record

- `https://www.linkedin.com/in/jorge-gnz` answers automated requests with HTTP 999
  (LinkedIn's bot block); the URL is as provided and loads in a browser.
- GitHub Pages is still set to "Deploy from a branch" (legacy Jekyll build). After merging,
  switch **Settings → Pages → Source** to **GitHub Actions** so `.github/workflows/deploy.yml`
  is used; the legacy builder doesn't support Jekyll 4.
