# Playbook: write page content

Use this when you write or edit anything a user reads. It covers what a content designer would do. The detailed style rules are in `govuk-content-style.md`. This playbook is the process.

Official sources:

- Content design: planning, writing and managing content: https://www.gov.uk/guidance/content-design
- Writing for user interfaces: https://www.gov.uk/service-manual/design/writing-for-user-interfaces

## Step 1: know what the content is for

Answer these before writing:

1. What does the user need to do or know on this page?
2. What do they already know when they arrive?
3. What is the one thing they must not miss?

If the page has no clear purpose, it may not need to exist. Say so.

## Step 2: find the facts

Content in a government service has consequences. Getting it wrong can cost someone money or a deadline.

- Take facts from the developer, the existing codebase, or documents you have been given: eligibility rules, fees, time limits, legal wording, contact details, opening hours.
- **Never invent them.** If a fact is missing, use a visible placeholder such as `[CONTENT NEEDED: processing time]` and list it in your summary.
- Do not rewrite legal declarations, privacy wording or statutory text. Leave them exactly as given and flag if they are hard to read.
- Do not copy content from another service and assume it applies.

## Step 3: write it

Write in this order.

1. **The `h1`.** A question for a question page. A plain description for anything else. This also becomes the start of the page title.
2. **What the user must do**, as the first thing after the heading.
3. **Only then, supporting detail**, and only if it changes what the user does.
4. **The action**: the button or link that moves them on.

As you write:

- Use the words users use, not internal names. If the codebase calls it `applicant_ref`, the user sees "application number".
- Use the same name for the same thing on every page.
- One idea per paragraph. Short paragraphs.
- Use a bulleted list when a sentence has 3 or more items.
- Use an `h2` when content has more than one topic.
- Put information where the user needs it. Do not front-load a page with everything they might need later.

## Step 4: place help correctly

Choose by who needs it.

| Who needs it | Where it goes |
|---|---|
| Everyone answering the question | Hint text, or a short paragraph above the field |
| Some users | Details component, below the field it relates to |
| Users who are stuck | Contact details, in the same place on every page |
| Nobody on this page | Remove it |

Do not use tooltips, placeholder text or content that appears on hover.

## Step 5: write the microcopy

| Element | Rule |
|---|---|
| Page title | Same as the `h1`, then service name, then "GOV.UK" |
| Back link | "Back" |
| Buttons | Verb first: "Continue", "Save and continue", "Accept and send" |
| "Change" links | "Change" plus visually hidden text naming the answer |
| Optional fields | "(optional)" at the end of the label |
| Hints | Format or example only. "For example, 27 3 2007" |
| Error summary title | "There is a problem" |
| Error messages | From the templates in `govuk-components.md` |
| Confirmation panel | What was done, past tense: "Application complete" |
| Status tags | One or two words, sentence case: "Not yet started", "Completed" |
| Empty states | Say there is nothing yet and what the user can do: "You have no saved applications" |
| Loading states | Say what is happening in text, not only a spinner |

## Step 6: write the pages around the journey

These are often forgotten. Check they exist and read well.

- **Not eligible pages.** Say clearly that the user cannot use the service, why, and what they can do instead. Do not use the word "sorry" more than once, and do not blame them.
- **Confirmation page.** Reference number, what happens next, when, and what to do if it does not.
- **Problem with the service.** Say whether answers were saved, and how to contact the team.
- **Page not found.** Suggest checking the address. Give a link to continue.
- **Timeout page.** Say what happened and whether answers were kept.
- **Emails and text messages.** Same names, same reference number, same tone as the pages.

## Step 7: edit

Read what you wrote and cut it.

1. Remove any sentence the user does not need in order to act.
2. Replace long words with short ones using the table in `govuk-content-style.md`.
3. Split sentences over 25 words.
4. Change passive to active.
5. Check sentence case on every heading, label, button and link.
6. Read it aloud. If it sounds like a letter from a solicitor, rewrite it.
7. Check every number, date and amount against its source.

## Where content lives in the code

- Follow the project's convention. If it uses locale or translation files, put strings there, not in templates.
- Do not put user-facing text in JavaScript, in validation libraries' default messages, or in database error text. Override library defaults with messages written from the templates.
- Do not show raw error codes, stack traces, field names or enum values to users. Map them to plain English.
- Keep content out of images.

## Checklist

- [ ] Page has one clear purpose and the `h1` states it
- [ ] Facts come from a source, and missing ones are placeholders listed in the summary
- [ ] Legal and statutory wording left unchanged
- [ ] The action is clear and the button says what happens
- [ ] Help placed by who needs it
- [ ] Same thing called the same name on every page, and in emails
- [ ] No library default messages, error codes or internal field names shown to users
- [ ] Edited for length, plain words and active voice
- [ ] Style rules in `govuk-content-style.md` checked
- [ ] Translation flagged if the service is bilingual
