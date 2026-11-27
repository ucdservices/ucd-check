# Validation

Error summary, error messages, and server-side validation.

## When this check applies

Run this check when a form can be submitted or a route validates an answer. Skip it for pages with no input, and say why.

## What to look for

The rules are in [Step 5: handle the POST](../standards/build-a-form-page.md), [Step 3](../standards/build-a-form-page.md), [Standard error messages](../standards/govuk-components.md) and the "Recover from validation errors" row of [GOV.UK patterns](../standards/govuk-patterns.md).

- Validate on the server, in the route or controller, using the project's existing approach. Do not validate only in the browser. Do not validate as the user types unless research in this project supports it. See [Step 5](../standards/build-a-form-page.md).
- The form is `<form method="post" novalidate>`. Inputs do not use the `required` attribute. See [Step 4](../standards/build-a-form-page.md).
- When there are errors, re-render the same page with an error summary at the top of `<main>`, titled "There is a problem", with one link per error. Each link's `href` points at the field `id` (the first option for radios and checkboxes, the first field in error for a date). Show the same message next to the field. See [Step 5](../standards/build-a-form-page.md) and [Asking for information](../standards/govuk-components.md).
- The page title starts with "Error: " when errors are shown. See [Step 4](../standards/build-a-form-page.md) and [Page structure](../standards/accessibility-wcag-2.2-aa.md).
- Keep every submitted value in the field, including wrong values. Trim whitespace and accept reasonable variations the pattern names, such as postcode case and spaces in reference numbers. See [Step 5](../standards/build-a-form-page.md).
- After a valid answer, save and redirect. POST, then redirect, then GET. If the user came from check answers, send them back there unless further questions are now needed. See [Step 5](../standards/build-a-form-page.md).
- Messages follow the templates in [Standard error messages](../standards/govuk-components.md) and [Step 3](../standards/build-a-form-page.md). Say what happened and how to fix it. Use "Enter..." for an empty field and "... must be ..." for a wrong one. Use the words from the question. Use the same text in the summary and next to the field. No closing full stop.
- Do not use "please", "sorry", "valid", "invalid", "forbidden", "illegal", "you forgot", "oops" or "error" in the message text. No jokes and no jargon. Be specific: not "This field is required". See [Rules for every message](../standards/govuk-components.md).
- Do not invent validation rules, such as a length limit the data model does not enforce. See [Step 3](../standards/build-a-form-page.md).
- Do not use an error message for something the user cannot fix, such as eligibility or a service failure. Use a page for those. Do not use a notification banner for validation errors. See [Asking for information](../standards/govuk-components.md) and [Showing information](../standards/govuk-components.md).
- In plain HTML the error state needs `govuk-form-group--error`, the error class on the input, a `govuk-error-message` with a visually hidden "Error:" prefix and an `id`, and that `id` on the input's `aria-describedby`. The Nunjucks `errorMessage` option does this. Do not write a separate focus script. The error summary moves focus when GOV.UK Frontend JavaScript is initialised. See [Step 4](../standards/build-a-form-page.md) and [Step 5](../standards/build-a-form-page.md).
- Do not show library default messages, raw error codes, stack traces, field names or enum values. See [Where content lives in the code](../standards/write-page-content.md).

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. Examples: no error message, browser-only validation, an error summary with no matching message by the field, a summary link that does not go to the field, answers wiped after an error.
- **should fix** — harder to use or inconsistent. Examples: "Please enter a valid value", a missing "Error: " prefix on the title, `required` left on an input, no `novalidate`, a message that does not use the question's words.
- **consider** — needs a decision. Example: a length rule that might already exist in the data model. Ask rather than inventing the limit.

## The standard fix

Move the check to the server. Add `novalidate` and remove `required`. On failure, re-render with the error summary and the field message from the templates, keep the posted values, and prefix the title with "Error: ". On success, redirect. Use the project's validation library if it has one, and replace its default text with a message from the templates. Take the error summary and error message markup from the installed package.

## What a human still has to do

Whether the rules match the real policy (what is eligible, which dates are allowed, which formats the back end accepts) needs the person who owns the data. See [What needs a human](../standards/needs-a-human.md). Do not say the form is compliant.
