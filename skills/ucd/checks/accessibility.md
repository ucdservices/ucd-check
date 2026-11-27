# Accessibility

WCAG 2.2 level AA issues that can be found by reading code.

## When this check applies

Run this check on user-facing templates, styles and client-side scripts. Skip it for code a user never encounters, and say why. This check only reports what the source shows. It does not test with assistive technology.

## What to look for

Use [Accessibility: WCAG 2.2 level AA](../standards/accessibility-wcag-2.2-aa.md). Keep GOV.UK and MoJ markup unchanged, including focus, colour, spacing, ARIA, visually hidden text and `data-module`. See [The most important rule](../standards/accessibility-wcag-2.2-aa.md).

- `lang` on `<html>`, and `lang` on any text in another language. One `<h1>`, no skipped heading levels, a unique `<title>` that starts with the `<h1>` text, then the service name, then "GOV.UK", and "Error: " when validation fails. Skip link first, `id="main-content"` on `<main>`. See [Page structure](../standards/accessibility-wcag-2.2-aa.md).
- Every input has a visible `<label>` linked by `for` and `id`. Groups use a `<fieldset>` and `<legend>`. Hints and errors are in `aria-describedby`. No placeholder text. `autocomplete` on the user's own details. No `type="number"`. `spellcheck="false"` on names, reference numbers and email addresses. See [Forms](../standards/accessibility-wcag-2.2-aa.md).
- Do not disable a button to show a form is incomplete. Do not remove the GOV.UK focus style or set `outline: none` without the Design System focus style. No positive `tabindex`. Links go somewhere, buttons do something, and click handlers are not on a `<div>` or `<span>`. "Change" and other repeated links need visually hidden text. See [Keyboard and focus](../standards/accessibility-wcag-2.2-aa.md).
- No hard-coded hex colours. Do not use colour alone. No fixed widths that break 320 CSS pixels or 400% zoom. No fixed heights on text. No text in images. Informative images have `alt` text. Decorative images have `alt=""`. See [Colour, text and layout](../standards/accessibility-wcag-2.2-aa.md) and [Images and media](../standards/accessibility-wcag-2.2-aa.md).
- The page works without JavaScript. Do not submit a form, open a window or move the user when a field changes or receives focus. If a session can time out, warn the user and let them extend it. See [Dynamic content and JavaScript](../standards/accessibility-wcag-2.2-aa.md).
- The WCAG 2.2 items in [New in WCAG 2.2](../standards/accessibility-wcag-2.2-aa.md): focus not fully hidden by a sticky header or footer (2.4.11), a click or tap alternative to dragging (2.5.7), targets at least 24 by 24 CSS pixels and no shrunk GOV.UK controls (2.5.8), help in the same place on every page (3.2.6), do not ask for the same information twice (3.3.7), allow paste and password managers and do not use a CAPTCHA for sign-in (3.3.8).
- Unique `id` values. Prefer native HTML to ARIA. Do not add ARIA to a GOV.UK component beyond what its macro outputs. Do not put `aria-hidden="true"` on anything focusable. See [ARIA](../standards/accessibility-wcag-2.2-aa.md).
- Paste is allowed in every field. See the accessibility checklist in [review before merge](../standards/review-before-merge.md).

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. Examples: no label, a keyboard trap, focus style removed, an image that conveys information with no `alt` text, a control that cannot be reached from the keyboard and is the only way to finish the task.
- **should fix** — harder to use or inconsistent. Examples: missing `autocomplete`, positive `tabindex`, a hard-coded colour, a target smaller than 24 by 24 CSS pixels, "Change" with no visually hidden text, duplicate `id`s, a disabled submit button. A disabled button is not, by itself, a must fix.
- **consider** — something the code suggests but a person must confirm, such as whether a sticky header actually covers focus. Do not guess a failure you cannot see in the code.

## The standard fix

Restore the installed component markup rather than patching ARIA onto hand-written HTML. Add the missing label, legend, `alt` text, `autocomplete` or visually hidden text the standard describes. Remove `outline: none`, positive `tabindex` and `type="number"`. Take colours, spacing and focus from GOV.UK Frontend. Do not claim the page passes WCAG.

## What a human still has to do

State that a person still needs to test with screen readers, voice control and magnification, and that an audit and an accessibility statement are human work. See [What you cannot check](../standards/accessibility-wcag-2.2-aa.md) and [Accessibility testing](../standards/needs-a-human.md). Automated tools find only some problems. Do not say the page is accessible, compliant or ready for assessment.
