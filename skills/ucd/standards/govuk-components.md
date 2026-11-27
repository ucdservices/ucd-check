# GOV.UK Design System components

A quick reference for choosing and using components. It tells you when to use each one and the mistakes to avoid. It does not contain markup: take that from the installed package or the component's page, so it matches your version.

Official source: https://design-system.service.gov.uk/components/

Each component's page is at `https://design-system.service.gov.uk/components/[name]/`, for example `/components/date-input/`.

## How to use a component

1. Find it in the tables below.
2. With Nunjucks, import the macro from `govuk/components/[name]/macro.njk` and call it. Check the option names in `node_modules/govuk-frontend/dist/govuk/components/[name]/`.
3. With plain HTML, copy the HTML from the component's page for your installed version. Keep every class, attribute and visually hidden element.
4. Do not restyle it. If it does not fit, you probably need a different component or pattern.

Components that need JavaScript: accordion, button (double-click prevention), character count, checkboxes and radios (conditional reveal), error summary (focus), exit this page, file upload (enhanced version), notification banner (focus), password input, service navigation, skip link, tabs. Make sure GOV.UK Frontend JavaScript is initialised. All of them fall back to something usable without it.

## Asking for information

| Component | Macro | Use it for | Do not |
|---|---|---|---|
| Text input | `govukInput` | Short answers of one line. Set a width that matches the expected answer. | Do not use `type="number"`: use `inputmode="numeric"`. Do not disable paste. Do not use placeholder text. |
| Textarea | `govukTextarea` | Answers longer than one line. Set `rows` to suit. | Do not use when you expect a few words. |
| Character count | `govukCharacterCount` | A textarea with a character or word limit. | Do not stop the user typing past the limit. Let them go over and tell them. |
| Radios | `govukRadios` | Choosing one option. Order alphabetically unless there is a clear reason. Add an "or" divider before an option like "None of these". | Do not pre-select an option. Use inline radios only for 2 short options. Do not reveal content from inline radios. |
| Checkboxes | `govukCheckboxes` | Choosing one or more options, or a single confirmation. Add the hint "Select all that apply". Use the "none" behaviour for an exclusive option. | Do not use for a yes or no question. Do not pre-select. |
| Select | `govukSelect` | A last resort in public services. Acceptable for settings and for sorting. | Do not use for long lists: ask a narrowing question first. Never use `multiple`. Do not use for dates. |
| Date input | `govukDateInput` | Dates the user knows or can look up without a calendar. Hint: "For example, 27 3 2007". For date of birth, set `autocomplete` to `bday-day`, `bday-month`, `bday-year`. | Do not use when the user is unlikely to know the exact date. Do not use a native date picker. |
| File upload | `govukFileUpload` | Uploading a file. Say which file types and sizes are accepted. | Do not ask for a file if the user can type the information. |
| Password input | `govukPasswordInput` | Passwords, with a show and hide button. | Do not block paste or password managers. Do not ask users to type it twice. |
| Fieldset | `govukFieldset` | Grouping related fields under a legend, such as an address. Radios, checkboxes and date input include their own. | Do not wrap a single input in one. Do not nest fieldsets if you can avoid it. |
| Button | `govukButton` | Actions. One primary button per page. Secondary for other actions, warning for destructive ones. Start button only on a start page. | Do not disable buttons. Do not use a button to navigate: use a link. Do not put icons in buttons. |
| Error message | `govukErrorMessage` (usually via the field's `errorMessage` option) | The message next to a field that failed validation. | Do not use for problems the user cannot fix, such as eligibility or a service failure. Use a page for those. |
| Error summary | `govukErrorSummary` | The list of errors at the top of the page. Title: "There is a problem". Every item links to its field. | Do not show it without matching messages next to the fields. |

### Conditional reveal: use with care

Radios and checkboxes can reveal a follow-up question. Only use this for a single, simple, related question. If the follow-up has several parts or is complicated, put it on the next page. Only reveal questions, never other content. There is a known issue that screen reader users are not always told when content is revealed.

## Navigation

| Component | Macro | Use it for | Do not |
|---|---|---|---|
| Back link | `govukBackLink` | Going to the previous page in a journey. Place it before `<main>`. | Do not use with breadcrumbs. Do not rely on browser history alone: set a real `href`. |
| Breadcrumbs | `govukBreadcrumbs` | Showing where a page sits in a hierarchy of content. | Do not use in a linear form journey. |
| Skip link | `govukSkipLink` | Always present, provided by the template. | Do not remove it. |
| GOV.UK header | `govukHeader` | The header on services on `gov.uk` domains. | Do not add custom navigation into it. Use service navigation. Do not use on other domains. |
| Generic header | Check the installed package | Services that are not on a `gov.uk` domain or do not use GOV.UK branding. | |
| Service navigation | `govukServiceNavigation` | The service name and top-level navigation links, below the header. | Do not add more than a few links. Do not use for a linear journey that has no sections. |
| GOV.UK footer | `govukFooter` | The footer, with links to cookies, accessibility statement and privacy. | Do not remove the licence and copyright content unless your service does not publish under the Open Government Licence. |
| Pagination | `govukPagination` | Moving between pages of results, or previous and next in a sequence of content. | Do not use to move through a form. |
| Language navigation | Check the installed package | Switching between languages, such as English and Welsh. | |
| Exit this page | `govukExitThisPage` | Services where a user may be at risk if someone sees their screen. Follow the whole "Exit a page quickly" pattern. | Do not add it to ordinary services. |

## Showing information

| Component | Macro | Use it for | Do not |
|---|---|---|---|
| Summary list | `govukSummaryList` | Key and value pairs, such as "Check your answers". Each "Change" link needs visually hidden text naming the row. Summary cards group several lists. | Do not use for tabular data with several columns. |
| Table | `govukTable` | Data users need to compare across rows and columns. Add a caption. Right-align numbers. | Do not use for layout. Do not use for a list of key and value pairs. |
| Task list | `govukTaskList` | A service with several sections the user can complete in any order, with a status for each. | Do not use for a short linear journey. |
| Details | `govukDetails` | Help that only some users need, hidden behind a short link-like summary. | Do not hide information most users need. Do not put it inside hint text. |
| Accordion | `govukAccordion` | Several sections of related content where users need only a few. | Do not use for content everyone needs to read, or in a form. Try better headings and shorter content first. |
| Tabs | `govukTabs` | Switching between related views of content where users need one at a time. | Do not use if users need to compare the tabs or read them in order. Avoid on question pages. |
| Inset text | `govukInsetText` | Setting apart a quote, example or extra detail. | Do not use for warnings. Do not use more than once or twice on a page. |
| Warning text | `govukWarningText` | Something with serious consequences, such as a fine. Has visually hidden "Warning" text. | Do not use for general advice. |
| Notification banner | `govukNotificationBanner` | Telling the user about something not directly related to the page content, or confirming success after an action. | Do not use for validation errors. Do not show more than one. |
| Panel | `govukPanel` | The confirmation at the top of a confirmation page, with a reference number. | Do not use anywhere else. |
| Tag | `govukTag` | A short status, such as "Completed" or "In progress". Sentence case. | Do not use as a link or button. Do not rely on its colour alone. |
| Phase banner | `govukPhaseBanner` | Showing that a service is in alpha or beta, with a feedback link. | Do not show once the service is live. |
| Cookie banner | `govukCookieBanner` | Asking for consent to non-essential cookies. Must work without JavaScript. | Do not show it if the service only uses essential cookies. Do not set non-essential cookies before consent. |
| Feedback | Check the installed package | Collecting feedback about a page or service. | |

The macro names for Generic header, Language navigation and Feedback are not listed here because they are newer components. Find them in `node_modules/govuk-frontend/dist/govuk/components/`. If they are missing, the installed version is older than the component.

## Standard error messages

Use these templates. Replace the bracketed part with the wording from the question.

**Text input**

| Problem | Example |
|---|---|
| Empty | Enter your first name |
| Too long | Address line 1 must be 35 characters or less |
| Too short | Full name must be 2 characters or more |
| Between two lengths | Last name must be between 2 and 35 characters |
| Characters not allowed, and you know which | Town or city must not include è and £ |
| Characters not allowed, and you do not know which | Full name must only include letters a to z, and special characters such as hyphens, spaces and apostrophes |
| Not a number | Hours worked a week must be a number, like 30 |
| Not a whole number | Hours worked a week must be a whole number, like 30 |
| Number too low | Hours worked a week must be 16 or more |
| Number too high | Hours worked a week must be 99 or fewer |
| Number outside a range | Hours worked a week must be between 16 and 99 |
| Money needs pence | How much you earn a week must include pence, like 123.45 or 156.00 |
| Money must not have pence | How much you earn a week must not include pence, like 123 instead of 123.45 |

**Radios**

| Question type | Template |
|---|---|
| Yes or no | Select yes if [whatever it is is true] |
| Two options that are not yes or no | Select if [whatever it is] |
| More than two options | Select [whatever it is] |

**Date input**

| Problem | Example | Highlight |
|---|---|---|
| Nothing entered | Enter your date of birth | Whole date |
| Part missing | Date of birth must include a month | Only the missing fields |
| Not a real date | Date of birth must be a real date | The wrong field, or the whole date if unclear |
| Must be in the past | Date of birth must be in the past | Whole date |
| Must be today or in the past | Date of birth must be today or in the past | Whole date |
| Must be in the future | The date your course ends must be in the future | Whole date |
| Must be after another date | The day your course ends must be after 1 September 2017 | Whole date |
| Must be between two dates | The date your contract started must be between 1 September 2017 and 30 September 2017 | Whole date |

When a date has several problems, show one message. Missing parts come first, then dates that cannot be real, then other rules.

For checkboxes, character count, file upload and textarea, and for the patterns such as addresses, email addresses, names, National Insurance numbers and phone numbers, check the "Error messages" section of that component or pattern's page.

**Rules for every message**

- Say what happened and how to fix it.
- Use an instruction for an empty field ("Enter...") and a description for a wrong one ("... must be ...").
- Use the same words as the question, and the same message in the summary and next to the field.
- Do not use "please", "sorry", "valid", "invalid", "forbidden", "illegal" or "you forgot". No jokes. No jargon.
- Keep the user's answer in the field, even when it is wrong.

## If no component fits

Read `choose-a-component.md`. Do not invent a component without following it.
