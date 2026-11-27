# Playbook: review before merge

Use this when you finish any task that changed something users see, and when you are asked to review someone else's change.

This is the review a design team would give. Go through each section against the actual diff. Do not tick items you have not checked.

## How to run the review

1. List the pages and templates the change touches.
2. For each page, go through sections 1 to 5.
3. For the change as a whole, go through sections 6 and 7.
4. Fix what you can. For anything you cannot fix or are unsure of, report it.
5. Write the summary in section 8.

Rate each problem you find:

- **Blocker**: stops some users completing the task, or breaks a legal requirement. Examples: no label on an input, a keyboard trap, an error with no message.
- **Should fix**: makes the service harder to use or inconsistent. Examples: title case headings, a select where radios fit, missing `autocomplete`.
- **Consider**: an improvement that needs a design decision.

## 1. Structure

- [ ] Extends the project layout, with skip link, header and footer intact
- [ ] Unique, descriptive `<title>` in the standard format
- [ ] Exactly one `h1`, and headings in order
- [ ] Back link or breadcrumbs outside `<main>`, not both
- [ ] Content in a two-thirds column unless it needs more
- [ ] Phase banner present if the service is in alpha or beta

## 2. Components and patterns

- [ ] Every interface element is a GOV.UK or MoJ component, or an existing project component
- [ ] Markup matches the installed version, with nothing removed or restyled
- [ ] The component fits the job. Check against `choose-a-component.md`
- [ ] Nothing from the "avoid" list has slipped in: modals, tooltips, placeholder text, disabled buttons, inline validation
- [ ] Any custom component is justified and listed

## 3. Forms

- [ ] One thing per page
- [ ] Question is the `h1`, as a label or legend
- [ ] `novalidate` on the form, no `required` attributes, validation on the server
- [ ] Error summary and error messages both present, with matching text
- [ ] Error summary links focus the right field
- [ ] "Error: " prefix on the title when errors are shown
- [ ] Answers kept after an error and when going back
- [ ] `autocomplete`, `spellcheck` and `inputmode` set where they apply
- [ ] Paste works in every field
- [ ] POST then redirect

## 4. Content

- [ ] Sentence case on every heading, label, button, link and tag
- [ ] Plain English, short sentences, "you" and "we"
- [ ] Buttons and links describe what they do
- [ ] Error messages follow the templates, with no "please", "sorry", "valid" or "invalid"
- [ ] Dates, times, numbers and money in GOV.UK format
- [ ] Same names for the same things as the rest of the service
- [ ] No invented facts. Placeholders marked and listed
- [ ] No internal names, codes or library default messages shown to users

## 5. Accessibility

- [ ] Every input has a visible, linked label
- [ ] Groups have a fieldset and legend
- [ ] Hints and errors linked with `aria-describedby`
- [ ] All controls reachable and usable by keyboard, in a sensible order
- [ ] Focus always visible and not hidden behind anything
- [ ] No colour-only meaning, no hard-coded colours
- [ ] Images have suitable `alt` text
- [ ] Works at 320 pixels wide and 400% zoom
- [ ] Works with JavaScript off
- [ ] Targets at least 24 by 24 CSS pixels
- [ ] Dynamic updates announced with the right live region
- [ ] Automated accessibility tests run and passing, or their absence reported

Full detail: `accessibility-wcag-2.2-aa.md`.

## 6. Journey

- [ ] Next, back and change routes work for every branch
- [ ] Opening a page out of order is handled
- [ ] New answers appear on check answers
- [ ] Changing an earlier answer clears answers it makes irrelevant
- [ ] No dead ends. Every page has a way forward
- [ ] Confirmation says what happens next
- [ ] Nothing is asked twice
- [ ] Error pages exist for not found, problem with the service and unavailable

## 7. Code quality that affects users

- [ ] No personal data in URLs, logs or analytics
- [ ] CSRF protection on forms, following the project's approach
- [ ] No new frontend dependency added without agreement
- [ ] No overrides of `govuk-` or `moj-` classes
- [ ] Custom CSS uses the project prefix and GOV.UK mixins
- [ ] User-facing strings in the project's content or locale files
- [ ] Tests added or updated for new pages, validation and routing
- [ ] No secrets or real personal data in code, fixtures or tests

## 8. Write the summary

End every task with a summary in this shape. Keep it short and factual.

**What changed**
The pages added or changed, in a sentence or two.

**Standards applied**
Components and patterns used. Any custom component, with the reason.

**Problems found and fixed**
Anything from this review you corrected.

**Problems not fixed**
Each one with its rating (blocker, should fix or consider) and why you left it.

**Placeholders and assumptions**
Any content you could not source, and any decision you made without confirmation.

**Needs a human**
What you could not check. Always include, where relevant: testing with assistive technology, testing with users, content review of placeholders, and translation. See `needs-a-human.md`.

Do not say a page "is accessible" or "meets WCAG 2.2 AA". Say what you checked and what still needs checking.
