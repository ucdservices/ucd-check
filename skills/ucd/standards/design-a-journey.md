# Playbook: design a journey

Use this when you are asked to build more than one page: a new service, a new section, or a feature that takes the user through several steps.

This covers what a service designer and an interaction designer would do before any page is built. Do the thinking first, show the developer the plan, then build.

Official sources:

- Question pages: https://design-system.service.gov.uk/patterns/question-pages/
- Check answers: https://design-system.service.gov.uk/patterns/check-answers/
- Complete multiple tasks: https://design-system.service.gov.uk/patterns/complete-multiple-tasks/
- Designing good questions: https://www.gov.uk/service-manual/design/designing-good-questions

## Step 1: understand the task

Before planning pages, write down the answers to these. If you cannot answer one from the request or the codebase, ask the developer.

1. Who is the user, and what are they trying to get done?
2. What does the service need to know to do it? List each piece of information.
3. Why is each piece needed, and what is it used for?
4. What does the user get at the end, and when?
5. What happens to users who are not eligible or cannot continue?
6. Does the user need to gather anything first, such as documents or numbers?
7. Can the user finish in one sitting, or do they need to save and come back?

Do not invent answers. Do not invent user needs or research findings.

## Step 2: write a question protocol

List every piece of information the service will ask for. For each one, record:

| Field | Why it is needed | Who uses the answer | Required? | Could we already know it? |
|---|---|---|---|---|

Then challenge the list:

- Remove anything that is "nice to have" or collected "just in case".
- Remove anything the service already holds or can look up.
- Ask whether an optional question should be asked at all.

Share this table with the developer. It often shows that the journey can be shorter.

## Step 3: put the questions in order

1. **Eligibility first.** Ask the questions that decide whether someone can use the service before anything else. Let people who cannot use it find out fast.
2. **Then the order that makes sense to the user**, not the order of the database. Usually: about the thing they are applying for, then about them, then contact details.
3. **Start easy.** Do not open with the hardest or most sensitive question.
4. **Group related questions** next to each other.
5. **Sensitive and optional questions last**, such as equality information.
6. **Branch, do not show everything.** Use a short filter question to route users past pages that do not apply to them.

## Step 4: choose the shape of the journey

| Shape | Use when | Structure |
|---|---|---|
| Linear | A short task done in one sitting, up to roughly 10 to 15 questions | Start, questions, check answers, confirmation |
| Task list | Several sections, users may leave and return, or sections can be done in any order | Start, task list page, sections each with their own questions and check answers, final declaration, confirmation |
| Add to a list | The user needs to give several of the same thing, such as people or jobs | Question pages for one item, then a summary with "Add another" and "Change" and "Remove" |
| Hub with actions | A staff-facing service where users pick up items and act on them | List or dashboard, item page, action pages, confirmation banners |

Most public-facing services are linear or a task list.

## Step 5: map every page

Write a page list before building. For each page:

| Page | URL path | Type | Comes from | Goes to | Condition |
|---|---|---|---|---|---|

Include all of these, not only the question pages:

- Start page, if it lives inside the service
- Each question page
- Each "you cannot use this service" page, with what to do instead
- Check answers
- Declaration, if needed
- Confirmation
- Sign in or save and return pages, if the service has accounts
- Error pages: page not found, problem with the service, service unavailable
- Session timeout page, if sessions expire
- Cookies, accessibility statement and privacy notice, if they do not exist

URL paths are lower case words with hyphens, describing the page: `/date-of-birth`, not `/step-3` or `/dob`. No personal data in URLs.

## Step 6: define routing

Put routing in one place if the project allows it, so order can change without editing every page.

For each page define:

- **Next**: where the user goes after a valid answer, including each branch.
- **Back**: the page the user actually came from, including when pages were skipped.
- **Change**: when the user arrived from check answers, return them there after saving, unless their new answer means further questions are now needed. In that case, ask those, then return.
- **Guard**: what happens if a user opens the page directly without earlier answers. Usually redirect to the first unanswered page.

When an answer changes and makes later answers irrelevant, remove the irrelevant answers so they are not shown or submitted.

## Step 7: plan what happens around the journey

- **Saving progress.** Keep answers in the session as the user goes. Never lose answers when the user goes back or hits an error.
- **Timeouts.** If the session expires, warn the user first and let them extend it.
- **Confirmation.** The confirmation page shows a reference number and what happens next. Also send it by email or text message, because users close the page.
- **Getting help.** Decide where contact details appear and keep them in the same place on every page.
- **Other channels.** Check there is a route for people who cannot use the online service.
- **Double submission.** Prevent the final submit from running twice.

## Step 8: build

1. Share the question protocol and page list with the developer and wait for agreement, unless they told you to go ahead.
2. Build one page at a time using `build-a-form-page.md`.
3. Build check answers and confirmation using `govuk-patterns.md`.
4. Add journey tests that cover each branch, the back links, and changing an answer from check answers.
5. Finish with `review-before-merge.md`.

## Checklist

- [ ] Every question has a recorded reason
- [ ] Eligibility questions come first, with exit pages for those who do not qualify
- [ ] One thing per page
- [ ] Journey shape chosen and matches the size of the task
- [ ] Page list includes check answers, confirmation and error pages
- [ ] URLs are readable and contain no personal data
- [ ] Back, next and change routes defined for every page, including branches
- [ ] Answers kept on back, on error and on change
- [ ] Stale answers removed when an earlier answer changes
- [ ] Confirmation also sent by email or text message
- [ ] Journey tests cover each branch
