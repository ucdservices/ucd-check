# Question pages

One question per page. Labels, hints, legends and fieldsets match the question page pattern.

## When this check applies

Run this check when a page asks the user for information: a form, a question template, or a route that renders one. Skip it for pages that do not ask a question, such as a start page, a content page or a confirmation page, and say why.

## What to look for

The rules are in [build a form page](../standards/build-a-form-page.md) and the question pages row of [GOV.UK patterns](../standards/govuk-patterns.md).

- One thing per page. A thing is one question or one closely related group, such as an address or a date. Unrelated fields are separate pages, unless the project already has research that supports a longer page. See [Step 1: decide what the page asks](../standards/build-a-form-page.md).
- Do not ask for information the service will not use, and do not ask again for something an earlier page collected. If a question applies only to some people, use a filter question and route around it instead of showing it to everyone. See [Step 1](../standards/build-a-form-page.md).
- The question is the `<h1>`. For a single field, the `<label>` is the `<h1>`. For a group, the `<legend>` is the `<h1>`. With Nunjucks, that is `isPageHeading: true` and the large label or legend class. See [Step 3](../standards/build-a-form-page.md) and [Step 4](../standards/build-a-form-page.md).
- Radios, checkboxes and date fields sit in a fieldset with a legend that asks the question. Do not wrap a single input in a fieldset. See [Forms](../standards/accessibility-wcag-2.2-aa.md) and [Asking for information](../standards/govuk-components.md).
- Every input has a visible label linked by `for` and `id`. Placeholder text is not a label, and placeholder text is not used. See [Forms](../standards/accessibility-wcag-2.2-aa.md).
- Hint text is used only when it helps: the format, where to find the information, or an example. Keep it short. One sentence is the usual length. A pattern can ask for both the format and where to find the information, as the National Insurance hint does, and that may be two sentences. No links inside hints. Do not repeat the question. Dates use an example such as "For example, 27 3 2007". See [Step 3](../standards/build-a-form-page.md), [Ask users for...](../standards/govuk-patterns.md) and [Labels, legends and hints](../standards/govuk-content-style.md).
- Help that only some people need goes in a details component, not in the hint and not in a tooltip. See [Step 4: place help correctly](../standards/write-page-content.md).
- Choose the control from [Step 2: choose the component](../standards/build-a-form-page.md): radios for one choice from a short list, inline radios only for two short options such as yes or no, checkboxes for one or more with the hint "Select all that apply", text input for short text, textarea for long text, date input for a date the user knows, no native date picker and no `type="date"` for that case.
- The page has a back link before `<main>`, a two-thirds column, and a "Continue" button (or "Save and continue" when answers are saved). One main button. No "Reset" or "Clear". See [Step 3](../standards/build-a-form-page.md) and [Step 4](../standards/build-a-form-page.md).
- The page title is the question, then the service name, then "GOV.UK". See [Step 4](../standards/build-a-form-page.md).
- Mark optional fields with "(optional)" at the end of the label. Do not mark required fields and do not use asterisks. See [Labels, legends and hints](../standards/govuk-content-style.md).

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. Examples: an input with no visible label, a group of radios or checkboxes with no legend, more than one unrelated question on the page when nothing in the project says that was researched.
- **should fix** — harder to use or inconsistent. Examples: the question is not the `<h1>`, a hint missing where the format is easy to get wrong, placeholder text used as the hint, no back link, a "Submit" button in the middle of a journey.
- **consider** — needs a design decision. Example: a longer page that the project might already have research for. Ask before treating it as a fault.

## The standard fix

Split unrelated questions onto separate pages. Make the label or legend the only `<h1>`. Add the hint, fieldset and legend the pattern describes. Remove placeholder text. Point the back link at the previous page in the journey. Use the component from [Step 2](../standards/build-a-form-page.md), taken from the installed package. Do not invent a layout.

## What a human still has to do

Whether one thing per page is right for these users is a research question when the project has no recorded decision. Wording of the question needs a content designer when the subject is eligibility, money, or the law. See [What needs a human](../standards/needs-a-human.md). Do not say the page is compliant.
