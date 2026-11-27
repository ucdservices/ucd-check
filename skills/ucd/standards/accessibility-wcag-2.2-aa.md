# Accessibility: WCAG 2.2 level AA

Public sector services in the UK must meet WCAG 2.2 level AA under the Public Sector Bodies (Websites and Mobile Applications) Accessibility Regulations 2018. They must also publish an accessibility statement.

This file tells you what to do in code. It is written as rules you can check, grouped by the kind of work you are doing. Success criterion numbers are given so the developer can look them up.

Official sources:

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- Service Manual, making your service accessible: https://www.gov.uk/service-manual/helping-people-to-use-your-service/making-your-service-accessible-an-introduction
- GOV.UK Design System accessibility: https://design-system.service.gov.uk/accessibility/

## The most important rule

GOV.UK Design System components are built and tested to meet WCAG 2.2 AA. You keep that benefit only if you:

- use the component's markup unchanged, from the installed version
- do not override its focus, colour or spacing styles
- do not remove its ARIA attributes, visually hidden text or `data-module` attributes
- load and initialise GOV.UK Frontend JavaScript so components that need it work

Most accessibility failures in government services come from custom components, changed markup and unclear content. Avoid all three.

## Page structure

- Set `lang="en"` on `<html>`. Mark up text in another language, such as Welsh, with its own `lang` attribute. (3.1.1, 3.1.2)
- Give every page a unique `<title>` that starts with the page's `<h1>` text, then the service name, then "GOV.UK". When the page shows validation errors, start the title with "Error: ". (2.4.2)
- Use exactly one `<h1>` per page. Do not skip heading levels. Do not use heading classes on text that is not a heading, or heading elements just for size. (1.3.1, 2.4.6)
- Keep the skip link as the first focusable element, and keep `id="main-content"` on `<main>`. (2.4.1)
- Use landmark elements once each: `<header>`, `<main>`, `<footer>`. Put the back link, breadcrumbs and phase banner outside `<main>`.
- Keep DOM order the same as visual order. Do not reorder content with CSS. (1.3.2, 2.4.3)
- Use lists for lists and `<table>` only for data. Give tables a `<caption>` and `scope` on header cells. (1.3.1)

## Forms

- Every input has a visible `<label>` linked by `for` and `id`. Placeholder text is not a label. Do not use placeholder text at all. (1.3.1, 3.3.2, 4.1.2)
- Group radios, checkboxes and date fields in a `<fieldset>` with a `<legend>` that asks the question. (1.3.1)
- Link hint text and error messages to the input with `aria-describedby`. The macros do this for you. (1.3.1, 3.3.1)
- Add `autocomplete` attributes to fields that collect the user's own details, such as `name`, `email`, `tel`, `postal-code`, `bday-day`. (1.3.5)
- Do not use `type="number"`. For whole numbers use `type="text"` with `inputmode="numeric"`. Set `spellcheck="false"` on fields like names, reference numbers and email addresses.
- Do not disable buttons to show a form is incomplete. Let the user submit and show errors. (Disabled controls are hard to perceive and cannot take focus.)
- When validation fails, show an error summary at the top, move focus to it, and show a message next to each field. Messages must be text and must say how to fix the problem. (3.3.1, 3.3.3)
- For anything legal, financial or that changes stored data, give the user a way to check and change answers before they submit. (3.3.4)

## Keyboard and focus

- Everything works with the keyboard alone, with no traps. (2.1.1, 2.1.2)
- Never remove or restyle the GOV.UK focus style. Never set `outline: none` without the replacement the Design System provides. (2.4.7)
- Do not use positive `tabindex` values. Use `tabindex="-1"` only to move focus to something by script.
- Make things that go somewhere links, and things that do something buttons. Do not attach click handlers to `<div>` or `<span>`. (4.1.2)
- Link text makes sense on its own. Not "click here" or "more". When several links share the same text, such as "Change", add visually hidden text to say what each one changes. (2.4.4)

## Colour, text and layout

- Use GOV.UK Frontend colour variables and helpers. Do not hard-code hex values.
- Text contrast is at least 4.5:1, or 3:1 for large text. Borders and states of controls, and meaningful graphics, are at least 3:1. (1.4.3, 1.4.11)
- Never use colour alone to show meaning. Pair it with text or an icon that has a text alternative. (1.4.1)
- Pages work at 320 CSS pixels wide with no horizontal scrolling, and at 400% zoom. Use the GOV.UK grid, not fixed widths. (1.4.10)
- Text can be resized to 200% and line, word and letter spacing can be increased without content being cut off. Do not set fixed heights on containers of text. (1.4.4, 1.4.12)
- Do not put text in images. (1.4.5)
- Do not lock orientation. (1.3.4)

## Images and media

- Informative images have `alt` text that says what a sighted user learns from them. Decorative images have `alt=""`. (1.1.1)
- Avoid icons without visible text. If you use one, give it an accessible name.
- Video needs captions and audio description or a transcript. Do not autoplay. (1.2.x, 1.4.2)
- Nothing flashes more than 3 times a second. Movement that starts on its own and lasts more than 5 seconds can be paused. Respect `prefers-reduced-motion`. (2.3.1, 2.2.2)

## Dynamic content and JavaScript

- The page works with JavaScript off. Then enhance.
- When content changes without a page load, tell assistive technology. Use `role="alert"` for errors and `role="status"` or `aria-live="polite"` for other updates. Do not move focus unless the user asked for the change. (4.1.3)
- Changing a field's value or focusing it must not submit a form, open a window or move the user. (3.2.1, 3.2.2)
- If the session times out, warn the user and let them extend it, and do not lose what they entered. (2.2.1)
- Content that appears on hover or focus can be dismissed, hovered over and stays until dismissed. Prefer not to use hover content at all. (1.4.13)

## New in WCAG 2.2: check these every time

Coding agents and older codebases often miss these because they were added in 2.2.

| Criterion | What to do |
|---|---|
| 2.4.11 Focus not obscured (AA) | A focused element must not be fully hidden by sticky headers, cookie banners or fixed footers. Avoid sticky elements. If one exists, add `scroll-padding` so focus stays visible. |
| 2.5.7 Dragging movements (AA) | Anything done by dragging, such as reordering or sliders, also works with a single click or tap, for example "Move up" and "Move down" buttons. |
| 2.5.8 Target size (AA) | Clickable targets are at least 24 by 24 CSS pixels, or have enough space around them. Do not shrink GOV.UK buttons, radios or checkboxes. Take care with icon buttons and tightly packed inline links. |
| 3.2.6 Consistent help (A) | If pages offer help, such as a contact link or phone number, put it in the same place on every page. |
| 3.3.7 Redundant entry (A) | Do not ask for the same information twice in one journey. Pre-fill it or let the user pick it. Keep answers when the user goes back. |
| 3.3.8 Accessible authentication (AA) | Sign-in must not rely on memory or puzzles alone. Allow paste and password managers. Do not block `autocomplete` on password or code fields. Do not use CAPTCHAs that need solving. |

WCAG 2.2 removed 4.1.1 Parsing. You should still output valid HTML with unique `id` values, because duplicate ids break labels and error links.

## ARIA

- Prefer native HTML. A `<button>` is better than `role="button"`.
- Do not add ARIA to GOV.UK components beyond what their macros produce.
- Never use `aria-hidden="true"` on anything focusable.
- If you must build a custom widget, follow the matching pattern in the WAI-ARIA Authoring Practices and flag it for testing with assistive technology.

## How to test your change

Do these in order before you say the work is done.

1. **Automated check.** Run the project's accessibility tests if it has them, such as axe-core or pa11y. If it has none, tell the developer and suggest adding them. Automated tools find only a minority of problems, so a pass does not mean the page is accessible.
2. **HTML check.** Confirm one `<h1>`, a correct `<title>`, no duplicate ids, and that every input has a label.
3. **Keyboard walk-through.** Describe the tab order from the skip link to the footer. Confirm every control is reachable, focus is visible, and after a failed submit focus lands on the error summary.
4. **Zoom and reflow.** Confirm the layout uses grid classes and has no fixed widths or heights that would break at 320 pixels or 400% zoom.
5. **JavaScript off.** Confirm the journey can still be completed.

## What you cannot check

Tell the developer a human needs to:

- test with screen readers, voice control and screen magnifiers
- test with disabled users as part of user research
- get an accessibility audit before the service goes to public beta
- write and publish the accessibility statement

## Checklist

- [ ] Only GOV.UK or MoJ components used, with unchanged markup
- [ ] One `<h1>`, unique `<title>`, correct heading order
- [ ] Every input has a visible label, and groups have a legend
- [ ] `autocomplete` set on personal detail fields
- [ ] Errors shown in a summary and next to fields, in text
- [ ] Keyboard only: all controls reachable, focus always visible and not hidden
- [ ] No colour-only meaning, no hard-coded colours
- [ ] Works at 320 pixels wide and with JavaScript off
- [ ] Targets at least 24 by 24 CSS pixels
- [ ] No information asked for twice
- [ ] Paste allowed in every field
- [ ] Human checks listed in the summary
