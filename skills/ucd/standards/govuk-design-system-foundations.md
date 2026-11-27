# GOV.UK Design System foundations: layout, type, colour and spacing

Use this when you change how a page is laid out or styled. The rule is simple: use the classes and Sass helpers GOV.UK Frontend provides, and write almost no CSS of your own.

Official source: https://design-system.service.gov.uk/styles/

The Styles section covers: page template, layout, spacing, section break, typeface, type scale, headings, paragraphs, links, lists, font override classes, colour and images.

## Check the version first

Look up `govuk-frontend` in `package.json`.

- **v6** changed the Sass architecture, colour names and functions, the type scale, the page template, and how the header and footer are customised. It also removed deprecated options. It needs Dart Sass 1.79.0 or later.
- **v5** changed the JavaScript to ES modules, moved files under `dist/`, and updated components for WCAG 2.2.
- **v4 or earlier** is out of date. Tell the developer. Do not upgrade it unless asked.

Never copy markup or Sass from a different major version to the one installed. If you are unsure, read the files in `node_modules/govuk-frontend/dist/govuk/`.

Changes in v6: https://frontend.design-system.service.gov.uk/changes-to-govuk-frontend-v6

## Page template

- Every page extends the project's layout, which extends the GOV.UK page template.
- The template provides the skip link, header, main wrapper and footer. Do not rebuild these by hand.
- Standard order inside the width container: phase banner, then back link or breadcrumbs, then `<main>`.
- Use either a back link or breadcrumbs, not both. Use a back link in transactional journeys.
- Show the service name in the header or service navigation, the same on every page.

## Layout

- Wrap content in `govuk-width-container`, then `govuk-main-wrapper` on `<main>`. The template does this for you.
- Use the grid: `govuk-grid-row` containing `govuk-grid-column-*` classes.
- Default to **two-thirds** width for content and forms. Long lines are hard to read.
- Use full width only for things that need it, such as wide tables or task dashboards.
- Do not nest width containers. Do not set fixed pixel widths.
- The layout is mobile first. Columns stack on small screens. Do not add your own breakpoints unless you have to, and then use the GOV.UK media query mixin.

## Spacing

- Use the spacing scale, not arbitrary values. In classes, use the override classes of the form `govuk-!-margin-bottom-6` or `govuk-!-padding-4`. In Sass, use the GOV.UK spacing function or responsive spacing mixins.
- Components carry their own spacing. Do not add margins around them unless a layout needs it.
- Use a section break (`govuk-section-break` with a size modifier) to separate sections, not empty elements or `<br>`.

## Typography

- Do not set `font-family`, `font-size` or `line-height` yourself. Use the classes.
- The GOV.UK typeface, GDS Transport, may only be used on services on the `gov.uk` domain. Elsewhere, the fallback fonts apply. Do not load it from another source.
- Headings: `govuk-heading-xl`, `-l`, `-m`, `-s`. Pick the element (`h1` to `h4`) by structure and the class by visual size. They do not have to match.
- A typical question page has an `h1` at size `l`. A typical content page has an `h1` at size `xl` or `l`, and `h2` at size `m`.
- Captions above headings: `govuk-caption-l` and similar, for a section name.
- Body text: `govuk-body`. Lead paragraph: `govuk-body-l`, at most one per page. Small text: `govuk-body-s`, sparingly.
- Lists: `govuk-list`, with `govuk-list--bullet` or `govuk-list--number`.
- Links: `govuk-link`. Add `govuk-link--no-visited-state` where visited styling is unhelpful, such as navigation or "Change" links.
- Links that open in a new tab: avoid. If you must, add "(opens in new tab)" to the link text and `rel="noreferrer noopener"`.
- Use the font override classes only when no semantic class fits.
- No italics. No underlining except links. Bold only for the few words a user must not miss. No all-capitals text.

## Colour

- Use the GOV.UK colour functions and variables in Sass. Do not hard-code hex values. The names and functions changed in v6, so check the installed version.
- Use functional colours by purpose: text, secondary text, link, focus, error, success, border.
- Do not create new colour meanings. Red means error. Green means success or a primary action. Yellow means focus.
- Do not use tint or brand colours for decoration.
- Any custom colour pairing must meet contrast: 4.5:1 for text, 3:1 for large text and for the edges of controls.
- The focus style is a yellow background with a thick dark underline or outline. Never change it.

## Images and icons

- Avoid decorative images. They slow pages and distract.
- Use images only when they help users do the task, such as showing where to find a number on a document.
- Give informative images `alt` text. Give decorative ones `alt=""`.
- Do not add icon libraries. GOV.UK services use very few icons, and each one that exists is part of a component.
- Do not use the crown logo, crest or GOV.UK logo anywhere other than through the header component, and only on `gov.uk` domains.

## Writing your own CSS

Sometimes you have to. When you do:

- Prefix classes with the project's own prefix, such as `app-`. Never use `govuk-` or `moj-` for your own classes.
- Never override `govuk-` classes. Add a modifier class of your own next to them.
- Use GOV.UK Sass mixins for type, spacing, media queries and focus.
- Follow the same naming convention as GOV.UK Frontend: block, element, modifier.
- Keep it in the project's existing stylesheet structure.
- Tell the developer what you added and why no existing class worked.

## Checklist

- [ ] Installed `govuk-frontend` version checked, and markup matches it
- [ ] Page extends the existing layout
- [ ] Content in a two-thirds column unless it needs more
- [ ] No hard-coded colours, font sizes or pixel spacing
- [ ] No overrides of `govuk-` or `moj-` classes
- [ ] Heading elements follow structure, classes follow size
- [ ] Custom classes use the project prefix and are listed in the summary
