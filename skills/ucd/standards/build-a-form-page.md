# Playbook: build a form page

Use this when you add or change a page that asks the user for information.

This playbook covers what an interaction designer, a content designer and an accessibility specialist would each check. Work through the steps in order.

Official sources:

- Question pages: https://design-system.service.gov.uk/patterns/question-pages/
- Validation: https://design-system.service.gov.uk/patterns/validation/
- Error message: https://design-system.service.gov.uk/components/error-message/
- Error summary: https://design-system.service.gov.uk/components/error-summary/

## Step 1: decide what the page asks

1. **Check the question is needed.** Only ask for information the service will use. If you cannot tell what an answer is used for, ask the developer before building.
2. **One thing per page.** A "thing" is one question or one closely related group, such as the parts of an address or a date. If you are asked to add several unrelated fields to one page, build them as separate pages and say why. The exception is when the project already has research supporting a longer page.
3. **Check it has not been asked already.** If an earlier page collected the same information, reuse it. Do not ask twice.
4. **Decide if everyone needs to see it.** If the question only applies to some users, add a filter question before it and route around it, rather than showing a conditional field to everyone.

## Step 2: choose the component

Pick by the kind of answer, not by how compact it looks.

| The answer is... | Use | Notes |
|---|---|---|
| One choice from a short list | Radios | Order options alphabetically unless there is a clear reason not to. Use an "or" divider before an option like "None of the above". Do not pre-select an option. |
| Yes or no | Radios, inline | Inline only suits 2 short options. Do not reveal content from inline radios. |
| One or more choices | Checkboxes | Add "Select all that apply" as hint text. Use the "none" exclusive option if needed. |
| One choice from a long list | First try an earlier question that narrows the list, then radios. If the list is still long, an autocomplete that enhances a select | Select is a last resort in public-facing services. Many users find it hard to use. |
| Short free text | Text input | Set the width to match the expected answer length. |
| Long free text | Textarea, or character count if there is a limit | |
| A date the user knows, such as a date of birth | Date input (3 fields) | Do not use a calendar picker or `type="date"`. |
| A date the user needs to look up, such as an appointment | Date picker from MoJ if installed, otherwise date input | |
| A whole number, such as a quantity | Text input with `inputmode="numeric"` | Not `type="number"`. |
| Money | Text input with a "£" prefix | Accept commas and pence. |
| A file | File upload | One file per page where possible. |
| A password or security code | Password input, or text input with `autocomplete="one-time-code"` | Always allow paste. |
| An address | The Addresses pattern | Multiple labelled fields with `autocomplete`. |
| A name | The Names pattern | One "Full name" field unless separate parts are needed. |

If none fit, read `choose-a-component.md`.

A full list of standard error messages is in `govuk-components.md`. A worked example of a finished page is on the question pages pattern: https://design-system.service.gov.uk/patterns/question-pages/.

## Step 3: write the content

Write the content before the markup. It decides the structure.

**The question (page heading)**

- Make the question the `<h1>`. For a single field, the `<label>` is the `<h1>`. For a group, the `<legend>` is the `<h1>`.
- Phrase it as a question or a short statement: "What is your date of birth?" or "Your contact details".
- Use sentence case. No full stop on headings.
- Address the user as "you" and the service as "we".

**Hint text**

- Add a hint only if it helps the user answer: the format, where to find the information, or an example.
- One short sentence. No links inside hints.
- For dates, give an example: "For example, 27 3 2007".
- Do not repeat the question.

**Buttons**

- "Continue" to move through a journey.
- "Save and continue" if answers are saved for a returning user.
- A verb that says what happens for a final action, such as "Submit application" or "Accept and send".
- One main button per page. No "Reset" or "Clear" buttons.

**Error messages**

Write one message for each way the answer can be wrong. Each says what happened and how to fix it. Use the same wording in the summary and next to the field.

| Problem | Template | Example |
|---|---|---|
| Empty text field | Enter [whatever it is] | Enter your full name |
| Nothing selected, yes or no question | Select yes if [whatever it is is true] | Select yes if you have a UK passport |
| Nothing selected, more than 2 options | Select [whatever it is] | Select the country where you live |
| Empty date | Enter [the date] | Enter your date of birth |
| Part of a date missing | [The date] must include a [missing part] | Date of birth must include a year |
| Not a real date | [The date] must be a real date | Date of birth must be a real date |
| Date in the wrong period | [The date] must be in the past | Date of birth must be in the past |
| Too long | [Whatever it is] must be [number] characters or less | Address line 1 must be 35 characters or less |
| Wrong format | Enter [whatever it is] in the correct format, like [example] | Enter an email address in the correct format, like name@example.com |
| Not a number | [Whatever it is] must be a number, like [example] | Hours worked must be a number, like 30 |

Rules for error messages:

- Do not use "please", "sorry", "invalid", "valid", "forbidden", "oops" or "error" in the message text.
- Do not blame the user or use technical terms.
- Be specific. "Enter your National Insurance number", not "This field is required".
- Follow the templates, which have no closing full stop.
- Do not invent validation rules, such as length limits. Ask the developer or use what the data model already enforces.

## Step 4: build the page

**Structure**

- Extend the project's existing layout. Do not create a new one.
- Set the page title to: question text, then service name, then "GOV.UK". Prefix with "Error: " when errors are shown.
- Put a back link before `<main>`, in the layout's `beforeContent` block or the project's equivalent.
- Put the form in a two-thirds column: `govuk-grid-row` then `govuk-grid-column-two-thirds`.
- Use `<form method="post" novalidate>`. Include the project's CSRF token if it uses one.
- Do not add the `required` attribute to inputs.

**With Nunjucks**

- Import and use the macro for each component, for example `govukInput`, `govukRadios`, `govukDateInput`, `govukButton`, `govukErrorSummary`, `govukBackLink`.
- To make the question the heading, set `isPageHeading: true` with the large label or legend class (`govuk-label--l` or `govuk-fieldset__legend--l`).
- Pass the error to the macro's `errorMessage` option. The macro then adds the error classes, the visually hidden "Error:" prefix and `aria-describedby` for you.
- Pass the submitted value back in so the user does not lose what they typed.
- Check the macro options against the installed version in `node_modules/govuk-frontend/dist/govuk/components/`. Do not guess option names.

**With plain HTML**

- Copy the component's HTML from the Design System page for the installed version. Keep every class, attribute and visually hidden span.
- In the error state you need all of these: `govuk-form-group--error` on the form group, the error class on the input (such as `govuk-input--error`), a `govuk-error-message` paragraph with a visually hidden "Error:" prefix and an `id`, and that `id` added to the input's `aria-describedby` alongside the hint's `id`.

**Field attributes**

- Give every field a unique `id` and a `name` that matches the project's naming convention.
- Add `autocomplete` for the user's own details.
- Add `spellcheck="false"` for names, emails, reference numbers and codes.
- Choose a width class that matches the expected answer, such as `govuk-input--width-10` for a postcode.
- Add `preventDoubleClick: true` (or `data-prevent-double-click="true"`) to buttons that submit payments or applications.

## Step 5: handle the POST

1. **Validate on the server**, in the route or controller, using the project's existing validation approach.
2. **Trim whitespace** and accept reasonable variations: spaces in reference numbers, upper or lower case postcodes, a leading zero in a day or month.
3. **If there are errors**, re-render the same page with:
   - an error summary at the top of `<main>`, titled "There is a problem", with one link per error
   - each link's `href` pointing to the `id` of the field. For radios and checkboxes, the first option. For dates, the first field that has the error.
   - the error message next to each field
   - every submitted value still filled in
   - "Error: " at the start of the page title
4. **If there are no errors**, save the answer and redirect to the next page. Use POST, then redirect, then GET, so that refresh and back do not resubmit.
5. **If the user came from the "Check your answers" page**, send them back there after they change an answer, not to the next question.
6. **Do not validate as the user types** unless research in this project supports it.

The error summary component moves focus to itself when the page loads, as long as GOV.UK Frontend JavaScript is initialised. Do not write your own focus script.

## Step 6: fit the page into the journey

- Add the new answer to the "Check your answers" page, with a "Change" link that has visually hidden text naming the answer.
- Make the back link go to the previous page in the journey, including when pages were skipped by routing.
- If the page changes who is eligible or what later pages show, update the routing for those pages too.
- If the project has journey or page tests, add or update them.

## Example: what good looks like

A page asking for an email address, in outline:

- Title: "What is your email address? – Apply for a permit – GOV.UK"
- Back link, above the main content
- `<h1>` containing the label: "What is your email address?"
- Hint: "We'll only use this to send you updates about your application"
- One text input, `type="email"`, `autocomplete="email"`, `spellcheck="false"`
- Button: "Continue"
- Errors: "Enter your email address" when empty, and "Enter an email address in the correct format, like name@example.com" when malformed

Common mistakes in this page: a separate `<h1>` and label saying the same thing, placeholder text instead of a hint, a "Submit" button mid-journey, `required` on the input, and a red border with no error text.

## Checklist

Interaction design

- [ ] The page asks one thing
- [ ] The component matches the type of answer
- [ ] The question is the `<h1>`, as a label or legend
- [ ] Back link present and goes to the right page
- [ ] Answer appears on "Check your answers" with a working "Change" link
- [ ] Nothing asked that was already collected

Content design

- [ ] Sentence case, plain English, "you" and "we"
- [ ] Hint text only where it helps, and no placeholder text
- [ ] Button text says what happens
- [ ] An error message written for every validation rule, using the templates
- [ ] No invented rules, legal wording or contact details

Accessibility

- [ ] Label or legend linked to every input
- [ ] Hint and error linked with `aria-describedby`
- [ ] `autocomplete` set where it applies
- [ ] Error summary links go to the right field
- [ ] Page title correct, with "Error: " prefix on failure
- [ ] Works with JavaScript off

Build

- [ ] Server-side validation, `novalidate` on the form, no `required` attributes
- [ ] Submitted values kept after an error
- [ ] POST, redirect, GET
- [ ] Macro options checked against the installed `govuk-frontend` version
- [ ] Tests added or updated

Then run the checks in `accessibility-wcag-2.2-aa.md`.
