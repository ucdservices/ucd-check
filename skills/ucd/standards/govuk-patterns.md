# GOV.UK Design System patterns

Patterns are tested ways of solving common problems using components. Before you design a page or journey, check whether a pattern already covers it. If one does, follow it.

Official source: https://design-system.service.gov.uk/patterns/

Each pattern's page is at `https://design-system.service.gov.uk/patterns/[name]/`, for example `/patterns/check-answers/`. Read the page before building. The notes below are a summary to help you pick, not a replacement.

## Ask users for...

| Pattern | Key points |
|---|---|
| Addresses | Use several labelled text inputs: address line 1, address line 2 (optional), town or city, county (optional), postcode. Set `autocomplete` on each. Or use a postcode lookup with a manual entry fallback. Accept postcodes in any case, with or without a space. |
| Bank details | Name on the account, sort code, account number. Accept sort codes with or without hyphens or spaces. Say where to find the details. |
| Dates | Use the date input for dates users know. For approximate dates, ask only for what you need, such as month and year. Write dates out as "27 March 2007". |
| Email addresses | One field, `type="email"`, `autocomplete="email"`, `spellcheck="false"`. Say why you need it. Do not ask users to type it twice. Confirm it by sending an email if it matters. |
| Equality information | Optional, with "Prefer not to say" options. Use the standard question wording. Ask at the end, and explain why. Do not write your own versions of these questions. |
| Names | A single "Full name" field where you can. Use separate first and last name fields only if the service needs them apart. Do not ask for a title. Allow long names, hyphens, apostrophes and accents. Turn spellcheck off. |
| National Insurance numbers | One text input. Accept spaces and any case. Hint with the example format and where to find it. Turn spellcheck off. |
| Passwords | Use the password input. Allow paste and password managers. Say the rules up front. Do not ask for it twice. Do not set complicated composition rules. |
| Payment card details | Use GOV.UK Pay where possible. Do not build your own card form unless the team has decided to. |
| Phone numbers | One field, `type="tel"`, `autocomplete="tel"`. Accept spaces, brackets, dashes and country codes. Say why you need it. Errors: "Enter a UK phone number" when empty, and "Enter a phone number, like 01632 960 001, 07700 900 982 or +44 808 157 0192" when the format is wrong. |

## Help users to...

| Pattern | Key points |
|---|---|
| Check a service is suitable | Ask a few short filter questions at the start so users do not waste time. Send people who are not eligible to a page that explains why and what to do instead. |
| Check answers | Before submitting, show every answer in summary lists with "Change" links. Each link returns to the question, pre-filled, then back to this page. Group under headings for long journeys. The button says what happens, such as "Accept and send". |
| Complete multiple tasks | Use a task list page when a service has several sections, may take more than one sitting, or sections can be done in any order. Show a status for each task. |
| Confirm a phone number | Send a security code by text message. One input, `autocomplete="one-time-code"`, `inputmode="numeric"`. Give a way to request a new code. |
| Confirm an email address | Send a link or code by email. Tell the user to check their inbox and what to do if it does not arrive. |
| Contact a department or service team | Show contact details as text with opening hours and call charges link. Offer more than one channel. Put them in the same place on every page. |
| Create a username | Prefer the email address as the username. |
| Create accounts | Only ask users to create an account if it clearly helps them. Prefer GOV.UK One Login if the project uses it. Let users do as much as possible before signing in. |
| Exit a page quickly | For services where users may be at risk. Includes the "Exit this page" component, a keyboard shortcut and an explanatory page. Follow the whole pattern or do not use it. |
| Navigate a service | Use the service navigation component for top-level sections. Keep the number of links small. Highlight the current section. |
| Recover from validation errors | Error summary at the top, error messages by the fields, "Error: " in the title, answers kept. Server-side validation. See `build-a-form-page.md`. |
| Start using a service | Most services start from a page on GOV.UK. If the start page is in the service, it has a short description, what the user needs, and a green "Start now" button. |

## Pages

| Pattern | Key points |
|---|---|
| Confirmation pages | A panel with "Application complete" or similar and a reference number, then what happens next and when. Include contact details and a feedback link. Do not rely on the user remembering it: also send an email. |
| Cookies page | Lists the cookies used, grouped by purpose, with a form to change consent. Needed if the service sets any cookies. |
| Interruption pages | A rare, full-page warning before something unusual or risky. Do not use for routine confirmation. |
| Page not found pages | For a 404. Title "Page not found". Suggest checking the address and give a way to continue. No "404", no jokes, no red text. |
| Question pages | One question per page, question as the `h1`, back link, "Continue" button. See `build-a-form-page.md`. |
| Service unavailable pages | For planned or unplanned downtime. Say when the service will be back if known, and what the user can do meanwhile. Return a 503. |
| Step by step navigation | For GOV.UK content journeys that span several services. Rarely built inside a transactional service. |
| There is a problem with the service pages | For a 500. Title "Sorry, there is a problem with the service". Say whether answers were saved and how to contact the team. Do not show technical details. |

## Patterns that cover a whole journey

A typical transactional service is built from these, in this order:

1. Start page
2. Check a service is suitable (filter questions)
3. Question pages, one thing per page
4. Check answers
5. Declaration, if one is needed, with a button such as "Accept and send"
6. Confirmation page, plus an email or text message

Longer services wrap steps 3 and 4 in a task list.

See `design-a-journey.md` for how to plan this.

## If no pattern fits

- Check the MoJ patterns in `moj-components-and-patterns.md`.
- Check whether the department has its own design system. Many do, including HMRC, DWP, Home Office, DfE and NHS. Ask the developer which applies.
- If you still have nothing, build from GOV.UK components, keep it simple, and flag in your summary that the design is untested and needs review by a designer and testing with users.
