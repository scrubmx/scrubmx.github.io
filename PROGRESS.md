# Progress

Reference: https://astro-zen.vercel.app/ — compared at 1440px and 390px with Playwright
(full-page + per-section screenshots, plus a computed-style diff of every styled element).

## Iteration 1 — rebuild as single-page portfolio

Starting point was the Kactus/Cactus blog theme, so the first pass replaced it wholesale.
Top 3 visible differences before this iteration:

1. **Layout/structure** — blog post list + profile header vs. single-page hero / experience / about.
   Fixed: new `index.html` sections and `_layouts/default.html` (sticky header, footer).
2. **Typography** — theme fonts vs. Gabarito (headings) and Be Vietnam Pro (body), both declared at
   weight 400 only so bold is browser-synthesized, as on the reference. Fixed via Google Fonts.
3. **Colors/spacing** — light theme vs. `#0e141b` bg, `#e2e8f0` text, `#94a3b8` neutral, `#2563eb`
   primary, 18px base text, 48rem column. Fixed in `assets/css/style.css` with values from the
   reference's computed styles.

Result: computed-style diff shows only content-driven geometry (longer text, fewer nav/footer links),
`object-fit: cover` (the profile photo is not square) and colour/radius notation differences.

## Iteration 2 — exact colour and radius values

1. `.job-meta span` colour and the footer/menu border colours used `rgba()` approximations; the
   reference uses `oklab()`. Copied the exact oklab values.
2. Rounded-full radius `9999px` vs. Tailwind's `calc(infinity * 1px)`. Copied exactly.
3. About padding sits on the wrapper instead of the `<p>`: identical box (no change needed).
4. **Active nav state never showed** (found by the interaction-state check): the reference's
   IntersectionObserver uses `threshold: 0.5`, which a ~3,500px-tall Work Experience section can
   never reach. Switched to `rootMargin: '-50% 0px -50% 0px'` (section crossing mid-viewport) so
   the white text + blue dot appear as on the reference.

After iteration 2, interaction states match the reference exactly: nav hover `#e2e8f0`, footer hover
`#2563eb`, active link white + dot at md, header scroll-linked slide (−29.2979px at 300px scroll on
both), mobile menu toggles with `aria-expanded`.
