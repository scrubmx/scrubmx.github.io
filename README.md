# scrubmx.github.io

Personal portfolio of Jorge González, Senior Full Stack Developer, live at
[scrubmx.github.io](https://scrubmx.github.io).

It's a single static page built with Jekyll and deployed to GitHub Pages. Its design is modelled
on [Astro Zen](https://github.com/immois/astro-zen) by Moisés Machuca.

![Portfolio at 1440px](screenshots/final-1440.png)

## Structure

| Path | Contents |
| --- | --- |
| `index.html` | Page content: hero, work experience, about |
| `_layouts/default.html` | Meta tags, sticky header and mobile menu, footer, nav script |
| `assets/css/style.css` | All styles (no framework). Values copied from the reference's computed styles |
| `assets/images/` | Profile photo, favicon, check and external-link icons |
| `_config.yml` | Site title, author, description, URL |
| `.github/workflows/deploy.yml` | Builds with Jekyll and deploys to GitHub Pages |

Fonts are [Gabarito](https://fonts.google.com/specimen/Gabarito) for headings and
[Be Vietnam Pro](https://fonts.google.com/specimen/Be+Vietnam+Pro) for body text, loaded from
Google Fonts at weight 400 only. The browser synthesizes the bold, as on the reference.

## Editing content

- **Work experience:** each role is a `.job` block in `index.html`. Bullets are copied verbatim
  from the resume.
- **Featured Projects:** not built yet. Look for the `<!-- TODO -->` comments in `index.html` and
  `_layouts/default.html`, and see [BLOCKERS.md](BLOCKERS.md) for what's needed.
- **Name, title and meta description:** set in `_config.yml`.

## Local development

Requires Docker. A system Ruby works too, as long as it's 3.x with Bundler.

Build the site into `_site/`:

```bash
docker run --rm -v "$PWD":/srv -v jekyll-gems:/usr/local/bundle -w /srv ruby:3.3 sh -c "bundle install && bundle exec jekyll build"
```

Serve the build with a plain static server:

```bash
python3 -m http.server 4000 -d _site
```

Then open http://localhost:4000.

## Deployment

Each push to `master` runs `.github/workflows/deploy.yml`. It builds the site with Jekyll 4 and
publishes it with the official `actions/upload-pages-artifact` and `actions/deploy-pages`
actions. Asset paths use Jekyll's `relative_url` filter, so the build works at the domain root
or under a sub-path.

One-time setup: in the repo's **Settings → Pages**, set **Source** to **GitHub Actions**.

## License

[MIT](LICENSE).
